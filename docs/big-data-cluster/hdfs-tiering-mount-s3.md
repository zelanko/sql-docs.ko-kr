---
title: HDFS 계층화를 위한 S3 탑재
titleSuffix: SQL Server big data clusters
description: 이 문서 (미리 보기)는 SQL Server 2019 빅 데이터 클러스터에서 HDFS에 외부 S3 파일 시스템 탑재에 계층화 하는 HDFS를 구성 하는 방법에 설명 합니다.
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f126620c4da759a4c56abad05bf2e989d7d1bc3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782065"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>빅 데이터 클러스터에 계층화 하는 HDFS에 대 한 탑재 S3 하는 방법

다음 섹션에서는 HDFS S3 저장소 데이터 원본을 사용 하 여 계층을 구성 하는 방법의 예제를 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [배포 된 빅 데이터 클러스터](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**
- 만들고 S3 버킷에 데이터 업로드 
  - CSV 업로드 하 여 S3 버킷에 파일 Parquet 또는 합니다. 이 빅 데이터 클러스터의 HDFS에 탑재 하는 외부 HDFS 데이터입니다.

## <a name="access-keys"></a>액세스 키

1. 빅 데이터 클러스터에 액세스할 수 있는 클라이언트 컴퓨터에서 명령 프롬프트를 엽니다.

1. 라는 로컬 파일을 만듭니다 **filename.creds** 다음 형식을 사용 하 여 S3 계정 자격 증명을 포함 하는:

   ```text
    fs.s3a.access.key=<Access Key ID of the key>
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > S3 액세스 키를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [S3 선택키가](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys)합니다.

## <a id="mount"></a> 원격 HDFS 저장소를 탑재 합니다.

액세스 키를 사용 하 여 자격 증명 파일을 준비, 했으므로 탑재를 시작할 수 있습니다. 다음 단계를 빅 데이터 클러스터의 로컬 HDFS 저장소에 S3에서 원격 HDFS storage를 탑재 합니다.

1. 사용 하 여 **kubectl** 끝점에 대 한 IP 주소를 찾으려면 **컨트롤러 svc 외부** 빅 데이터 클러스터의 서비스입니다. 검색할 합니다 **EXTERNAL-IP**합니다.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. 사용 하 여 로그인 **mssqlctl** 컨트롤러 끝점의 외부 IP 주소를 사용 하 여 클러스터 사용자 이름 및 암호를 사용 하 여:

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```

1. 사용 하 여 Azure에서 원격 HDFS storage를 탑재 **mssqlctl 클러스터 저장소 풀 마운트 만들기**합니다. 다음 명령을 실행 하기 전에 자리 표시자 값을 바꿉니다.

   ```bash
   mssqlctl cluster storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name> --credential-file <path-to-s3-credentials>/file.creds
   ```

   > [!NOTE]
   > 탑재 명령 만들기는 비동기적입니다. 이때 탑재 성공 여부를 나타내는 메시지가 없는 합니다. 참조를 [상태](#status) 섹션에 탑재의 상태를 확인 합니다.

성공적으로 탑재 하는 경우 HDFS 데이터를 쿼리하고 대해 Spark 작업을 실행할 수 있어야 합니다. 지정 된 위치에서 빅 데이터 클러스터의 HDFS에 나타나도록 `--mount-path`합니다.

## <a id="status"></a> 탑재의 상태를 가져옵니다.

빅 데이터 클러스터의 모든 탑재의 상태를 나열 하려면 다음 명령을 사용 합니다.

```bash
mssqlctl cluster storage-pool mount status
```

HDFS에서 특정 경로에 탑재의 상태를 나열 하려면 다음 명령을 사용 합니다.

```bash
mssqlctl cluster storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> 탑재를 삭제 합니다.

탑재를 삭제 하려면 사용 합니다 **mssqlctl 클러스터 저장소 풀 마운트 삭제** 명령을 실행 하 고 HDFS의 탑재 경로 지정:

```bash
mssqlctl cluster storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>다음 단계

SQL Server 2019 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.
