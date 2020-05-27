---
title: DROP TRIGGER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 810367b817aec0688a2bc5168be10c7ff073affc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73980992"
---
# <a name="drop-trigger-transact-sql"></a>DROP TRIGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 데이터베이스에서 하나 이상의 DML 또는 DDL 트리거를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658), [!INCLUDE[sssds](../../includes/sssds-md.md)]).  
  
 이미 있는 경우에만 트리거를 조건부로 삭제합니다.  
  
 *schema_name*  
 DML 트리거가 속한 스키마의 이름입니다. DML 트리거는 트리거가 생성된 테이블 또는 뷰의 스키마로 한정됩니다. *schema_name*은 DDL 또는 LOGON 트리거에 대해 지정될 수 없습니다.  
  
 *trigger_name*  
 제거할 트리거의 이름입니다. 현재 생성된 트리거 목록을 보려면 [sys.server_assembly_modules](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) 또는 [sys.server_triggers](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)를 사용하세요.  
  
 DATABASE  
 현재 데이터베이스에 적용된 DDL 트리거의 범위를 나타냅니다. 트리거를 만들거나 수정할 때 DATABASE를 지정한 경우 DATABASE를 지정해야 합니다.  
  
 ALL SERVER  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
 현재 서버에 적용된 DDL 트리거의 범위를 나타냅니다. 트리거를 만들거나 수정할 때 ALL SERVER를 지정한 경우 ALL SERVER를 지정해야 합니다. ALL SERVER는 로그온 트리거에도 적용됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>설명  
 트리거 또는 트리거 테이블을 삭제하여 DML 트리거를 제거할 수 있습니다. 테이블을 삭제하면 이와 연결된 모든 트리거도 삭제됩니다.  
  
 트리거를 삭제하면 **sys.objects**, **sys.triggers** 및 **sys.sql_modules** 카탈로그 뷰에서 트리거 정보가 제거됩니다.  
  
 같은 ON 절을 사용하여 만든 DDL 트리거에 대해서만 하나의 DROP TRIGGER 문으로 여러 개의 DDL 트리거를 삭제할 수 있습니다.  
  
 트리거의 이름을 바꾸려면 DROP TRIGGER와 CREATE TRIGGER를 사용합니다. 트리거의 정의를 변경하려면 ALTER TRIGGER를 사용합니다.  
  
 특정 트리거에 대한 종속성을 결정하는 방법에 대 한 자세한 내용은 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md), [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) 및 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)을 참조하세요.  
  
 트리거의 텍스트 보기에 대한 자세한 내용은 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md) 및 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)을 참조하세요.  
  
 기존 트리거의 목록 보기에 대한 자세한 내용은 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) 및 [sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)을 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 DML 트리거를 삭제하려면 트리거가 정의된 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
 서버 범위(ON ALL SERVER)로 정의된 DDL 트리거 또는 LOGON 트리거를 삭제하려면 현재 서버에서 CONTROL SERVER 권한이 필요합니다. 데이터베이스 범위(ON DATABASE)로 정의된 DDL 트리거를 삭제하려면 현재 데이터베이스에서 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-dml-trigger"></a>A. DML 트리거 삭제  
 다음 예에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스에서 `employee_insupd` 트리거를 삭제합니다. ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터는 DROP TRIGGER IF EXISTS 구문을 사용할 수 있습니다.)  
  
```  
IF OBJECT_ID ('employee_insupd', 'TR') IS NOT NULL  
   DROP TRIGGER employee_insupd;  
```  
  
### <a name="b-dropping-a-ddl-trigger"></a>B. DML 트리거 삭제  
 다음 예에서는 `safety` DDL 트리거를 삭제합니다.  
  
> [!IMPORTANT]  
>  DDL 트리거는 스키마 범위가 아니고 따라서 **sys.objects** 카탈로그 뷰에 표시되지 않기 때문에 OBJECT_ID 함수를 사용하여 데이터베이스에 DDL 트리거가 있는지 여부를 쿼리할 수 없습니다. 스키마 범위가 아닌 개체는 해당 카탈로그 뷰를 사용하여 쿼리해야 합니다. DDL 트리거의 경우 **sys.triggers**를 사용합니다.  
  
```  
DROP TRIGGER safety  
ON DATABASE;  
```  
  
## <a name="see-also"></a>참고 항목  
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
  
  
