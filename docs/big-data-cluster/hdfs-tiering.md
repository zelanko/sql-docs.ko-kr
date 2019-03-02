---
title: HDFS 계층 구성
titleSuffix: SQL Server 2019 big data clusters
description: 이 문서에는 HDFS에 계층화 (미리 보기)는 SQL Server 2019 빅 데이터 클러스터에서 HDFS에 외부 Azure 데이터 레이크 저장소 파일 시스템 탑재를 구성 하는 방법을 설명 합니다.
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 02/29/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 04f493109997d4b673a6a308de5c9ebee6eac7e4
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57239134"
---
# <a name="configure-hdfs-tiering-on-sql-server-2019-big-data-clusters"></a>SQL Server 2019 빅 데이터 클러스터에 계층화 하는 HDFS 구성

HDFS 계층화 할 수 있게 탑재 외부 HDFS 호환 파일 시스템 HDFS에 합니다. 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 계층화 HDFS 구성 하는 방법에 설명 합니다. 이때 CTP 2.3이 문서의 핵심 이기도 Azure Data Lake 저장소 Gen2, 연결할만 지원 합니다.

## <a name="hdfs-tiering-overview"></a>HDFS 계층 개요

계층화 된 응용 프로그램 원활 하 게 처럼 액세스할 수 있습니다 다양 한 외부 저장소의에서 데이터를 HDFS에서 데이터 상주 합니다. 탑재는 HDFS에 외부 파일 시스템에 네임 스페이스를 설명 하는 메타 데이터를 복사한 위치 메타 데이터 작업입니다. 이 메타 데이터와 사용 권한 및 Acl 파일과 외부 디렉터리에 대 한 정보를 포함합니다. 해당 데이터는 데이터 자체에 액세스할 때만 복사 요청 됩니다. 외부 파일 시스템 데이터는 이제 SQL Server 빅 데이터 클러스터에서 액세스할 수 있습니다. 실행할 수 있습니다 Spark SQL 쿼리와 작업이이 데이터에 대해 실행 하는 해당 클러스터에서 HDFS에 저장 하는 로컬 데이터에 대해 동일한 방식.

> [!NOTE]
> 기능은 Microsoft에서 개발한 HDFS 계층화 및 Apache Hadoop 3.1 배포의 일부로 릴리스된 버전으로 합니다. 자세한 내용은 [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806) 세부 정보에 대 한 합니다.

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

## <a id="mount"></a> 원격 HDFS 저장소를 탑재 합니다.

다음 단계를 빅 데이터 클러스터의 로컬 HDFS 저장소로 Azure Data Lake에서 원격 HDFS storage를 탑재 합니다.

1. 빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다.

1. 라는 로컬 파일을 만듭니다 **files.creds** 다음 형식을 사용 하 여 Azure Data Lake 저장소 Gen2 계정 자격 증명을 포함 하는:

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

   > [!TIP]
   > 액세스 키를 찾는 방법에 대 한 자세한 내용은 (`<storage-account-access-key>`) 저장소 계정에 대 한 참조 [액세스 키 보기 및 복사](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys)합니다.

1. 사용 하 여 **kubectl** 에 대 한 IP 주소를 찾으려면 합니다 **끝점 서비스 프록시** 빅 데이터 클러스터의 서비스입니다. 검색할 합니다 **EXTERNAL-IP**합니다.

   ```bash
   kubectl get svc endpoint-service-proxy -n <your-cluster-name>
   ```

1. 사용 하 여 로그인 **mssqlctl** 서비스 프록시 끝점을 사용 하 여 클러스터 사용자 이름 및 암호를 사용 하 여:

   ```bash
   mssqlctl login -e https://<IP-of-endpoint-service-proxy>:30777/ -u <username> -p <password>
   ```

1. 사용 하 여 Azure에서 원격 HDFS storage를 탑재 **mssqlctl 저장소 탑재 만들기**합니다. 다음 명령을 실행 하기 전에 자리 표시자 값을 바꿉니다.

   ```bash
   mssqlctl storage mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --local-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > 탑재 명령 만들기는 비동기적입니다. 이때 탑재 성공 여부를 나타내는 메시지가 없는 합니다. 참조를 [상태](#status) 섹션에 탑재의 상태를 확인 합니다.

성공적으로 탑재 하는 경우 HDFS 데이터를 쿼리하고 대해 Spark 작업을 실행할 수 있어야 합니다. 지정 된 위치에서 빅 데이터 클러스터의 HDFS에 나타나도록 `--local-path`합니다.

## <a id="status"></a> 탑재의 상태를 가져옵니다.

빅 데이터 클러스터의 모든 탑재의 상태를 나열 하려면 다음 명령을 사용 합니다.

```bash
mssqlctl storage mount status
```

HDFS에서 특정 경로에 탑재의 상태를 나열 하려면 다음 명령을 사용 합니다.

```bash
mssqlctl storage mount status --local-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 탑재를 삭제 합니다.

탑재를 삭제 하려면 사용 합니다 **mssqlctl 저장소 탑재 삭제** 명령을 실행 하 고 HDFS의 탑재 경로 지정:

```bash
mssqlctl storage mount delete --local-path <mount-path-in-hdfs>
```

## <a id="issues"></a> 알려진된 문제 및 제한 사항

SQL Server 빅 데이터 클러스터에 계층화 하는 HDFS를 사용 하는 경우 다음 목록에서는 알려진된 문제 및 현재 제한 사항:

- 탑재 되는 외부 디렉터리의 크기는 클러스터의 용량 보다 큰 경우 탑재 실패 합니다.

- 에 걸려 탑재 하는 경우는 `CREATING` 가능성이 못했습니다 오랜 시간, 상태입니다. 이 경우 명령을 취소 하 고 필요한 경우 탑재를 삭제 합니다. 매개 변수 및 자격 증명 올바른지 확인 후 다시 시도 하세요.

- 기존 디렉터리의 탑재를 만들 수 없습니다.

- 기존 탑재 내 탑재를 만들 수 없습니다.

- 탑재 지점의 상위 항목 모두 존재 하지 않는 경우 만들어집니다 권한으로 r-xr-xr-x (555)를 기본값으로 합니다.

- 탑재 생성 되 고 탑재 된 파일의 크기와 수에 따라 다소 시간이 걸릴 수 있습니다. 이 과정에서 탑재에 있는 파일이 사용자에 게 보이지 않습니다. 모든 파일에 기본적으로 임시 경로 추가할 탑재를 만드는 동안 `/_temporary/_mounts/<mount-location>`합니다.

- 탑재 만들기 명령 비동기입니다. 명령이 실행 된 후 탑재의 상태를 이해 하려면 탑재 상태를 확인할 수 있습니다.

- 인수에 대 한 사용 탑재를 만들 때 **-로컬 경로** 는 기본적으로 탑재의 고유 식별자입니다. 다음 명령에서 동일한 문자열 (있는 경우 끝에 "/" 포함)를 사용 합니다.

- 탑재는 읽기 전용입니다. 모든 디렉터리 또는 탑재를 아래에 있는 파일을 만들 수 없습니다.

- 탑재 디렉터리 및 파일을 변경할 수 있는 권장 하지 않습니다. 탑재를 만든 후 모든 변경 내용이 나 업데이트 된 원격 위치에 반영 되지 않습니다의 HDFS에 탑재 합니다. 변경 내용을 원격 위치에서 발생 하는 경우 삭제 하 고 업데이트 된 상태를 반영 하도록 탑재 다시 선택할 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.