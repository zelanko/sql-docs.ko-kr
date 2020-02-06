---
title: ENABLE TRIGGER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENABLE TRIGGER
- ENABLE_TSQL
- ENABLE_TRIGGER_TSQL
- ENABLE
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, enabling
- triggers [SQL Server], enabling
- DML triggers, enabling
- ENABLE TRIGGER statement
ms.assetid: 6e21f0ad-68d0-432f-9c7c-a119dd2d3fc9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 369dd7ec16ee530d7612222ad7e77dd6faf66e14
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73980941"
---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

DML, DDL 또는 LOGON 트리거를 활성화합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>인수  
*schema_name*  
트리거가 속한 스키마의 이름입니다. *schema_name*은 DDL 또는 LOGON 트리거에 대해 지정될 수 없습니다.  
  
*trigger_name*  
활성화할 트리거의 이름입니다.  
  
ALL  
ON 절의 범위에서 정의한 모든 트리거를 활성화할 것임을 나타냅니다.  
  
*object_name*  
실행할 DML 트리거 *trigger_name*이 만들어진 테이블 또는 뷰의 이름입니다.  
  
DATABASE  
DDL 트리거의 경우 데이터베이스 범위에서 실행하도록 *trigger_name*을 만들거나 수정했음을 나타냅니다.  
  
ALL SERVER  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
DDL 트리거의 경우 서버 범위에서 실행하도록 *trigger_name*을 만들거나 수정했음을 나타냅니다. ALL SERVER는 로그온 트리거에도 적용됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>설명  
트리거를 활성화해도 트리거를 다시 만드는 것은 아닙니다. 비활성화된 트리거는 현재 데이터베이스 내에 여전히 개체로 존재하지만 실행하지는 않습니다. 트리거를 활성화하려면 트리거가 원래 프로그래밍된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 실행될 때 트리거가 실행되도록 합니다. 트리거는 [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md)를 사용하여 비활성화됩니다. 테이블에 정의된 DML 트리거는 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)을 사용하여 비활성화되거나 활성화될 수도 있습니다.  
  
## <a name="permissions"></a>사용 권한  
DML 트리거를 활성화하려면 최소한 트리거가 만들어진 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
서버 범위(ON ALL SERVER)의 DDL 트리거 또는 LOGON 트리거를 활성화하려면 서버에 대한 CONTROL SERVER 권한이 필요합니다. 데이터베이스 범위(ON DATABASE)에서 DDL 트리거를 활성화하려면 최소한 현재 데이터베이스에 대한 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>A. 테이블의 DML 트리거 활성화  
다음 예에서는 AdventureWorks 데이터베이스의 `uAddress` 테이블에서 만든 `Address` 트리거를 비활성화한 다음, 다시 활성화하는 방법을 보여 줍니다.  
  
```sql  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>B. DDL 트리거 활성화  
다음 예에서는 데이터베이스 범위에서 DDL 트리거 `safety`를 만든 다음, 비활성화하고 활성화합니다.  
  
```sql  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. 같은 범위에서 정의된 모든 트리거 활성화  
다음 예에서는 서버 범위에서 만든 모든 DDL 트리거를 활성화합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상  
  
```sql  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  
