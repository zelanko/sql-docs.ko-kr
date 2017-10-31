---
title: DROP TRIGGER (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP TRIGGER
- DROP_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- renaming triggers
- triggers [SQL Server], removing
- DDL triggers, removing
- DROP TRIGGER statement
- deleting triggers
- dropping triggers
- removing triggers
- DML triggers, removing
ms.assetid: 092d0d71-9f1e-4e38-a1c4-2487adfa5b4e
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e3ca35b2b33a60d0af5dd31467f1381402f8f99b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-trigger-transact-sql"></a>DROP TRIGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 하나 이상의 DML 또는 DDL 트리거를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Trigger on an INSERT, UPDATE, or DELETE statement to a table or view (DML Trigger)  
  
DROP TRIGGER [ IF EXISTS ] [schema_name.]trigger_name [ ,...n ] [ ; ]  
  
-- Trigger on a CREATE, ALTER, DROP, GRANT, DENY, REVOKE or UPDATE statement (DDL Trigger)  
  
DROP TRIGGER [ IF EXISTS ] trigger_name [ ,...n ]   
ON { DATABASE | ALL SERVER }   
[ ; ]  
  
-- Trigger on a LOGON event (Logon Trigger)  
  
DROP TRIGGER [ IF EXISTS ] trigger_name [ ,...n ]   
ON ALL SERVER  
```  

  
## <a name="arguments"></a>인수  
 *경우에 존재*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 통해 [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).  
  
 조건에 따라 이미 있는 경우에 트리거를 삭제 합니다.  
  
 *schema_name*  
 DML 트리거가 속한 스키마의 이름입니다. DML 트리거는 트리거가 생성된 테이블 또는 뷰의 스키마로 한정됩니다. *schema_name* DDL 또는 logon 트리거에 대해서는 지정할 수 없습니다.  
  
 *trigger_name*  
 제거할 트리거의 이름입니다. 현재 생성된 된 트리거 목록을 보려면 [sys.server_assembly_modules](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) 또는 [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)합니다.  
  
 DATABASE  
 현재 데이터베이스에 적용된 DDL 트리거의 범위를 나타냅니다. 트리거를 만들거나 수정할 때 DATABASE를 지정한 경우 DATABASE를 지정해야 합니다.  
  
 ALL SERVER  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 현재 서버에 적용된 DDL 트리거의 범위를 나타냅니다. 트리거를 만들거나 수정할 때 ALL SERVER를 지정한 경우 ALL SERVER를 지정해야 합니다. ALL SERVER는 로그온 트리거에도 적용됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>주의  
 트리거 또는 트리거 테이블을 삭제하여 DML 트리거를 제거할 수 있습니다. 테이블을 삭제하면 이와 연결된 모든 트리거도 삭제됩니다.  
  
 트리거에 대 한 정보가에서 제거 되는 트리거를 삭제 하는 경우는 **sys.objects**, **sys.triggers** 및 **sys.sql_modules** 카탈로그 뷰.  
  
 같은 ON 절을 사용하여 만든 DDL 트리거에 대해서만 하나의 DROP TRIGGER 문으로 여러 개의 DDL 트리거를 삭제할 수 있습니다.  
  
 트리거의 이름을 바꾸려면 DROP TRIGGER와 CREATE TRIGGER를 사용합니다. 트리거의 정의를 변경하려면 ALTER TRIGGER를 사용합니다.  
  
 특정 트리거에 대 한 종속성을 확인 하는 방법에 대 한 자세한 내용은 참조 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md), [sys.dm_sql_referenced_entities&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md), 및 [sys.dm_sql_referencing_entities&#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md).  
  
 트리거의 텍스트 보기에 대 한 자세한 내용은 참조 [sp_helptext &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md) 및 [sys.sql_modules&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md).  
  
 기존 트리거의 목록 보기에 대 한 자세한 내용은 참조 [sys.triggers&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) 및 [sys.server_triggers&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 DML 트리거를 삭제하려면 트리거가 정의된 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
 서버 범위(ON ALL SERVER)로 정의된 DDL 트리거 또는 LOGON 트리거를 삭제하려면 현재 서버에서 CONTROL SERVER 권한이 필요합니다. 데이터베이스 범위(ON DATABASE)로 정의된 DDL 트리거를 삭제하려면 현재 데이터베이스에서 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-dml-trigger"></a>1. DML 트리거 삭제  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `employee_insupd` 트리거를 삭제합니다. (부터는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 트리거 IF EXISTS DROP 구문을 사용할 수 있습니다.)  
  
```  
IF OBJECT_ID ('employee_insupd', 'TR') IS NOT NULL  
   DROP TRIGGER employee_insupd;  
```  
  
### <a name="b-dropping-a-ddl-trigger"></a>2. DML 트리거 삭제  
 다음 예에서는 `safety` DDL 트리거를 삭제합니다.  
  
> [!IMPORTANT]  
>  DDL 트리거는 스키마 범위 아니며에 표시 되지 않습니다는 **sys.objects** 카탈로그 뷰의 OBJECT_ID 함수를 사용 하 여를 데이터베이스에 존재 하는지 여부를 쿼리할 수 없습니다. 스키마 범위가 아닌 개체는 해당 카탈로그 뷰를 사용하여 쿼리해야 합니다. DDL 트리거에 대 한 사용 하 여 **sys.triggers**합니다.  
  
```  
DROP TRIGGER safety  
ON DATABASE;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [ENABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [DML 트리거에 대한 정보 가져오기](../../relational-databases/triggers/get-information-about-dml-triggers.md)   
 [sp_help&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptrigger&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptrigger-transact-sql.md)   
 [sys.triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)   
 [sys.trigger_events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trigger-events-transact-sql.md)   
 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.server_triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)   
 [sys.server_trigger_events&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)   
 [sys.server_sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql.md)   
 [sys.server_assembly_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)  
  
  

