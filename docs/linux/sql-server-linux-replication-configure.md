---
title: Linux에서 SQL Server 복제 구성 | Microsoft Docs
description: 이 문서에서는 Linux의 SQL Server 복제를 구성 하는 방법을 설명 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7ab482a9c2a4bce9da7dc2b0a68cae6391759b92
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754455"
---
# <a name="configure-sql-server-replication-on-linux"></a>Linux에서 SQL Server 복제 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 에 대 한 SQL Server 복제에서는 Linux의 SQL Server의 인스턴스.

복제에 대 한 자세한 내용은 [SQL Server 복제 설명서](../relational-databases/replication/sql-server-replication.md)합니다.

SQL Server Management Studio (SSMS) 또는 TRANSACT-SQL 저장 프로시저를 사용 하 여 Linux에서 복제를 구성 합니다.

* SSMS를 사용 하려면이 문서의 지침을 따릅니다.

  SQL Server의 인스턴스에 연결 하려면 Windows 운영 체제에서 SSMS를 사용 합니다. 배경 지식 및 지침을 참조 하세요 [Linux의 SQL Server 관리를 사용 하 여 SSMS](./sql-server-linux-manage-ssms.md)합니다.
  
* 저장된 프로시저를 사용 하 여 예제를 수행 합니다 [Linux에서 SQL Server 구성 복제](sql-server-linux-replication-tutorial-tsql.md) 자습서입니다.

## <a name="prerequisites"></a>사전 요구 사항

게시자, 배포자 및 구독자를 구성 하기 전에 SQL Server 인스턴스에 대 한 몇 가지 구성 단계를 완료 해야 합니다.

1. 복제 에이전트를 사용 하도록 SQL Server 에이전트를 사용 하도록 설정 합니다. 모든 Linux 서버에서 터미널에서 다음 명령을 실행 합니다.

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. 복제에 대 한 SQL Server 인스턴스를 구성 합니다. 복제에 대 한 SQL Server 인스턴스를 구성 하려면 `sys.sp_MSrepl_createdatatypemappings` 복제에 참여 하는 모든 인스턴스에서 합니다.

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. 스냅숏 폴더를 만듭니다. SQL Server 에이전트는 스냅숏 폴더에 읽기/쓰기를 필요 합니다. 배포자에서 스냅숏 폴더를 만듭니다.

  스냅숏 폴더를 만들고 액세스 권한을 부여 하려면 `mssql` 사용자, 다음 명령을 실행 합니다.

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>구성 하 고 SQL Server Management Studio (SSMS) 사용 하 여 복제를 모니터링 합니다.

### <a name="configure-the-distributor"></a>배포자 구성
  
배포자를 구성 합니다. 

1. SSMS 개체 탐색기에서 SQL Server 인스턴스에 연결 합니다.

1. 마우스 오른쪽 단추로 클릭 **복제**를 클릭 하 고 **배포 구성 하는 중...** .

1. 지침에 따라 합니다 **배포 구성 마법사**합니다.

### <a name="create-publication-and-articles"></a>게시 및 아티클 만들기

게시 및 문서를 만들려면:

1. 개체 탐색기에서 클릭 **복제** > **로컬 게시**> **새 게시 하는 중...** .

1. 지침 따라 합니다 **새 게시 마법사** 복제 및 게시에 속한 아티클에의 유형을 구성 합니다.

### <a name="configure-the-subscription"></a>구독 구성

개체 탐색기에서 구독을 구성 하려면 클릭 **복제** > **로컬 구독**> **새 구독...** .

### <a name="monitor-replication-jobs"></a>복제 작업 모니터링

복제 모니터를 사용 하 여 복제 작업을 모니터링 합니다.

개체 탐색기에서 마우스 오른쪽 단추로 클릭 **복제**, 클릭 **복제 모니터 시작**합니다.

## <a name="next-steps"></a>다음 단계

[개념: Linux에서 SQL Server 복제](sql-server-linux-replication.md)

[복제 저장 프로시저](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)합니다.
