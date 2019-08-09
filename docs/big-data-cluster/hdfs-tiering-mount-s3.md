---
title: HDFS 계층화를 위한 S3 탑재
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터(미리 보기)의 HDFS에 외부 S3 파일 시스템을 탑재하도록 HDFS 계층화를 구성하는 방법을 설명합니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/31/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 10e7d0e30135622fedfcbe8f8dba67bfaf1908cd
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702873"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>빅 데이터 클러스터에 HDFS 계층화를 위한 S3를 탑재하는 방법

다음 섹션에서는 S3 스토리지 데이터 원본을 사용하여 HDFS 계층화를 구성하는 방법의 예제를 제공합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [빅 데이터 클러스터 배포](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- 데이터 만들기 및 S3 버킷에 업로드 
  - CSV 또는 Parquet 파일을 S3 버킷에 업로드합니다. 이 파일이 빅 데이터 클러스터의 HDFS에 탑재되는 외부 HDFS 데이터입니다.

## <a name="access-keys"></a>액세스 키

### <a name="set-environment-variable-for-access-key-credentials"></a>액세스 키 자격 증명에 대해 환경 변수 설정

빅 데이터 클러스터에 액세스할 수 있는 클라이언트 머신에서 명령 프롬프트를 엽니다. 다음 형식을 사용하여 환경 변수를 설정합니다. 자격 증명은 쉼표로 구분된 목록에 있어야 합니다. Windows에서는 ‘set’ 명령을 사용합니다. Linux를 사용하는 경우, 대신 ‘export’를 사용합니다.

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > S3 액세스 키를 만드는 방법에 대한 자세한 내용은 [S3 액세스 키](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)를 참조하세요.

## <a id="mount"></a> 원격 HDFS 스토리지 탑재

이제 액세스 키를 사용하여 자격 증명 파일을 준비했으므로 탑재를 시작할 수 있습니다. 다음 단계에서는 빅 데이터 클러스터의 로컬 HDFS 스토리지에 S3의 원격 HDFS 스토리지를 탑재합니다.

1. **kubectl**을 사용하여 빅 데이터 클러스터에서 엔드포인트 **controller-svc-external** 서비스의 IP 주소를 찾습니다. **External-IP**를 찾습니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 클러스터 사용자 이름 및 암호와 함께 컨트롤러 엔드포인트의 외부 IP 주소를 사용하여 **azdata**로 로그인합니다.

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. 위의 지침에 따라 환경 변수 MOUNT_CREDENTIALS를 설정합니다.

1. **azdata bdc storage-pool mount create**를 사용하여 Azure에 원격 HDFS 스토리지를 탑재합니다. 다음 명령을 실행하기 전에 자리 표시자 값을 바꿉니다.

   ```bash
   azdata bdc storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > mount create 명령은 비동기입니다. 지금은 탑재의 성공 여부를 나타내는 메시지가 없습니다. 탑재 상태를 확인하려면 [상태](#status) 섹션을 참조하세요.

성공적으로 탑재된 경우 HDFS 데이터를 쿼리하고, 이 데이터에 대해 Spark 작업을 실행할 수 있어야 합니다. 빅 데이터 클러스터의 HDFS에서 `--mount-path`로 지정된 위치에 표시됩니다.

## <a id="status"></a> 탑재 상태 가져오기

빅 데이터 클러스터에 있는 모든 탑재 상태를 나열하려면 다음 명령을 사용합니다.

```bash
azdata bdc hdfs mount status
```

HDFS의 특정 경로에 있는 탑재 상태를 나열하려면 다음 명령을 사용합니다.

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>탑재 새로 고침

다음 예제에서는 탑재를 새로 고칩니다.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 탑재 삭제

탑재를 삭제하려면 **azdata bdc storage-pool mount delete** 명령을 사용하고 HDFS의 탑재 경로를 지정합니다.

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대한 자세한 내용은 [SQL Server 2019 빅 데이터 클러스터란?](big-data-cluster-overview.md)을 참조하세요.
