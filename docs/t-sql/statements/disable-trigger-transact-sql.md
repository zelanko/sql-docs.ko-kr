---
title: DISABLE TRIGGER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DISABLE_TSQL
- DISABLE
- DISABLE TRIGGER
- DISABLE_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DML triggers, disabling
- DDL triggers, disabling
- DISABLE TRIGGER statement
- triggers [SQL Server], disabling
- disabling triggers
ms.assetid: e6529f06-e442-437e-a7bf-41790bc092c5
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 02888ae3de27c6859cd37bec9119761f4777b2bd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="disable-trigger-transact-sql"></a>DISABLE TRIGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  트리거를 비활성화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DISABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 트리거가 속한 스키마의 이름입니다. *schema_name* DDL 또는 logon 트리거에 대해서는 지정할 수 없습니다.  
  
 *trigger_name*  
 비활성화할 트리거의 이름입니다.  
  
 ALL  
 ON 절의 범위에서 정의된 모든 트리거가 비활성화되었음을 나타냅니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 병합 복제용으로 게시된 데이터베이스에서 트리거를 만듭니다. 게시된 데이터베이스에서 ALL을 지정하면 이 두 트리거가 비활성화되어 복제가 중단됩니다. ALL을 지정하려면 먼저 현재 데이터베이스가 병합 복제용으로 게시되었는지를 확인하세요.  
  
 *object_name*  
 DML 트리거는 뷰나 테이블의 이름인 *trigger_name* 실행을 생성 합니다.  
  
 DATABASE  
 DDL 트리거를 하 고 있음을 나타냅니다 *trigger_name* 작성 또는 데이터베이스 범위에서 실행 하도록 수정 합니다.  
  
 ALL SERVER  
 **적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 DDL 트리거를 하 고 있음을 나타냅니다 *trigger_name* 작성 또는 서버 범위에서 실행 하도록 수정 합니다. ALL SERVER는 로그온 트리거에도 적용됩니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>주의  
 트리거 생성 될 때 기본적으로 활성화 됩니다. 트리거를 비활성화하면 트리거는 삭제되지 않고 현재 데이터베이스의 개체로 남아 있습니다. 그러나 해당 트리거가 프로그래밍된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하는 경우에도 트리거는 실행되지 않습니다. 사용 하 여 트리거를 다시 설정할 수 있습니다 [ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md)합니다. 테이블에 정의 된 DML 트리거 수 또한 비활성화 되거나 활성화 될를 사용 하 여 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)합니다.  
  
 트리거를 사용 하 여 변경 된 **ALTER TRIGGER** 문은 트리거를 설정 합니다.  
  
## <a name="permissions"></a>Permissions  
 DML 트리거를 비활성화하려면 사용자에게 최소한 트리거를 만든 테이블 또는 뷰에 대한 ALTER 권한이 필요합니다.  
  
 서버 범위(ON ALL SERVER)의 DDL 트리거 또는 로그온 트리거를 비활성화하려면 서버에 대한 CONTROL SERVER 권한이 필요합니다. 데이터베이스 범위(ON DATABASE)에서 DDL 트리거를 비활성화하려면 사용자에게 최소한 현재 데이터베이스에서 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
다음 예에서는 AdventureWorks2012 데이터베이스에 설명 되어 있습니다.
  
### <a name="a-disabling-a-dml-trigger-on-a-table"></a>1. 테이블에 대한 DML 트리거 비활성화  
 다음 예에서는 `uAddress` 테이블에 만들어진 `Address` 트리거를 비활성화합니다.  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-disabling-a-ddl-trigger"></a>2. DDL 트리거 비활성화  
 다음 예에서는 데이터베이스 범위에서 DDL 트리거 `safety`를 만든 후 비활성화합니다.  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-disabling-all-triggers-that-were-defined-with-the-same-scope"></a>3. 같은 범위에서 정의된 모든 트리거 비활성화  
 다음 예에서는 서버 범위에서 만든 모든 DDL 트리거를 비활성화합니다.  
  
```  
DISABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ENABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  

