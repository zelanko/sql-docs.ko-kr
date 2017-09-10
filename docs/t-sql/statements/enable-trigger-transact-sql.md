---
title: ENABLE TRIGGER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fb2fba080ea3c51e5c29456b2166eeea6274f8a3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  DML, DDL 또는 LOGON 트리거를 활성화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>인수  
 *schema_name*  
 트리거가 속한 스키마의 이름입니다. *schema_name* DDL 또는 logon 트리거에 대해서는 지정할 수 없습니다.  
  
 *trigger_name*  
 활성화할 트리거의 이름입니다.  
  
 ALL  
 ON 절의 범위에서 정의한 모든 트리거를 활성화할 것임을 나타냅니다.  
  
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
 트리거를 활성화하더라도 트리거를 다시 만드는 것은 아닙니다. 비활성화된 트리거는 현재 데이터베이스 내에 여전히 개체로 존재하지만 시작하지는 않습니다. 트리거를 활성화하면 트리거를 시작하도록 원래 프로그래밍된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 실행될 때마다 트리거가 시작됩니다. 트리거를 사용 하 여 비활성화 됩니다 [DISABLE TRIGGER](../../t-sql/statements/disable-trigger-transact-sql.md)합니다. 테이블에 정의 된 DML 트리거 수 또한 비활성화 되거나 활성화 될를 사용 하 여 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 DML 트리거를 활성화하려면 최소한 트리거가 만들어진 테이블이나 뷰에 대한 ALTER 권한이 필요합니다.  
  
 서버 범위(ON ALL SERVER)의 DDL 트리거 또는 LOGON 트리거를 활성화하려면 서버에 대한 CONTROL SERVER 권한이 필요합니다. 데이터베이스 범위(ON DATABASE)에서 DDL 트리거를 활성화하려면 최소한 현재 데이터베이스에 대한 ALTER ANY DATABASE DDL TRIGGER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>1. 테이블의 DML 트리거 활성화  
 트리거를 비활성화 하는 다음 예제에서는 `uAddress` 테이블에 만든 `Address` AdventureWorks 데이터베이스의 한 다음 다시 활성화 합니다.  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>2. DDL 트리거 활성화  
 다음 예에서는 DDL 트리거를 만듭니다. `safety` 와 데이터베이스 범위, 한 다음 사용 하지 않도록 설정 하 고 활성화 합니다.  
  
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
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>3. 같은 범위에서 정의된 모든 트리거 활성화  
 다음 예에서는 서버 범위에서 만든 모든 DDL 트리거를 활성화합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
```  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DISABLE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  

