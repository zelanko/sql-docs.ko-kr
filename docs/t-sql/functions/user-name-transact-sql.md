---
title: USER_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USER_NAME
- USER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- IDs [SQL Server], databases
- USER_NAME function
- users [SQL Server], database username
- names [SQL Server], database users
- identification numbers [SQL Server], databases
- database usernames [SQL Server]
ms.assetid: ab32d644-4228-449a-9ef0-5a975c305775
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e407ab5ac5e69c78d19a1022210ca8da5e470d64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927592"
---
# <a name="username-transact-sql"></a>USER_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 ID 번호에서 데이터베이스 사용자 이름을 반환합니다.  
  
 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
USER_NAME ( [ id ] )  
```  
  
## <a name="arguments"></a>인수  
 *id*  
 데이터베이스 사용자와 연결된 ID 번호입니다. *id*는 **int**입니다. 괄호가 필요합니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar(256)**  
  
## <a name="remarks"></a>Remarks  
 *id*를 생략하면 현재 컨텍스트의 현재 사용자로 가정하여 지정됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다. EXECUTE AS 문 다음에 *id*를 지정하지 않고 USER_NAME을 호출하면 USER_NAME은 가장된 사용자의 이름을 반환합니다. Windows 보안 주체가 그룹 멤버 자격으로 데이터베이스에 액세스하는 경우 USER_NAME은 그룹 이름 대신 Windows 보안 주체의 이름을 반환합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-username"></a>1\. USER_NAME 사용  
 다음 예에서는 사용자 ID `13`에 대한 사용자 이름을 반환합니다.  
  
```  
SELECT USER_NAME(13);  
GO  
```  
  
### <a name="b-using-username-without-an-id"></a>2\. ID 없이 USER_NAME 사용  
 다음 예에서는 ID를 지정하지 않고 현재 사용자의 이름을 찾습니다.  
  
```  
SELECT USER_NAME();  
GO  
```  
  
 sysadmin 고정 서버 역할의 멤버인 사용자의 경우 결과 집합은 다음과 같습니다.  
  
 ```
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="c-using-username-in-the-where-clause"></a>C. WHERE 절에서 USER_NAME 사용  
 다음 예에서는 `sysusers`에서 `USER_NAME` 시스템 함수를 사용자 ID 번호 `1`에 적용하는 결과와 이름이 동일한 행을 찾습니다.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
name  
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="d-calling-username-during-impersonation-with-execute-as"></a>D. EXECUTE AS로 가장하는 동안 USER_NAME 호출  
 다음 예에서는 가장이 진행되는 동안의 `USER_NAME` 작동 방식을 보여 줍니다.  
  
```  
SELECT USER_NAME();  
GO  
EXECUTE AS USER = 'Zelig';  
GO  
SELECT USER_NAME();  
GO  
REVERT;  
GO  
SELECT USER_NAME();  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
DBO  
Zelig  
DBO
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-username-without-an-id"></a>E. ID 없이 USER_NAME 사용  
 다음 예에서는 ID를 지정하지 않고 현재 사용자의 이름을 찾습니다.  
  
```  
SELECT USER_NAME();  
```  
  
 현재 로그인한 사용자에 대한 결과 집합입니다.  
  
```  
------------------------------   
User7                              
```  
  
### <a name="f-using-username-in-the-where-clause"></a>F. WHERE 절에서 USER_NAME 사용  
 다음 예에서는 `sysusers`에서 `USER_NAME` 시스템 함수를 사용자 ID 번호 `1`에 적용하는 결과와 이름이 동일한 행을 찾습니다.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
name                             
------------------------------   
User7                              
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact-SQL&#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40;Transact-SQL&#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SYSTEM_USER&#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)  
  
