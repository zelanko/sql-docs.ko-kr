---
title: 스트레치 지원 데이터베이스 Backup
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: 18f0dff0-d8ce-4bee-a935-76ed6dfb3208
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 897f748c5aeab43c7e3ef98f6dbfff84b9da69d7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286307"
---
# <a name="backup-stretch-enabled-databases-stretch-database"></a>스트레치 사용 데이터베이스 백업(Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


 데이터베이스 백업은 다양한 유형의 실패, 오류 및 재해로부터 복구하는 데 도움이 됩니다.  
  
 -   스트레치 사용 SQL Server 데이터베이스를 백업해야 합니다.  
      
 -   Microsoft Azure는 Stretch Database가 SQL Server에서 Azure로 마이그레이션한 원격 데이터를 자동으로 백업합니다.  

> [!TIP]
> Backup은 전체 고가용성 및 비즈니스 연속성 솔루션의 한 부분입니다. 고가용성에 대한 자세한 내용은 [고가용성 솔루션](../../database-engine/sql-server-business-continuity-dr.md)을 참조하세요.
   
## <a name="back-up-your-sql-server-data"></a>SQL Server 데이터 백업  
  
스트레치 사용 SQL Server 데이터베이스를 백업하기 위해 현재 사용하는 SQL Server 백업 방법을 계속 사용할 수 있습니다. 자세한 내용은 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)을 참조하세요.
  
 스트레치 지원 SQL Server 데이터베이스의 Backup에는 로컬 데이터와 백업이 실행된 시점에 마이그레이션에 적합한 데이터만 포함됩니다. 적격한 데이터는 아직 마이그레이션되지 않았지만 테이블의 마이그레이션 설정에 따라 Azure로 마이그레이션될 예정인 데이터입니다. 이를 **단순 복사** 백업이라고 하며 이미 Azure로 마이그레이션된 데이터는 포함되지 않습니다.  
  
## <a name="back-up-your-remote-azure-data"></a>원격 Azure 데이터 백업   
  
Microsoft Azure는 Stretch Database가 SQL Server에서 Azure로 마이그레이션한 원격 데이터를 자동으로 백업합니다.    
### <a name="azure-reduces-the-risk-of-data-loss-with-automatic-backup"></a>Azure에서 자동 백업을 사용하여 데이터 손실 위험을 줄임  
Azure의 SQL Server Stretch Database 서비스는 적어도 8시간마다 자동 스토리지 스냅샷을 사용하여 원격 데이터베이스를 보호합니다. 가능한 한 광범위한 복원 지점을 제공하기 위해 각 스냅샷은 7일 동안 유지됩니다.  
  
### <a name="azure-reduces-the-risk-of-data-loss-with-geo-redundancy"></a>Azure에서 지리적 중복을 사용하여 데이터 손실 위험을 줄임  
Azure 데이터베이스 백업은 Azure 지역 중복 스토리지(RA-GRS)에 저장되므로 기본적으로 지역 중복입니다. 지역 중복 스토리지는 기본 지역에서 수백 마일 떨어져 있는 보조 영역에 데이터를 복제합니다. 주 지역과 보조 지역 둘 다에서 데이터가 별도의 오류 도메인 및 업그레이드 도메인에 각각 세 번씩 복제됩니다. 이렇게 하면 전체 지역 가동 중단 또는 Azure 지역 중 하나를 사용할 수 없는 재해가 발생하더라도 데이터가 지속됩니다.

### <a name="stretch-database-reduces-the-risk-of-data-loss-for-your-azure-data-by-retaining-migrated-rows-temporarily"></a><a name="stretchRPO"></a>Stretch Database는 마이그레이션된 행을 일시적으로 유지하여 Azure 데이터의 데이터 손실 위험을 줄여줍니다.
Stretch Database는 SQL Server의 적격 행을 Azure로 마이그레이션한 후 해당 행을 8시간 이상 스테이징 테이블에 유지합니다. Azure 데이터베이스의 백업을 복원하면 Stretch Database는 스테이징 테이블에 저장된 행을 사용하여 SQL Server 및 Azure 데이터베이스를 조정합니다.

Azure 데이터 백업을 복원한 후 저장 프로시저 [sys.sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 를 실행하여 스트레치 사용 SQL Server 데이터베이스를 원격 Azure 데이터베이스에 다시 연결해야 합니다. **sys.sp_rda_reauthorize_db**를 실행하면 스트레치 데이터베이스가 SQL Server와 Azure 데이터베이스를 자동으로 조정합니다.

스트레치 데이터베이스가 준비 테이블에 일시적으로 유지하는 마이그레이션된 데이터의 시간 수를 늘리려면 저장 프로시저 [sys.sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) 을 실행하고 8보다 큰 시간 수를 지정합니다. 유지할 데이터 양을 결정하려면 다음 요소를 고려합니다.
-   Azure 자동 백업 빈도(최소 8시간마다)
-   문제 발생 후 문제를 인식하고 백업 복원을 결정하는 데 필요한 시간
-   Azure 복원 작업 기간

> [!NOTE]
> Stretch Database가 스테이징 테이블에 일시적으로 유지하는 데이터의 양을 늘리면 SQL Server에 필요한 공간의 크기도 커집니다.

스트레치 데이터베이스가 현재 준비 테이블에 일시적으로 유지하는 데이터의 시간 수를 확인하려면 저장 프로시저 [sys.sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)을 실행합니다.

## <a name="see-also"></a>참고 항목  
[스트레치 사용 데이터베이스 복원](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
 [Stretch Database 관리 및 문제 해결](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)   
   
  
  
