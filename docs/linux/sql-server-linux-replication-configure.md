---
title: 복제 구성(SSMS)
description: 이 문서에서는 Linux에서 SQL Server 복제를 구성하는 방법을 설명합니다.
ms.custom: seo-dt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
titleSuffix: SQL Server on Linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4f367f7d6c41600ddb26d12b28ae14d0fc1cdffc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882691"
---
# <a name="configure-sql-server-replication-on-linux"></a>Linux의 SQL Server 복제 구성

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]에서는 LSQL Server on Linux 인스턴스에 SQL Server 복제를 도입했습니다.

복제에 대한 자세한 내용은 [SQL Server 복제 설명서](../relational-databases/replication/sql-server-replication.md)를 참조하세요.

SSMS(SQL Server Management Studio) 또는 Transact-SQL 저장 프로시저를 사용하여 Linux에서 복제를 구성합니다.

* SSMS를 사용하려면 이 문서의 지침을 따르세요.

  Windows 운영 체제에서 SSMS를 사용하여 SQL Server 인스턴스에 연결합니다. 배경 및 지침은 [SSMS를 사용하여 Linux의 SQL Server 관리](./sql-server-linux-manage-ssms.md)를 참조하세요.
  
* 저장 프로시저에 대한 예제를 보려면 [Linux의 SQL Server 복제 구성](sql-server-linux-replication-tutorial-tsql.md) 자습서를 따르세요.

## <a name="prerequisites"></a>사전 요구 사항

게시자, 배포자 및 구독자를 구성하기 전에 SQL Server 인스턴스에 대해 몇 가지 구성 단계를 완료해야 합니다.

1. SQL Server 에이전트를 사용하도록 설정하여 복제 에이전트를 사용합니다. 모든 Linux 서버의 터미널에서 다음 명령을 실행합니다.

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. 복제를 위해 SQL Server 인스턴스를 구성합니다. 복제를 위해 SQL Server 인스턴스를 구성하려면 복제에 참여하는 모든 인스턴스에 대해 `sys.sp_MSrepl_createdatatypemappings`를 실행합니다.

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. 스냅샷 폴더를 만듭니다. SQL Server 에이전트는 읽기/쓰기를 수행할 스냅샷 폴더가 필요합니다. 배포자에 스냅샷 폴더를 만듭니다.

  스냅샷 폴더를 만들고 사용자에게 `mssql` 액세스 권한을 부여하려면 다음 명령을 실행합니다.

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)를 사용하여 복제 구성 및 모니터링

### <a name="configure-the-distributor"></a>배포자 구성
  
배포자를 구성하려면 

1. SSMS의 개체 탐색기에서 SQL Server의 인스턴스에 연결합니다.

1. **복제**를 마우스 오른쪽 단추로 클릭하고 **배포 구성...** 을 클릭합니다.

1. **배포 구성 마법사**의 지침을 따릅니다.

### <a name="create-publication-and-articles"></a>게시 및 아티클 만들기

게시 및 아티클을 만들려면

1. 개체 탐색기에서 **복제** > **로컬 게시**> **새 게시...** 를 클릭합니다.

1. **새 게시 마법사**의 지침에 따라 복제 유형 및 게시에 속하는 아티클을 구성합니다.

### <a name="configure-the-subscription"></a>구독 구성

개체 탐색기에서 구독을 구성하려면 **복제** > **로컬 구독**> **새 구독...** 을 클릭합니다.

### <a name="monitor-replication-jobs"></a>복제 작업 모니터링

복제 모니터를 사용하여 복제 작업을 모니터링합니다.

개체 탐색기에서 **복제**를 마우스 오른쪽 단추로 클릭하고 **복제 모니터 시작**을 클릭합니다.

## <a name="next-steps"></a>다음 단계

[개념: Linux의 SQL Server 복제](sql-server-linux-replication.md)

[복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)
