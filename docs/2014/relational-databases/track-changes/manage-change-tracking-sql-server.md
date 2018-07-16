---
title: 변경 내용 추적 관리(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tracking data changes [SQL Server]
- change tracking [SQL Server], overhead
- change tracking [SQL Server]
- change tracking [SQL Server], managing
ms.assetid: 94a8d361-e897-4d6d-9a8f-1bb652e7a850
caps.latest.revision: 8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dba3c283bb5215bb573fa90caf6f8e9cff74ca63
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232983"
---
# <a name="manage-change-tracking-sql-server"></a>변경 내용 추적 관리(SQL Server)
  이 항목에서는 변경 내용 추적을 관리하는 방법에 대해 설명합니다. 또한 보안을 구성하는 방법과 변경 내용 추적을 사용할 때 저장소 및 성능에 미치는 영향을 확인하는 방법에 대해서도 설명합니다.  
  
## <a name="managing-change-tracking"></a>변경 내용 추적 관리  
 다음 섹션에서는 변경 내용 추적 관리와 관련된 카탈로그 뷰, 사용 권한 및 설정에 대해 설명합니다.  
  
### <a name="catalog-views"></a>카탈로그 뷰  
 다음 카탈로그 뷰를 사용하여 변경 내용 추적이 설정된 테이블 및 데이터베이스를 확인할 수 있습니다.  
  
-   [sys.change_tracking_databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases)  
  
-   [sys.change_tracking_tables&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables)  
  
 [sys.internal_tables](/sql/relational-databases/system-catalog-views/sys-internal-tables-transact-sql) 카탈로그 뷰는 사용자 테이블에 대한 변경 내용 추적을 설정할 때 만든 내부 테이블도 나열합니다.  
  
### <a name="security"></a>보안  
 [변경 내용 추적 함수](/sql/relational-databases/system-functions/change-tracking-functions-transact-sql)를 사용하여 변경 내용 추적 정보에 액세스하려면 보안 주체에 다음 사용 권한이 있어야 합니다.  
  
-   변경 내용 추적이 설정된 쿼리하는 테이블에 있는 한 개 이상의 기본 키 열에 대한 SELECT 권한  
  
-   변경 내용을 가져오는 테이블에 대한 VIEW CHANGE TRACKING 권한. VIEW CHANGE TRACKING 권한이 필요한 이유는 다음과 같습니다.  
  
    -   변경 내용 추적 레코드에는 삭제된 행, 특히 삭제된 행의 기본 키 값에 대한 정보가 포함됩니다. 일부 중요한 데이터를 삭제한 후에 보안 주체에게 변경 내용 추적이 설정된 테이블에 대한 SELECT 권한이 부여되었을 수 있습니다. 이러한 경우 해당 보안 주체가 변경 내용 추적을 사용하여 삭제된 정보에 액세스하지 못하도록 해야 합니다.  
  
    -   변경 내용 추적 정보는 업데이트 작업으로 변경된 열에 대한 정보를 저장할 수 있습니다. 보안 주체는 중요한 정보가 포함된 열에 대한 권한이 거부될 수 있습니다. 변경 내용 추적 정보를 사용할 수 있으므로 보안 주체는 열 값이 업데이트되었는지를 확인할 수 있지만 해당 열의 값은 확인할 수 없습니다.  
  
## <a name="understanding-change-tracking-overhead"></a>변경 내용 추적 오버헤드 이해  
 테이블에 변경 내용 추적이 설정되면 일부 관리 작업에 영향을 줄 수 있습니다. 다음 표에서는 작업 및 고려해야 하는 영향에 대해 설명합니다.  
  
|연산|변경 내용 추적이 설정된 경우|  
|---------------|-------------------------------------|  
|DROP TABLE|삭제된 테이블에 대한 모든 변경 내용 추적 정보가 제거됩니다.|  
|ALTER TABLE DROP CONSTRAINT|PRIMARY KEY 제약 조건을 삭제하려는 시도가 실패합니다. 변경 내용 추적을 해제해야 PRIMARY KEY 제약 조건을 삭제할 수 있습니다.|  
|ALTER TABLE DROP COLUMN|삭제된 열이 기본 키의 일부일 경우 변경 내용 추적과 관계없이 해당 열을 삭제할 수 없습니다.<br /><br /> 삭제된 열이 기본 키의 일부가 아닐 경우 해당 열을 삭제할 수 있습니다. 그러나 이 데이터를 동기화하는 응용 프로그램에 미치는 영향에 대해 먼저 이해해야 합니다. 테이블에 열 변경 내용 추적이 설정되어 있을 경우 삭제된 열이 여전히 변경 내용 추적 정보의 일부로 반환될 수도 있습니다. 삭제된 열은 응용 프로그램에서 처리해야 합니다.|  
|ALTER TABLE ADD COLUMN|변경 내용 추적이 설정된 테이블에 새 열이 추가될 경우 이 열 추가 작업은 추적되지 않습니다. 새 열에 대해 수행된 업데이트 및 변경 내용만 추적됩니다.|  
|ALTER TABLE ALTER COLUMN|기본 키가 아닌 열의 데이터 형식 변경 내용은 추적되지 않습니다.|  
|ALTER TABLE SWITCH|테이블 중 하나 또는 둘 모두에 변경 내용 추적이 설정된 경우 파티션 전환에 실패합니다.|  
|DROP INDEX 또는 ALTER INDEX DISABLE|기본 키를 강제 적용하는 인덱스는 삭제 또는 해제할 수 없습니다.|  
|TRUNCATE TABLE|테이블 잘라내기는 변경 내용 추적이 설정된 테이블에서 수행할 수 있습니다. 그러나 이 작업으로 삭제된 행은 추적되지 않으며 유효한 최소 버전이 업데이트됩니다. 응용 프로그램이 버전을 검사할 때 해당 버전이 너무 오래되어 다시 초기화해야 한다고 나타납니다. 이는 해당 테이블의 변경 내용 추적이 해제된 다음 다시 설정되는 것과 동일합니다.|  
  
 변경 내용 추적을 사용하더라도 변경 내용 추적 정보가 작업의 일부로 저장되므로 DML 작업에는 오버헤드가 추가되지 않습니다.  
  
### <a name="effects-on-dml"></a>DML에 미치는 영향  
 변경 내용 추적은 DML 작업에 대한 성능 오버헤드를 최소화하도록 최적화되었습니다. 테이블에 변경 내용 추적을 사용하는 것과 연관된 증분 성능 오버헤드는 테이블에 대해 인덱스가 생성되어 유지 관리가 필요해질 때 발생하는 오버헤드와 비슷합니다.  
  
 DML 작업으로 변경된 각 행의 경우 내부 변경 내용 추적 테이블에 한 개의 행이 추가됩니다. DML 작업과 관련한 이런 영향은 다음과 같은 다양한 요소에 따라 달라집니다.  
  
-   기본 키 열의 수  
  
-   사용자 테이블 행에서 변경되는 데이터의 양  
  
-   트랜잭션에서 수행되는 작업의 수  
  
 스냅숏 격리를 사용하는 경우에도 변경 내용 추적의 설정 여부와 관계없이 모든 DML 작업에 대한 성능에 영향을 미칩니다.  
  
### <a name="effects-on-storage"></a>저장소에 미치는 영향  
 변경 내용 추적 데이터는 다음과 같은 유형의 내부 테이블에 저장됩니다.  
  
-   내부 변경 테이블  
  
     변경 내용 추적을 설정한 각 사용자 테이블에 대해 하나의 내부 변경 테이블이 있습니다.  
  
-   내부 트랜잭션 테이블  
  
     데이터베이스에 대해 하나의 내부 트랜잭션 테이블이 있습니다.  
  
 이러한 내부 테이블은 다음과 같은 방법으로 저장소 요구 사항에 영향을 미칩니다.  
  
-   사용자 테이블에 있는 각 행에 대한 개별 변경 내용의 경우 내부 변경 내용 테이블에 한 행이 추가됩니다. 이 행에는 작은 고정 오버헤드와 기본 키 열의 크기와 같은 가변 오버헤드가 있습니다. 이 행은 응용 프로그램이 설정한 선택적 컨텍스트 정보를 포함할 수 있습니다. 그리고 열 추적이 설정된 경우 변경된 각 열은 추적 테이블에 4바이트가 필요합니다.  
  
-   커밋된 각 트랜잭션에 대해 하나의 행이 내부 트랜잭션 테이블에 추가됩니다.  
  
 다른 내부 테이블을 사용할 때와 같이 [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) 저장 프로시저를 사용하여 변경 내용 추적 테이블에 사용되는 공간을 결정할 수 있습니다. 내부 테이블의 이름은 다음 예와 같이 [sys.internal_tables](/sql/relational-databases/system-catalog-views/sys-internal-tables-transact-sql) 카탈로그 뷰를 사용하여 가져올 수 있습니다.  
  
```tsql  
sp_spaceused 'sys.change_tracking_309576141'  
sp_spaceused 'sys.syscommittab'  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터 변경 내용 추적&#40;SQL Server&#41;](track-data-changes-sql-server.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [데이터베이스 속성&#40;변경 내용 추적 페이지&#41;](../databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [sys.change_tracking_databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases)   
 [sys.change_tracking_tables&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](track-data-changes-sql-server.md)   
 [변경 내용 추적 정보&#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md)   
 [변경 데이터 작업&#40;SQL Server&#41;](work-with-change-data-sql-server.md)  
  
  
