---
title: HDFS 계층화를 위한 ADLS Gen2 탑재
titleSuffix: How to mount ADLS Gen2
description: 이 문서에서는 Azure Data Lake Storage Gen2 데이터 원본을 사용하여 HDFS 계층화를 구성하는 방법의 예제가 나와 있습니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/29/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a4bfb894112f071cc7a628146265ede17b3f0a14
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521040"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>빅 데이터 클러스터에 HDFS 계층화를 위한 ADLS Gen2를 탑재하는 방법

다음 섹션에서는 Azure Data Lake Storage Gen2 데이터 원본을 사용하여 HDFS 계층화를 구성하는 방법의 예제를 제공합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [빅 데이터 클러스터 배포](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="load-data-into-azure-data-lake-storage"></a><a id="load"></a> Azure Data Lake Storage에 데이터 로드

다음 섹션에서는 HDFS 계층화 테스트를 위해 Azure Data Lake Storage Gen2를 설정하는 방법을 설명합니다. Azure Data Lake Storage에 데이터가 이미 저장되어 있는 경우, 이 섹션을 건너뛰고 해당 데이터를 사용할 수 있습니다.

1. [Data Lake Storage Gen2 기능을 사용하여 스토리지 계정을 만듭니다](/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. 이 스토리지 계정에 데이터에 사용할 [파일 시스템을 만듭니다](/azure/storage/blobs/data-lake-storage-explorer).

1. CSV 또는 Parquet 파일을 컨테이너에 업로드합니다. 이 파일이 빅 데이터 클러스터의 HDFS에 탑재되는 외부 HDFS 데이터입니다.

## <a name="credentials-for-mounting"></a>탑재를 위한 자격 증명

### <a name="use-oauth-credentials-to-mount"></a>OAuth 자격 증명을 사용하여 탑재

OAuth 자격 증명을 사용하여 탑재하려면 아래 단계를 수행해야 합니다.

1. [Azure Portal](https://portal.azure.com)로 이동
1. “Azure Active Directory”로 이동합니다. 이 서비스는 왼쪽 탐색 모음에서 볼 수 있습니다.
1. 오른쪽 탐색 모음에서 “앱 등록”을 선택하고 새 등록을 만듭니다.
1. “웹 애플리케이션”을 만들고 마법사를 따릅니다. **여기서 만든 앱의 이름을 기억해 두세요**. 이 이름을 권한 있는 사용자로 ADLS 계정에 추가해야 합니다. 앱을 선택할 때 개요에 표시되는 애플리케이션 클라이언트 ID도 기억해 두세요.
1. 웹 애플리케이션이 생성되면 “인증서 및 암호”로 이동해서 **새 클라이언트 암호** 를 만들고 키 지속 기간을 선택합니다. 암호를 **추가** 합니다.
1. 앱 등록 페이지로 돌아가서 맨 위의 “엔드포인트”를 클릭합니다. **“OAuth 토큰 엔드포인트(v2)”** URL을 기록해 둡니다.
1. 이제 OAuth에 대해 적어 둔 다음 정보를 보유하고 있습니다.

    - 웹 애플리케이션의 “애플리케이션 클라이언트 ID”
    - 클라이언트 암호
    - 토큰 엔드포인트

### <a name="adding-the-service-principal-to-your-adls-account"></a>ADLS 계정에 서비스 주체 추가

1. 포털로 다시 이동하여 ADLS 스토리지 계정 파일 시스템으로 이동하고 왼쪽 메뉴에서 Access control (IAM)를 선택합니다.
1. “역할 할당 추가”를 선택합니다. 
1. “Storage Blob 데이터 Contributor” 역할을 선택합니다.
1. 위에서 만든 이름을 검색합니다. 목록에는 표시되지 않지만 전체 이름을 검색하면 찾을 수 있습니다.
1. 역할을 저장합니다.

탑재를 위해 자격 증명을 사용하기 전에 5~10분간 기다립니다.

### <a name="set-environment-variable-for-oauth-credentials"></a>OAuth 자격 증명에 대해 환경 변수 설정

빅 데이터 클러스터에 액세스할 수 있는 클라이언트 머신에서 명령 프롬프트를 엽니다. 다음 형식을 사용하여 환경 변수를 설정합니다. 자격 증명은 쉼표로 구분된 목록에 있어야 합니다. Windows에서는 ‘set’ 명령을 사용합니다. Linux를 사용하는 경우, 대신 ‘export’를 사용합니다.

**참고:** 자격 증명을 입력할 때 쉼표 “,” 사이에 있는 줄 바꿈과 공백을 모두 제거해야 합니다. 아래와 같은 서식은 오직 가독성을 좋게 만들기 위한 용도입니다.

```console
   set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
   fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
   fs.azure.account.oauth2.client.endpoint=[token endpoint],
   fs.azure.account.oauth2.client.id=[Application client ID],
   fs.azure.account.oauth2.client.secret=[client secret]
```

## <a name="use-access-keys-to-mount"></a>액세스 키를 사용하여 탑재

Azure Portal에서 ADLS 계정에 대해 얻을 수 있는 액세스 키를 사용하여 탑재할 수도 있습니다.

 > [!TIP]
   > 스토리지 계정의 액세스 키(`<storage-account-access-key>`)를 찾는 방법에 대한 자세한 내용은 [계정 키 및 연결 문자열 보기](/azure/storage/common/storage-account-keys-manage#view-access-keys-and-connection-string)를 참조하세요.

### <a name="set-environment-variable-for-access-key-credentials"></a>액세스 키 자격 증명에 대해 환경 변수 설정

1. 빅 데이터 클러스터에 액세스할 수 있는 클라이언트 머신에서 명령 프롬프트를 엽니다.

1. 빅 데이터 클러스터에 액세스할 수 있는 클라이언트 머신에서 명령 프롬프트를 엽니다. 다음 형식을 사용하여 환경 변수를 설정합니다. 자격 증명은 쉼표로 구분된 목록에 있어야 합니다. Windows에서는 ‘set’ 명령을 사용합니다. Linux를 사용하는 경우, 대신 ‘export’를 사용합니다.

**참고:** 자격 증명을 입력할 때 쉼표 “,” 사이에 있는 줄 바꿈과 공백을 모두 제거해야 합니다. 아래와 같은 서식은 오직 가독성을 좋게 만들기 위한 용도입니다.

```console
set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
```

## <a name="mount-the-remote-hdfs-storage"></a><a id="mount"></a> 원격 HDFS 스토리지 탑재

이제 액세스 키 또는 OAuth를 사용하여 MOUNT_CREDENTIALS 환경 변수를 설정했으므로 탑재를 시작할 수 있습니다. 다음 단계에서는 빅 데이터 클러스터의 로컬 HDFS 스토리지에 Azure Data Lake의 원격 HDFS 스토리지를 탑재합니다.

1. **kubectl** 을 사용하여 빅 데이터 클러스터에서 엔드포인트 **controller-svc-external** 서비스의 IP 주소를 찾습니다. **External-IP** 를 찾습니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 클러스터 사용자 이름 및 암호와 함께 컨트롤러 엔드포인트의 외부 IP 주소를 사용하여 **azdata** 로 로그인합니다.

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080
   ```
1. 환경 변수 MOUNT_CREDENTIALS를 설정합니다(지침을 보려면 위로 스크롤).

1. **azdata bdc hdfs mount create** 를 사용하여 Azure에 원격 HDFS 스토리지를 탑재합니다. 다음 명령을 실행하기 전에 자리 표시자 값을 바꿉니다.

   ```bash
   azdata bdc hdfs mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > mount create 명령은 비동기입니다. 지금은 탑재의 성공 여부를 나타내는 메시지가 없습니다. 탑재 상태를 확인하려면 [상태](#status) 섹션을 참조하세요.

성공적으로 탑재된 경우 HDFS 데이터를 쿼리하고, 이 데이터에 대해 Spark 작업을 실행할 수 있어야 합니다. 빅 데이터 클러스터의 HDFS에서 `--mount-path`로 지정된 위치에 표시됩니다.

## <a name="get-the-status-of-mounts"></a><a id="status"></a> 탑재 상태 가져오기

빅 데이터 클러스터에 있는 모든 탑재 상태를 나열하려면 다음 명령을 사용합니다.

```bash
azdata bdc hdfs mount status
```

HDFS의 특정 경로에 있는 탑재 상태를 나열하려면 다음 명령을 사용합니다.

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>탑재 새로 고침

다음 예제에서는 탑재를 새로 고칩니다. 이렇게 새로 고치면 탑재 캐시도 지워집니다.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a name="delete-the-mount"></a><a id="delete"></a> 탑재 삭제

탑재를 삭제하려면 **azdata bdc hdfs mount delete** 명령을 사용하고 HDFS의 탑재 경로를 지정합니다.

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
