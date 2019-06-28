---
title: HDFS 계층화를 위한 ADLS Gen2 탑재
titleSuffix: How to mount ADLS Gen2
description: 이 문서에는 HDFS에 계층화 (미리 보기)는 SQL Server 2019 빅 데이터 클러스터에서 HDFS에 외부 Azure 데이터 레이크 저장소 파일 시스템 탑재를 구성 하는 방법을 설명 합니다.
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 06/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1d06b668a6c8badef75a0e90d3f58b67b1269984
ms.sourcegitcommit: ab867100949e932f29d25a3c41171f01156e923d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67419048"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>빅 데이터 클러스터에 계층화 하는 HDFS에 대 한 탑재 ADLS Gen2 하는 방법

다음 섹션에서는 Azure Data Lake 저장소 Gen2 데이터 원본을 사용 하 여 계층화 하는 HDFS를 구성 하는 방법의 예제를 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a id="load"></a> Azure Data Lake Storage로 데이터 로드

다음 섹션에서는 HDFS 계층으로 구성 테스트에 대 한 Azure Data Lake 저장소 Gen2를 설정 하는 방법을 설명 합니다. Azure Data Lake Storage에 저장 된 데이터에 이미 있는 경우에 고유한 데이터를 사용 하려면이 섹션을 건너뛸 수 있습니다.

1. [Data Lake 저장소 Gen2 기능을 사용 하 여 저장소 계정 만들기](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account)합니다.

1. [Blob 컨테이너 만들기](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) 외부 데이터에 대 한이 저장소 계정에 있습니다.

1. 컨테이너에 CSV 또는 Parquet 파일을 업로드 합니다. 이 빅 데이터 클러스터의 HDFS에 탑재 하는 외부 HDFS 데이터입니다.

## <a name="credentials-for-mounting"></a>탑재에 대 한 자격 증명

## <a name="use-oauth-credentials-to-mount"></a>OAuth 자격 증명을 사용 하 여 탑재

수행 해야 OAuth 자격 증명을 사용 하 여 탑재 하려면는 아래 단계:

1. 로 이동 합니다 [Azure portal](https://portal.azure.com)
1. 왼쪽된 탐색 창에서 "서비스"로 이동한 후 "Azure Active directory" 클록
1. "앱 등록"을 사용 하 여 메뉴에서 "웹 응용 프로그램을 만들고를 마법사에 따라 합니다. **여기에서 만든 이름을 기억할**합니다. 권한 있는 사용자로 ADLS 계정에이 이름을 추가 해야 합니다.
1. 웹 응용 프로그램을 만든 후 "키" "설정" 아래에서 앱으로 이동 합니다.
1. 저장 키 기간 및 클릭을 선택 합니다. **생성 된 키를 저장 합니다.**
1.  앱 등록 페이지로 돌아가서 맨 위에 있는 "끝점" 단추를 클릭 합니다. **"토큰 끝점" URL 아래로 note**
1. OAuth 용 적어둔 다음 작업을 이제 있어야 합니다.

    - 웹 앱의 "응용 프로그램 ID" 위의 단계에서 만든 3
    - 5 단계에서 생성 된 키
    - 6 단계에서 토큰 끝점

### <a name="adding-the-service-principal-to-your-adls-account"></a>ADLS 계정에 서비스 주체 추가

1. 포털에 다시 및 ADLS 계정을 열고 이동한 왼쪽된 메뉴에서 액세스 제어 (IAM)를 선택 합니다.
1. "역할 할당 추가"를 선택 하 고 (해당 목록에 표시 되지 않습니다 하지만 전체 이름을 찾을 경우 검색할 참고) 위의 3 단계에서 만든 이름을 검색 합니다.
1. 이제 "Storage Blob 데이터 기여자 (미리 보기)" 역할을 추가 합니다.

탑재에 대 한 자격 증명을 사용 하기 전에 5-10 분 동안 기다린 후

### <a name="set-environment-variable-for-oauth-credentials"></a>OAuth 자격 증명에 대 한 환경 변수 설정

빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다. 다음 형식을 사용 하 여 환경 변수를 설정 합니다. 쉼표에 자격 증명 해야 하는 구분 된 목록입니다. 'Set' 명령은 Windows에서 사용 됩니다. Linux를 사용 하는 경우 다음 '내보내기' 대신 사용 합니다.

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>액세스 키를 사용 하 여 탑재

Azure portal에서 ADLS 계정에 액세스할 수 있는 액세스 키를 사용 하 여 탑재할 수 있습니다.

 > [!TIP]
   > 액세스 키를 찾는 방법에 대 한 자세한 내용은 (`<storage-account-access-key>`) 저장소 계정에 대 한 참조 [계정 키 및 연결 문자열 보기](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string)합니다.

### <a name="set-environment-variable-for-access-key-credentials"></a>액세스 키 자격 증명에 대 한 환경 변수 설정

1. 빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다.

1. 빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다. 다음 형식을 사용 하 여 환경 변수를 설정 합니다. 쉼표에 자격 증명 해야 하는 구분 된 목록입니다. 'Set' 명령은 Windows에서 사용 됩니다. Linux를 사용 하는 경우 다음 '내보내기' 대신 사용 합니다.

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> 원격 HDFS 저장소를 탑재 합니다.

액세스 키 또는 OAuth를 사용 하 여 MOUNT_CREDENTIALS 환경 변수를 사용 하도록 설정한 했으므로 탑재를 시작할 수 있습니다. 다음 단계를 빅 데이터 클러스터의 로컬 HDFS 저장소에 Azure Data Lake에서 원격 HDFS storage를 탑재 합니다.

1. 사용 하 여 **kubectl** 끝점에 대 한 IP 주소를 찾으려면 **컨트롤러 svc 외부** 빅 데이터 클러스터의 서비스입니다. 검색할 합니다 **EXTERNAL-IP**합니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 사용 하 여 로그인 **mssqlctl** 컨트롤러 끝점의 외부 IP 주소를 사용 하 여 클러스터 사용자 이름 및 암호를 사용 하 여:

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. 환경 변수 설정 MOUNT_CREDENTIALS (지침에 대해 스크롤)

1. 사용 하 여 Azure에서 원격 HDFS storage를 탑재 **mssqlctl bdc 저장소 풀 마운트 만들기**합니다. 다음 명령을 실행 하기 전에 자리 표시자 값을 바꿉니다.

   ```bash
   mssqlctl bdc storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > 탑재 명령 만들기는 비동기적입니다. 이때 탑재 성공 여부를 나타내는 메시지가 없는 합니다. 참조를 [상태](#status) 섹션에 탑재의 상태를 확인 합니다.

성공적으로 탑재 하는 경우 HDFS 데이터를 쿼리하고 대해 Spark 작업을 실행할 수 있어야 합니다. 지정 된 위치에서 빅 데이터 클러스터의 HDFS에 나타나도록 `--mount-path`합니다.

## <a id="status"></a> 탑재의 상태를 가져옵니다.

빅 데이터 클러스터의 모든 탑재의 상태를 나열 하려면 다음 명령을 사용 합니다.

```bash
mssqlctl bdc storage-pool mount status
```

HDFS에서 특정 경로에 탑재의 상태를 나열 하려면 다음 명령을 사용 합니다.

```bash
mssqlctl bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 탑재를 삭제 합니다.

탑재를 삭제 하려면 사용 합니다 **mssqlctl bdc 저장소 풀 마운트 삭제** 명령을 실행 하 고 HDFS의 탑재 경로 지정:

```bash
mssqlctl bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
