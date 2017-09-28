---
title: CURRENT_USER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURRENT_USER
- CURRENT_USER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- current user names
- niladic functions
- CURRENT_USER
- users [SQL Server], names
ms.assetid: 29248949-325b-4063-9f55-5a445fb35c6e
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9edbc344723da335de150f5e829820eaef1d983e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="currentuser-transact-sql"></a>CURRENT_USER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

현재 사용자의 이름을 반환합니다. 이 함수는 USER_NAME()과 동등합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CURRENT_USER  
```  

## <a name="return-types"></a>반환 형식
**sysname**
  
## <a name="remarks"></a>주의  
CURRENT_USER는 현재 보안 컨텍스트의 이름을 반환합니다. EXECUTE AS 호출로 컨텍스트를 전환한 후 CURRENT_USER를 실행하면 가장된 컨텍스트 이름이 반환됩니다. Windows 보안 주체가 그룹의 멤버 자격을 통해 데이터베이스에 액세스한 경우에는 그룹 이름 대신 Windows 보안 주체 이름이 반환됩니다.
  
현재 사용자의 로그인을 반환 하려면 참조 [SUSER_NAME &#40; Transact SQL &#41; ](../../t-sql/functions/suser-name-transact-sql.md) 및 [SYSTEM_USER &#40; Transact SQL &#41; ](../../t-sql/functions/system-user-transact-sql.md).
  
## <a name="examples"></a>예  
  
### <a name="a-using-currentuser-to-return-the-current-user-name"></a>1. CURRENT_USER를 사용하여 현재 사용자 이름 반환  
다음 예에서는 현재 사용자의 이름을 반환합니다.
  
```sql
SELECT CURRENT_USER;  
GO  
```  
  
### <a name="b-using-currentuser-as-a-default-constraint"></a>2. CURRENT_USER를 DEFAULT 제약 조건으로 사용  
다음 예에서는 판매 행의 `CURRENT_USER` 열에 대한 `DEFAULT` 제약 조건으로 `order_person`를 사용하는 테이블을 만듭니다.
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'orders22')  
   DROP TABLE orders22;  
GO  
SET NOCOUNT ON;  
CREATE TABLE orders22  
(  
order_id int IDENTITY(1000, 1) NOT NULL,
cust_id  int NOT NULL,
order_date smalldatetime NOT NULL DEFAULT GETDATE(),
order_amt money NOT NULL,
order_person char(30) NOT NULL DEFAULT CURRENT_USER
);  
GO  
```  
  
다음 코드에서는 테이블에 레코드 하나를 삽입합니다. 이러한 문을 실행하고 있는 사용자의 이름은 `Wanida`입니다.
  
```sql
INSERT orders22 (cust_id, order_amt)  
VALUES (5105, 577.95);  
GO  
SET NOCOUNT OFF;  
GO  
```  
  
다음 쿼리는 `orders22` 테이블에서 모든 정보를 선택합니다.
  
```sql
SELECT * FROM orders22;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`order_id    cust_id     order_date           order_amt    order_person`
  
`----------- ----------- -------------------- ------------ ------------`
  
`1000        5105        2005-04-03 23:34:00  577.95       Wanida`
  
`(1 row(s) affected)`
  
### <a name="c-using-currentuser-from-an-impersonated-context"></a>3. 가장된 컨텍스트에서 CURRENT_USER 사용  
다음 예에서 `Wanida` 사용자는 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행합니다.
  
```sql
SELECT CURRENT_USER;  
GO  
EXECUTE AS USER = 'Arnalfo';  
GO  
SELECT CURRENT_USER;  
GO  
REVERT;  
GO  
SELECT CURRENT_USER;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`Wanida`
  
`Arnalfo`
  
`Wanida`
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-currentuser-to-return-the-current-user-name"></a>D: CURRENT_USER를 사용 하 여 현재 사용자 이름을 반환 하는  
다음 예에서는 현재 사용자의 이름을 반환합니다.
  
```sql
SELECT CURRENT_USER;  
```  
  
## <a name="see-also"></a>참고 항목
[USER_NAME &#40; Transact SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)  
[SYSTEM_USER &#40; Transact SQL &#41;](../../t-sql/functions/system-user-transact-sql.md)  
[sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[시스템 함수 &#40; Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  


