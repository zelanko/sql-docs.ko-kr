---
description: SYSTEM_USER(Transact-SQL)
title: SYSTEM_USER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SYSTEM_USER_TSQL
- SYSTEM_USER
dev_langs:
- TSQL
helpviewer_keywords:
- current user names
- system-supplied user names [SQL Server]
- users [SQL Server], logins
- logins [SQL Server], identification name
- current system user names
- SYSTEM_USER function
- inserting system user name into table
- system usernames [SQL Server]
- users [SQL Server], names
ms.assetid: 565984cd-60c6-4df7-83ea-2349b838ccb2
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 83684cab677210f0c584a7554042fbe2ce8f8a80
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480404"
---
# <a name="system_user-transact-sql"></a>SYSTEM_USER(Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  기본값이 지정되지 않은 경우에 현재 로그인에 대해 시스템이 제공한 값을 테이블에 삽입할 수 있도록 허용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
SYSTEM_USER  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식  
 **nvarchar(128)**  
  
## <a name="remarks"></a>설명  
 CREATE TABLE 및 ALTER TABLE 문에서 SYSTEM_USER 함수를 DEFAULT 제약 조건으로 사용할 수 있습니다. 이 함수를 표준 함수로 사용할 수도 있습니다.  
  
 사용자 이름과 로그인 이름이 다르면 SYSTEM_USER가 로그인 이름을 반환합니다.  
  
 현재 사용자가 Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로그인하면 SYSTEM_USER는 Windows 로그인 ID 이름을 다음과 같은 형식으로 반환합니다. *DOMAIN*\\*user_login_name*. 하지만 현재 사용자가 SQL Server 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로그인한 경우에는 SYSTEM_USER가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 ID 이름을 반환합니다. 예를 들어 `WillisJo`로 로그인한 사용자의 경우에는 `WillisJo`를 반환합니다.  
  
 SYSTEM_USER는 현재 실행 중인 컨텍스트의 이름을 반환합니다. EXECUTE AS 문이 컨텍스트를 전환하는 데 사용된 경우에는 SYSTEM_USER가 가장된 컨텍스트의 이름을 반환합니다.  

 SYSTEM_USER로 실행할 수 없습니다.

## <a name="examples"></a>예  
  
### <a name="a-using-system_user-to-return-the-current-system-user-name"></a>A. SYSTEM_USER를 사용하여 현재 시스템 사용자 이름 반환  
 다음 예에서는 `char` 변수를 선언하고 변수에 `SYSTEM_USER`의 현재 값을 저장한 다음에 변수에 저장된 값을 출력합니다.  
  
```sql
DECLARE @sys_usr CHAR(30);  
SET @sys_usr = SYSTEM_USER;  
SELECT 'The current system user is: '+ @sys_usr;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
----------------------------------------------------------
The current system user is: WillisJo

(1 row(s) affected)
 ```  
  
### <a name="b-using-system_user-with-default-constraints"></a>B. DEFAULT 제약 조건으로 SYSTEM_USER 사용  
 다음 예에서는 `SYSTEM_USER` 열에 대한 `DEFAULT` 제약 조건으로 `SRep_tracking_user`를 사용하는 테이블을 만듭니다.  
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.Sales_Tracking  
(  
    Territory_id INT IDENTITY(2000, 1) NOT NULL,  
    Rep_id INT NOT NULL,  
    Last_sale DATETIME NOT NULL DEFAULT GETDATE(),  
    SRep_tracking_user VARCHAR(30) NOT NULL DEFAULT SYSTEM_USER  
);  
GO  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (151);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (293, '19980515');  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (27882, '19980620');  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (21392);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (24283, '19981130');  
GO  
```  
  
 다음 쿼리는 `Sales_Tracking` 테이블에서 모든 정보를 선택합니다.  
  
```sql
SELECT * FROM Sales_Tracking ORDER BY Rep_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Territory_id Rep_id Last_sale            SRep_tracking_user
-----------  ------ -------------------- ------------------
2000         151    Mar 4 1998 10:36AM   ArvinDak
2001         293    May 15 1998 12:00AM  ArvinDak
2003         21392  Mar 4 1998 10:36AM   ArvinDak
2004         24283  Nov 3 1998 12:00AM   ArvinDak
2002         27882  Jun 20 1998 12:00AM  ArvinDak
  
(5 row(s) affected)
 ```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-system_user-to-return-the-current-system-user-name"></a>3. SYSTEM_USER를 사용하여 현재 시스템 사용자 이름 반환  
 다음 예에서는 `SYSTEM_USER`의 현재 값을 반환합니다.  
  
```sql
SELECT SYSTEM_USER;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact-SQL&#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40;Transact-SQL&#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [USER &#40;Transact-SQL&#41;](../../t-sql/functions/user-transact-sql.md)  
  
  

