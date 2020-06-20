---
title: 변경 내용 추적 설정 및 해제(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], disabling
- data changes [SQL Server]
- change tracking [SQL Server], enabling
- tracking data changes [SQL Server]
- change tracking [SQL Server], configuring
- data [SQL Server], changing
ms.assetid: 1c92ec7e-ae53-4498-8bfd-c66a42a24d54
author: rothja
ms.author: jroth
ms.openlocfilehash: 402c63ae03df14e3a725fbc440575f5233d502f9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037330"
---
# <a name="enable-and-disable-change-tracking-sql-server"></a>변경 내용 추적 설정 및 해제(SQL Server)
  이 항목에서는 데이터베이스 및 테이블에 변경 내용 추적을 사용하도록 설정하거나 사용하지 않도록 설정하는 방법에 대해 설명합니다.  
  
## <a name="enable-change-tracking-for-a-database"></a>데이터베이스에 변경 내용 추적을 사용하도록 설정  
 변경 내용 추적을 사용하기 전에 데이터베이스 수준에서 변경 내용 추적을 설정해야 합니다. 다음 예에서는 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options)를 사용하여 변경 내용 추적을 사용하도록 설정하는 방법을 보여 줍니다.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
```  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 데이터베이스 속성&#40;변경 내용 추적 페이지&#41; [Database Properties &#40;ChangeTracking Page&#41;](../databases/database-properties-changetracking-page.md) 에 변경 내용을 설정할 수도 있습니다.  
  
 변경 내용 추적을 설정할 때 CHANGE_RETENTION 및 AUTO_CLEANUP 옵션을 지정할 수 있으며, 변경 내용 추적을 설정한 후 언제든지 이 값을 변경할 수 있습니다.  
  
 변경 내용 보존 기간 값은 변경 내용 추적 정보가 유지되는 기간을 지정합니다. 이 기간보다 오래된 변경 내용 추적 정보는 정기적으로 제거됩니다. 이 값을 설정할 때 애플리케이션이 이 데이터베이스에 있는 테이블을 동기화하는 빈도를 고려해야 합니다. 지정한 보존 기간은 최대 동기화 간격 이상이어야 합니다. 애플리케이션이 좀 더 긴 간격으로 변경 내용을 가져오면 일부 변경 내용 정보가 제거되지 않았을 수도 있으므로 반환되는 결과가 정확하지 않을 수 있습니다. 잘못된 결과가 생성되는 것을 방지하기 위해 애플리케이션에서는 CHANGE_TRACKING_MIN_VALID_VERSION 시스템 함수를 사용하여 동기화 간의 간격이 너무 긴지 여부를 확인할 수 있습니다.  
  
 AUTO_CLEANUP 옵션을 사용하여 오래된 변경 내용 추적 정보를 제거하는 정리 태스크를 설정하거나 해제할 수 있습니다. 이 설정은 애플리케이션이 동기화되지 않는 일시적인 문제가 발생하여 이 문제가 해결될 때까지 보존 기간보다 오래된 변경 내용 추적 정보를 제거하는 프로세스를 일시 중지해야 하는 경우에 유용합니다.  
  
 변경 내용 추적을 사용하는 데이터베이스의 경우 다음 사항에 주의하십시오.  
  
-   변경 내용 추적을 사용하려면 데이터베이스 호환성 수준이 90 이상으로 설정되어야 합니다. 데이터베이스 호환성 수준이 90 미만인 경우에도 변경 내용 추적을 구성할 수 있지만 변경 내용 추적 정보를 얻기 위해 사용되는 CHANGETABLE 함수에서 오류를 반환합니다.  
  
-   스냅샷 격리를 사용하는 것은 모든 변경 내용 추적 정보가 일관되도록 보장하는 가장 쉬운 방법입니다. 이러한 이유로 데이터베이스에 대해 스냅샷 격리를 ON으로 설정하는 것이 가장 좋습니다. 자세한 내용은 [변경 내용 추적 사용&#40;SQL Server&#41;](work-with-change-tracking-sql-server.md)을 참조하세요.  
  
## <a name="enable-change-tracking-for-a-table"></a>테이블에 변경 내용 추적을 사용하도록 설정  
 추적하려는 테이블마다 변경 내용 추적을 설정해야 합니다. 변경 내용 추적이 설정되면 DML 작업에 의해 영향을 받는 테이블의 모든 행에 대해 변경 내용 추적 정보가 유지 관리됩니다.  
  
 다음 예에서는 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)을 사용하여 테이블에 변경 내용 추적을 사용하도록 설정하는 방법을 보여 줍니다.  
  
```sql  
ALTER TABLE Person.Contact  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 데이터베이스 속성&#40;변경 내용 추적 페이지&#41; [Database Properties &#40;ChangeTracking Page&#41;](../databases/database-properties-changetracking-page.md) 에 변경 내용을 설정할 수도 있습니다.  
  
 TRACK_COLUMNS_UPDATED 옵션이 ON으로 설정되면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서는 내부 변경 내용 추적 테이블에 업데이트된 열에 대한 추가 정보를 저장합니다. 열 추적을 사용하면 애플리케이션이 업데이트된 열만 동기화하도록 설정할 수 있습니다. 이로 인해 효율성과 성능이 향상될 수 있습니다. 그러나 열 추적 정보 유지 관리로 인해 스토리지 오버헤드가 추가되기 때문에 이 옵션은 기본적으로 OFF로 설정됩니다.  
  
## <a name="disable-change-tracking-for-a-database-or-table"></a>데이터베이스 또는 테이블에 변경 내용 추적을 사용하지 않도록 설정  
 우선 변경 내용 추적이 설정된 모든 테이블에 대해 변경 내용 추적을 해제해야 해당 데이터베이스에 대한 변경 내용 추적을 OFF로 설정할 수 있습니다. 데이터베이스에서 변경 내용 추적이 설정된 테이블을 확인하려면 [sys.change_tracking_tables](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables) 카탈로그 뷰를 사용합니다.  
  
 데이터베이스의 테이블에 변경 내용 추적이 설정되어 있지 않으면 해당 데이터베이스에 대해 변경 내용 추적을 해제할 수 있습니다. 다음 예에서는 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options)를 사용하여 데이터베이스에 변경 내용 추적을 사용하지 않도록 설정하는 방법을 보여 줍니다.  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF  
```  
  
 다음 예에서는 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)을 사용하여 테이블에 변경 내용 추적을 사용하지 않도록 설정하는 방법을 보여 줍니다.  
  
```sql  
ALTER TABLE Person.Contact  
DISABLE CHANGE_TRACKING;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 속성&#40;변경 내용 추적 페이지&#41;](../databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [sys.change_tracking_databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases)   
 [sys.change_tracking_tables&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](track-data-changes-sql-server.md)   
 [변경 내용 추적 정보&#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md)   
 [변경 데이터 작업&#40;SQL Server&#41;](work-with-change-data-sql-server.md)   
 [변경 내용 추적 관리&#40;SQL Server&#41;](manage-change-tracking-sql-server.md)  
  
  
