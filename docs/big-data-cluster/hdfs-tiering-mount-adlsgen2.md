---
title: HDFS 계층화를 위한 ADLS Gen2 탑재
titleSuffix: How to mount ADLS Gen2
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 HDFS에 외부 Azure Data Lake Storage 파일 시스템을 탑재 하도록 HDFS 계층화를 구성 하는 방법을 설명 합니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7d8a6dd53452700853dca9774ed0196ed7546fe
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419350"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>빅 데이터 클러스터에서 HDFS 계층화에 대 한 ADLS Gen2를 탑재 하는 방법

다음 섹션에서는 Azure Data Lake Storage Gen2 데이터 원본을 사용 하 여 HDFS 계층화를 구성 하는 방법의 예를 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a>Azure Data Lake Storage에 데이터 로드

다음 섹션에서는 HDFS 계층화 테스트를 위한 Azure Data Lake Storage Gen2를 설정 하는 방법을 설명 합니다. Azure Data Lake Storage에 저장 된 데이터가 이미 있는 경우이 섹션을 건너뛰고 사용자 고유의 데이터를 사용할 수 있습니다.

1. [Data Lake Storage Gen2 기능을 사용 하 여 저장소 계정을 만듭니다](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. 외부 데이터에 대 한이 저장소 계정에 [blob 컨테이너를 만듭니다](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) .

1. CSV 또는 Parquet 파일을 컨테이너에 업로드 합니다. 빅 데이터 클러스터의 HDFS에 탑재 되는 외부 HDFS 데이터입니다.

## <a name="credentials-for-mounting"></a>탑재를 위한 자격 증명

## <a name="use-oauth-credentials-to-mount"></a>OAuth 자격 증명을 사용 하 여 탑재

OAuth 자격 증명을 사용 하 여 탑재 하려면 아래 단계를 수행 해야 합니다.

1. [Azure Portal](https://portal.azure.com) 로 이동 합니다.
1. 왼쪽 탐색 창에서 "서비스"로 이동 하 고 "Azure Active Directory"의 시계
1. 메뉴에서 "앱 등록"을 사용 하 여 "웹 응용 프로그램을 만들고 마법사를 따릅니다. **여기서 만든 이름을 명심**하세요. 이 이름을 권한 있는 사용자로 ADLS 계정에 추가 해야 합니다.
1. 웹 응용 프로그램을 만든 후에는 앱에 대 한 "설정"의 "키"로 이동 합니다.
1. 키 기간을 선택 하 고 저장을 클릭 합니다. **생성 된 키를 저장 합니다.**
1.  앱 등록 페이지로 돌아가서 위쪽의 "끝점" 단추를 클릭 합니다. **"토큰 끝점" URL을 적어둡니다.**
1. 이제 OAuth에 대해 다음과 같은 항목이 표시 됩니다.

    - 3 단계에서 만든 웹 앱의 "응용 프로그램 ID"
    - 5 단계에서 방금 생성 한 키
    - 6 단계의 토큰 끝점

### <a name="adding-the-service-principal-to-your-adls-account"></a>ADLS 계정에 서비스 사용자 추가

1. 포털로 다시 이동 하 여 ADLS 계정을 열고 왼쪽 메뉴에서 액세스 제어 (IAM)를 선택 합니다.
1. "역할 할당 추가"를 선택 하 고 위의 3 단계에서 만든 이름을 검색 합니다. 목록에는 표시 되지 않지만 전체 이름을 검색 하면 검색 됩니다.
1. 이제 "저장소 Blob 데이터 참가자 (미리 보기)" 역할을 추가 합니다.

탑재에 자격 증명을 사용 하기 전에 5-10 분 동안 기다립니다.

### <a name="set-environment-variable-for-oauth-credentials"></a>OAuth 자격 증명에 대 한 환경 변수 설정

빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다. 다음 형식을 사용 하 여 환경 변수를 설정 합니다. 자격 증명은 쉼표로 구분 된 목록에 있어야 합니다. Windows에서 ' set ' 명령이 사용 됩니다. Linux를 사용 하는 경우 대신 ' export '를 사용 합니다.

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>액세스 키를 사용 하 여 탑재

Azure Portal에서 ADLS 계정에 대해 얻을 수 있는 액세스 키를 사용 하 여 탑재할 수도 있습니다.

 > [!TIP]
   > 저장소 계정에 대 한 액세스 키 (`<storage-account-access-key>`)를 찾는 방법에 대 한 자세한 내용은 [계정 키 및 연결 문자열 보기](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string)를 참조 하세요.

### <a name="set-environment-variable-for-access-key-credentials"></a>액세스 키 자격 증명에 대 한 환경 변수 설정

1. 빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다.

1. 빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다. 다음 형식을 사용 하 여 환경 변수를 설정 합니다. 자격 증명은 쉼표로 구분 된 목록에 있어야 합니다. Windows에서 ' set ' 명령이 사용 됩니다. Linux를 사용 하는 경우 대신 ' export '를 사용 합니다.

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a>원격 HDFS 저장소 탑재

이제 액세스 키 또는 OAuth를 사용 하 여 MOUNT_CREDENTIALS 환경 변수를 설정 했으므로 탑재를 시작할 수 있습니다. 다음 단계는 Azure Data Lake의 원격 HDFS 저장소를 빅 데이터 클러스터의 로컬 HDFS 저장소에 탑재 합니다.

1. **Kubectl** 를 사용 하 여 빅 데이터 클러스터의 끝점 **컨트롤러 svc 외부** 서비스에 대 한 IP 주소를 찾습니다. **외부 IP**를 찾습니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 클러스터 사용자 이름 및 암호를 사용 하 여 컨트롤러 끝점의 외부 IP 주소를 사용 하 여 **azdata** 로 로그인 합니다.

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. 환경 변수 설정 MOUNT_CREDENTIALS (지침을 보려면 위로 스크롤).

1. **Azdata bdc 저장소 풀 탑재 만들기**를 사용 하 여 Azure에서 원격 HDFS 저장소를 탑재 합니다. 다음 명령을 실행 하기 전에 자리 표시자 값을 바꿉니다.

   ```bash
   azdata bdc storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > Mount create 명령은 비동기입니다. 지금은 마운트가 성공적으로 수행 되었는지 여부를 나타내는 메시지가 없습니다. 탑재 상태를 확인 하려면 [상태](#status) 섹션을 참조 하세요.

성공적으로 탑재 된 경우 HDFS 데이터를 쿼리하고이 데이터에 대 한 Spark 작업을 실행할 수 있어야 합니다. 로 `--mount-path`지정 된 위치에 있는 빅 데이터 클러스터의 HDFS에 표시 됩니다.

## <a id="status"></a>탑재 상태 가져오기

빅 데이터 클러스터의 모든 탑재 상태를 나열 하려면 다음 명령을 사용 합니다.

```bash
azdata bdc storage-pool mount status
```

HDFS의 특정 경로에 탑재 상태를 나열 하려면 다음 명령을 사용 합니다.

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>탑재 새로 고침

다음 예에서는 탑재를 새로 고칩니다.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>탑재 삭제

탑재를 삭제 하려면 **azdata bdc 저장소-풀 탑재 삭제** 명령을 사용 하 고 HDFS에서 탑재 경로를 지정 합니다.

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
