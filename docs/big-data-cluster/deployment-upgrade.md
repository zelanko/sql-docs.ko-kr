---
title: 새 릴리스로 업그레이드
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 새 릴리스로 업그레이드 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7bdb1eb59fd36d065df9dba0f6d6879c1a294914
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419388"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>빅 데이터 클러스터 SQL Server 업그레이드 하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터를 새 릴리스로 업그레이드 하는 방법에 대 한 지침을 제공 합니다. 이 문서의 단계는 미리 보기 릴리스 간에 업그레이드 하는 방법에 특히 적용 됩니다.

## <a name="backup-and-delete-the-old-cluster"></a>이전 클러스터 백업 및 삭제

현재 빅 데이터 클러스터를 새 릴리스로 업그레이드 하는 유일한 방법은 클러스터를 수동으로 제거 하 고 다시 만드는 것입니다. 각 릴리스에는 이전 버전과 호환 되지 않는 고유한 **azdata** 버전이 있습니다. 또한 이전 클러스터가 새 노드에서 이미지를 다운로드 해야 하는 경우 최신 이미지가 클러스터의 이전 이미지와 호환 되지 않을 수 있습니다. 최신 릴리스로 업그레이드 하려면 다음 단계를 사용 합니다.

1. 이전 클러스터를 삭제 하기 전에 SQL Server 마스터 인스턴스와 HDFS의 데이터를 백업 합니다. SQL Server 마스터 인스턴스의 경우 [백업 및 복원을 SQL Server](data-ingestion-restore-database.md)사용할 수 있습니다. HDFS의 경우, [데이터를 **말아 넘기기**로 복사할 수](data-ingestion-curl.md)있습니다.

1. `azdata delete cluster` 명령을 사용 하 여 이전 클러스터를 삭제 합니다.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 클러스터와 일치 하는 **azdata** 버전을 사용 합니다. 최신 버전의 **azdata**를 사용 하 여 이전 클러스터를 삭제 하지 마세요.

1. CTP 3.2 이전에 **azdata** 는 **mssqlctl**를 호출 했습니다. **Mssqlctl** 또는 **azdata** 의 이전 릴리스가 설치 된 경우 최신 버전의 **azdata**를 설치 하기 전에 먼저를 제거 하는 것이 중요 합니다.

   CTP 2.3 이상에서는 다음 명령을 실행 합니다. 명령 `ctp3.1` 에서를 제거할 **mssqlctl** 버전으로 바꿉니다. 버전이 CTP 3.1 이전 버전인 경우 버전 번호 앞에 대시를 추가 합니다 (예: `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://mcr.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 최신 버전의 **azdata**를 설치 합니다. 다음 명령은 CTP 3.2에 대 한 **azdata** 를 설치 합니다.

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **용**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 각 릴리스에 대해 **azdata** 의 경로가 변경 됩니다. 이전에 **azdata** 또는 **mssqlctl**를 설치한 경우에도 새 클러스터를 만들기 전에 최신 경로에서 다시 설치 해야 합니다.

## <a id="azdataversion"></a>Azdata 버전 확인

새 빅 데이터 클러스터를 배포 하기 전에 `--version` 매개 변수와 함께 최신 버전의 **azdata** 를 사용 하 고 있는지 확인 합니다.

```bash
azdata --version
```

## <a name="install-the-new-release"></a>새 릴리스를 설치 합니다.

이전 빅 데이터 클러스터를 제거 하 고 최신 **azdata**를 설치한 후에는 현재 배포 지침을 사용 하 여 새로운 빅 데이터 클러스터를 배포 합니다. 자세한 내용은 [Kubernetes에서 빅 데이터 클러스터 SQL Server 배포 하는 방법](deployment-guidance.md)을 참조 하세요. 그런 다음 필요한 모든 데이터베이스 또는 파일을 복원 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [SQL Server 빅 데이터 클러스터 란?](big-data-cluster-overview.md)을 참조 하세요.
