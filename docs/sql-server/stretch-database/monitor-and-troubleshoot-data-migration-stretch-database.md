---
title: 데이터 마이그레이션 모니터링 및 문제 해결(Stretch Database) | Microsoft 문서
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, monitoring
- monitoring Stretch Database
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: aff3780352dbacd236e51f343999bd909d05207c
ms.sourcegitcommit: ec1f01b4bb54621de62ee488decf9511d651d700
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56240907"
---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>데이터 마이그레이션 모니터링 및 문제 해결(Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database 모니터에서 데이터 마이그레이션을 모니터링하려면 SQL Server Management Studio에서 데이터베이스에 대해 **태스크 | 스트레치 | 모니터** 를 선택합니다.  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>Stretch Database 모니터에서 데이터 마이그레이션 상태 확인  
 스트레치 데이터베이스 모니터를 열고 데이터 마이그레이션을 모니터링하려면 SQL Server Management Studio에서 데이터베이스에 대해 **태스크 | 스트레치 | 모니터** 를 선택합니다.  
  
-   모니터의 상단에는 스트레치 사용 SQL Server 데이터베이스 및 원격 Azure 데이터베이스 둘 다에 대한 일반 정보가 표시됩니다.  
  
-   모니터의 하단에는 데이터베이스의 각 스트레치 사용 테이블에 대한 데이터 마이그레이션 상태가 표시됩니다.  
  
 ![Stretch Database 모니터](../../sql-server/stretch-database/media/stretch-monitor.PNG "Stretch Database 모니터")  
  
##  <a name="Migration"></a> 동적 관리 뷰에서 데이터 마이그레이션 상태 확인  
 마이그레이션된 데이터의 배치 및 행 수를 보려면 동적 관리 뷰 **sys.dm_db_rda_migration_status** 를 엽니다. 자세한 내용은 [sys.dm_db_rda_migration_status&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)를 참조하세요.  
  
##  <a name="Firewall"></a> 데이터 마이그레이션 문제 해결  
 **스트레치 사용 테이블의 행이 Azure로 마이그레이션되지 않습니다. 어떤 문제 때문인가요?**  
 여러 가지 문제가 마이그레이션에 영향을 줄 수 있습니다. 다음 사항을 확인하세요.  
  
-   SQL Server 컴퓨터의 네트워크 연결을 확인합니다.  
  
-   Azure Firewall이 SQL Server의 원격 엔드포인트 연결을 차단하지 않는지 확인합니다.  
  
-   동적 관리 뷰 **sys.dm_db_rda_migration_status** 에서 최신 배치의 상태를 확인합니다. 오류가 발생한 경우 배치의 error_number, error_state 및 error_severity 값을 확인합니다.  
  
    -   뷰에 대한 자세한 내용은 [sys.dm_db_rda_migration_status&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md)를 참조하세요.  
  
    -   SQL Server 오류 메시지의 내용에 대한 자세한 내용은 [sys.messages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)를 참조하세요.  
  
 **Azure Firewall이 로컬 서버의 연결을 차단합니다.**  
 SQL Server가 원격 Azure 서버와 통신할 수 있도록 Azure 서버의 Azure Firewall 설정에 규칙을 추가해야 할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [스트레치 데이터베이스 관리 및 문제 해결](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  
