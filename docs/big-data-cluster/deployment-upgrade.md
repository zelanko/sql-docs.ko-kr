---
title: 새 릴리스로 업그레이드
titleSuffix: SQL Server big data clusters
description: 새 릴리스로 업그레이드 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (미리 보기) 하는 방법에 대해 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 867729b7d638960a2dbf2cb5f7544fecf698c94d
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652331"
---
# <a name="how-to-upgrade-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>업그레이드 하는 방법[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 SQL Server 빅 데이터 클러스터를 새 릴리스로 업그레이드하는 방법을 설명합니다. 이 문서의 단계는 특히 미리 보기 릴리스 간에 업그레이드하는 방법에 적용됩니다.

## <a name="backup-and-delete-the-old-cluster"></a>이전 클러스터 백업 및 삭제

현재, 빅 데이터 클러스터를 새 릴리스로 업그레이드하는 방법은 클러스터를 수동으로 제거하고 다시 만드는 것뿐입니다. 각 릴리스에는 이전 버전과 호환되지 않는 고유한 **azdata** 버전이 있습니다. 또한 이전 클러스터가 새 노드에 이미지를 다운로드해야 했다면 최신 이미지가 클러스터의 이전 이미지와 호환되지 않을 수도 있습니다. 최신 릴리스로 업그레이드하려면 다음 단계를 사용합니다.

1. 이전 클러스터를 삭제하기 전에 SQL Server 마스터 인스턴스와 HDFS의 데이터를 백업합니다. SQL Server 마스터 인스턴스의 경우 [SQL Server 백업 및 복원](data-ingestion-restore-database.md)을 사용할 수 있습니다. HDFS의 경우 [**curl**을 사용하여 데이터를 복사](data-ingestion-curl.md)할 수 있습니다.

1. `azdata delete cluster` 명령을 사용하여 이전 클러스터를 삭제합니다.

   ```bash
    azdata bdc delete --name <old-cluster-name>
   ```

   > [!Important]
   > 해당 클러스터와 일치하는 **azdata** 버전을 사용합니다. 최신 버전의 **azdata**를 사용하여 이전 클러스터를 삭제하면 안 됩니다.

1. CTP 3.2 이전에는 **azdata**를 **mssqlctl**이라고 불렀습니다. **mssqlctl** 또는 **azdata**의 이전 릴리스가 설치된 경우 먼저 제거한 다음, 최신 버전의 **azdata**를 설치해야 합니다.

   CTP 2.3 이상에서는 다음 명령을 실행합니다. 명령에서 `ctp3.1`을 제거할 **mssqlctl** 버전으로 바꿉니다. CTP 3.1 이전 버전의 경우 버전 번호 앞에 대시를 추가합니다(예: `ctp-2.5`).

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 최신 버전의 **azdata**를 설치합니다. 다음 명령은 CTP 3.2의 **azdata**를 설치합니다.

   **Windows:**

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

   **Linux:**

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!IMPORTANT]
   > 각 릴리스에서 **azdata**의 경로가 변경됩니다. 이전에 **azdata** 또는 **mssqlctl**을 설치했더라도 새 클러스터를 만들기 전에 최신 경로에서 다시 설치해야 합니다.

## <a id="azdataversion"></a> azdata 버전 확인

새로운 빅 데이터 클러스터를 배포하기 전에 `--version` 매개 변수를 통해 최신 버전의 **azdata**를 사용하고 있는지 확인합니다.

```bash
azdata --version
```

## <a name="install-the-new-release"></a>새 릴리스 설치

이전 빅 데이터 클러스터를 제거하고 최신 **azdata**를 설치한 후에는 현재 배포 지침을 사용하여 새로운 빅 데이터 클러스터를 배포합니다. 자세한 내용은 [Kubernetes에서 배포 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 하는 방법](deployment-guidance.md)을 참조 하세요. 그런 다음, 필요한 데이터베이스 또는 파일을 모두 복원합니다.

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터에 대 한 자세한 내용은 [항목 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ](big-data-cluster-overview.md)을 참조 하세요.
