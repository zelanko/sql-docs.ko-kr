---
title: HDFS 계층화를 위한 S3 탑재
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 2019 빅 데이터 클러스터 (미리 보기)의 HDFS에 외부 S3 파일 시스템을 탑재 하도록 HDFS 계층화를 구성 하는 방법을 설명 합니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 28c80d6076f07c8a4f1605149f4b5c730c8349a1
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419343"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>빅 데이터 클러스터에서 HDFS 계층화를 위해 S3을 탑재 하는 방법

다음 섹션에서는 S3 저장소 데이터 원본을 사용 하 여 HDFS 계층화를 구성 하는 방법의 예를 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- S3 버킷에 데이터 만들기 및 업로드 
  - S3 버킷에 CSV 또는 Parquet 파일을 업로드 합니다. 빅 데이터 클러스터의 HDFS에 탑재 되는 외부 HDFS 데이터입니다.

## <a name="access-keys"></a>액세스 키

### <a name="set-environment-variable-for-access-key-credentials"></a>액세스 키 자격 증명에 대 한 환경 변수 설정

빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다. 다음 형식을 사용 하 여 환경 변수를 설정 합니다. 자격 증명은 쉼표로 구분 된 목록에 있어야 합니다. Windows에서 ' set ' 명령이 사용 됩니다. Linux를 사용 하는 경우 대신 ' export '를 사용 합니다.

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > S3 액세스 키를 만드는 방법에 대 한 자세한 내용은 [s3 액세스 키](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)를 참조 하세요.

## <a id="mount"></a>원격 HDFS 저장소 탑재

이제 액세스 키를 사용 하 여 자격 증명 파일을 준비 했으므로 탑재를 시작할 수 있습니다. 다음 단계는 S3의 원격 HDFS 저장소를 빅 데이터 클러스터의 로컬 HDFS 저장소에 탑재 합니다.

1. **Kubectl** 를 사용 하 여 빅 데이터 클러스터의 끝점 **컨트롤러 svc 외부** 서비스에 대 한 IP 주소를 찾습니다. **외부 IP**를 찾습니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 클러스터 사용자 이름 및 암호를 사용 하 여 컨트롤러 끝점의 외부 IP 주소를 사용 하 여 **azdata** 로 로그인 합니다.

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. 위의 지침에 따라 환경 변수 MOUNT_CREDENTIALS 설정

1. **Azdata bdc 저장소 풀 탑재 만들기**를 사용 하 여 Azure에서 원격 HDFS 저장소를 탑재 합니다. 다음 명령을 실행 하기 전에 자리 표시자 값을 바꿉니다.

   ```bash
   azdata bdc storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
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
