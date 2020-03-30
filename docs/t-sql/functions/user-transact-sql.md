---
title: USER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USER
- USER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- system-supplied usernames [SQL Server]
- USER function
- users [SQL Server], database names
- names [SQL Server], database users
- database usernames [SQL Server]
ms.assetid: 82bbbd94-870c-4c43-9ed9-d9abc767a6be
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 46bb30958394b2196c5521620cf503f4558a6f82
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73844317"
---
# <a name="user-transact-sql"></a>USER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  기본값이 지정되지 않은 경우에 현재 사용자의 데이터베이스 사용자 이름에 대해 시스템이 제공한 값을 테이블에 삽입할 수 있도록 허용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
USER  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(128)**  
  
## <a name="remarks"></a>설명  
 USER는 USER_NAME 시스템 함수와 같은 기능을 제공합니다.  
  
 USER를 CREATE TABLE 또는 ALTER TABLE 문에서 DEFAULT 제약 조건으로 사용하거나 임의의 표준 함수로 사용합니다.  
  
 USER는 항상 현재 컨텍스트의 이름을 반환합니다. EXECUTE AS 문 다음에 USER를 호출하면 가장된 컨텍스트의 이름이 반환됩니다.  
  
 Windows 보안 주체가 그룹 멤버 자격으로 데이터베이스에 액세스하는 경우 USER는 그룹 이름 대신 Windows 보안 주체의 이름을 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-user-to-return-the-database-user-name"></a>A. USER를 사용하여 데이터베이스 사용자 이름 반환  
 다음 예에서는 변수를 `char`로 선언하고 USER의 현재 값을 변수에 할당한 다음 텍스트 설명과 함께 변수를 인쇄합니다.  
  
```  
DECLARE @usr char(30)  
SET @usr = user  
SELECT 'The current user''s database username is: '+ @usr  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-----------------------------------------------------------------------  
The current user's database username is: dbo  
  
(1 row(s) affected)
```  
  
### <a name="b-using-user-with-default-constraints"></a>B. DEFAULT 제약 조건으로 USER 사용  
 다음 예에서는 판매 행의 판매원에 대한 `USER` 제약 조건으로 `DEFAULT`를 사용하여 테이블을 만듭니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE inventory22  
(  
 part_id int IDENTITY(100, 1) NOT NULL,  
 description varchar(30) NOT NULL,  
 entry_person varchar(30) NOT NULL DEFAULT USER   
)  
GO  
INSERT inventory22 (description)  
VALUES ('Red pencil')  
INSERT inventory22 (description)  
VALUES ('Blue pencil')  
INSERT inventory22 (description)  
VALUES ('Green pencil')  
INSERT inventory22 (description)  
VALUES ('Black pencil')  
INSERT inventory22 (description)  
VALUES ('Yellow pencil')  
GO  
```  
  
 다음은 `inventory22` 테이블에서 모든 정보를 선택하는 쿼리입니다.  
  
```  
SELECT * FROM inventory22 ORDER BY part_id;  
GO  
```  
  
 결과 집합은 다음과 같습니다(`entry-person` 값 참고).  
  
 ```
part_id     description                    entry_person
----------- ------------------------------ -------------------------
100         Red pencil                     dbo
101         Blue pencil                    dbo
102         Green pencil                   dbo
103         Black pencil                   dbo
104         Yellow pencil                  dbo
  
(5 row(s) affected)
```  
  
### <a name="c-using-user-in-combination-with-execute-as"></a>C. EXECUTE AS와 함께 USER 사용  
 다음 예에서는 가장된 세션 내부에서 호출된 `USER`의 동작을 보여 줍니다.  
  
```  
SELECT USER;  
GO  
EXECUTE AS USER = 'Mario';  
GO  
SELECT USER;  
GO  
REVERT;  
GO  
SELECT USER;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
DBO
Mario
DBO
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact-SQL&#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [SESSION_USER &#40;Transact-SQL&#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)   
 [USER_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/user-name-transact-sql.md)  
  
  

