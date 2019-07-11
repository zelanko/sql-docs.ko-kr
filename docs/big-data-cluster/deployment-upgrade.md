---
title: 새 릴리스로 업그레이드
titleSuffix: SQL Server big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)를 새 릴리스로 업그레이드 하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8c8b8df4dc5643febdf3ddc808f215a9c34d24fe
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728771"
---
# <a name="how-to-upgrade-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터를 업그레이드 하는 방법

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터를 새 릴리스로 업그레이드 하는 방법에 지침을 제공 합니다. 이 문서의 단계는 특히 미리 보기 버전 간에 업그레이드 하는 방법에 적용 합니다.

## <a name="backup-and-delete-the-old-cluster"></a>백업 하 고 이전 클러스터를 삭제 합니다.

현재 빅 데이터 클러스터를 새 릴리스로 업그레이드 하는 유일한 방법은 수동으로 제거 하 고 클러스터를 다시 만듭니다. 에 고유한 버전의 각 릴리스에 **mssqlctl** 는 이전 버전과 호환 되지 않습니다. 또한 새 노드에서 이미지를 다운로드 하는 이전 클러스터 있으면 최신 이미지 클러스터에서 이전 이미지와 호환 되지 않을 수 있습니다. 최신 버전으로 업그레이드 하려면 다음 단계를 사용 합니다.

1. 이전 클러스터를 삭제 하기 전에 SQL Server 마스터 인스턴스 및 HDFS에서 데이터를 백업 합니다. SQL Server 마스터 인스턴스를 사용할 수 있습니다 [SQL Server 백업 및 복원](data-ingestion-restore-database.md)합니다. HDFS에 대 한 있습니다 [사용 하 여 데이터를 복사할 수 **curl**](data-ingestion-curl.md)합니다.

1. 사용 하 여 이전 클러스터를 삭제 합니다 `mssqlctl delete cluster` 명령입니다.

   ```bash
    mssqlctl bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 버전을 사용 하 여 **mssqlctl** 일치 하는 클러스터입니다. 최신 버전을 사용 하 여 이전 클러스터를 삭제 하지 마세요 **mssqlctl**합니다.

1. 모든 이전 버전의 경우 **mssqlctl** 설치를 반드시 제거할 **mssqlctl** 최신 버전을 설치 하기 전에 첫 번째입니다.

   CTP 2.3 이상에서 다음 명령을 실행 합니다. 바꿉니다 `ctp3.0` 버전의 명령에 **mssqlctl** 제거 됩니다. CTP 3.0 이전 버전 인 경우 버전 번호 앞에 대시를 추가 (예를 들어 `ctp-2.5`).

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. 최신 버전의 설치 **mssqlctl**합니다. 다음 명령을 설치할 **mssqlctl** CTP 3.1의 경우:

   **Windows:**

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

   **Linux:**

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt --user
   ```

   > [!IMPORTANT]
   > 각 릴리스에 대 한 경로 대 한 **mssqlctl** 변경 합니다. 이전에 설치한 경우에 **mssqlctl**, 최신 경로에서 새 클러스터를 만들기 전에 다시 설치 해야 합니다.

## <a id="mssqlctlversion"></a> Mssqlctl 버전 확인

새 빅 데이터 클러스터를 배포 하기 전에 최신 버전의를 사용 하 고 있는지를 확인 **mssqlctl** 사용 하 여는 `--version` 매개 변수:

```bash
mssqlctl --version
```

## <a name="install-the-new-release"></a>새 릴리스를 설치 합니다.

이전 빅 데이터 클러스터를 제거 하 고 최신을 설치한 후 **mssqlctl**, 현재 배포 지침을 사용 하 여 새 빅 데이터 클러스터를 배포 합니다. 자세한 내용은 [빅 데이터를 SQL Server를 배포 하는 방법에서 kubernetes 클러스터](deployment-guidance.md)합니다. 그런 다음 모든 필요한 데이터베이스 또는 파일을 복원 합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 참조 하십시오 [SQL Server 빅 데이터 클러스터 이란](big-data-cluster-overview.md)합니다.
