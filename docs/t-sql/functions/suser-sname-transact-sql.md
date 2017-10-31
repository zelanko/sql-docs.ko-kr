---
title: SUSER_SNAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_SNAME_TSQL
- SUSER_SNAME
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- SIDs [SQL Server]
- SUSER_SNAME function
- users [SQL Server], logins
- logins [SQL Server], names
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- names [SQL Server], logins
ms.assetid: 11ec7d86-d429-4004-a436-da25df9f8761
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 35e3429d49940cd863cd04fc336226268ddf61c9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="susersname-transact-sql"></a>SUSER_SNAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  SID(보안 ID)와 연결된 로그인 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
## <a name="arguments"></a>인수  
 *server_user_sid*  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 선택적 로그인 보안 ID입니다. *server_user_sid* 은 **varbinary(85)**합니다. *server_user_sid* 의 보안 id 번호 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 또는 그룹입니다. 경우 *server_user_sid* 은 지정 하지 않으면 현재 사용자에 대 한 정보가 반환 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar (128)**  
  
## <a name="remarks"></a>주의  
 SUSER_SNAME을 ALTER TABLE 또는 CREATE TABLE에서 DEFAULT 제약 조건으로 사용할 수 있습니다. SUSER_SNAME은 SELECT 목록이나 WHERE 절, 그리고 식이 사용되는 모든 곳에 사용할 수 있습니다. 지정된 매개 변수가 없는 경우에도 SUSER_SNAME 다음에는 항상 괄호가 나와야 합니다.  
  
 인수 없이 SUSER_SNAME이 호출되면 현재 보안 컨텍스트의 이름이 반환됩니다. EXECUTE AS를 사용하여 컨텍스트를 전환한 일괄 처리 내에서 인수 없이 SUSER_SNAME이 호출되면 가장된 컨텍스트의 이름이 반환됩니다. 가장된 컨텍스트에서 SUSER_SNAME이 호출된 경우 ORIGINAL_LOGIN은 원래 컨텍스트의 이름을 반환합니다.  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-remarks"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 주의 사항  
 SUSER_NAME은 항상 현재 보안 컨텍스트에 대한 로그인 이름을 반환합니다.  
  
 SUSER_SNAME 문은 EXECUTE AS를 통해 가장된 보안 컨텍스트를 사용하는 실행을 지원하지 않습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-susersname"></a>1. SUSER_SNAME 사용  
 다음 예에서는 현재 보안 컨텍스트의 로그인 이름을 반환합니다.  
  
```  
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-susersname-with-a-windows-user-security-id"></a>2. Windows 사용자의 SID로 SUSER_SNAME 사용  
 다음 예에서는 Windows SID와 연결된 로그인 이름을 반환합니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-susersname-as-a-default-constraint"></a>3. DEFAULT 제약 조건으로 SUSER_SNAME 사용  
 다음 예에서는 `SUSER_SNAME`를 `DEFAULT` 문의 `CREATE TABLE` 제약 조건으로 사용합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sname_example  
(  
login_sname sysname DEFAULT SUSER_SNAME(),  
employee_id uniqueidentifier DEFAULT NEWID(),  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sname_example DEFAULT VALUES;  
GO  
```  
  
### <a name="d-calling-susersname-in-combination-with-execute-as"></a>4. SUSER_SNAME을 EXECUTE AS와 함께 호출  
 이 예에서는 SUSER_SNAME이 가장된 컨텍스트에서 호출된 경우의 동작을 보여 줍니다.  
  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME();  
GO  
EXECUTE AS LOGIN = 'WanidaBenShoof';  
SELECT SUSER_SNAME();  
REVERT;  
GO  
SELECT SUSER_SNAME();  
GO  
  
```  
  
 결과는 다음과 같습니다.  
  
 ```
sa  
WanidaBenShoof  
sa
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-susersname"></a>5. SUSER_SNAME 사용  
 다음 예에서는 `0x01` 값을 갖는 SID에 대한 로그인 이름을 반환합니다.  
  
```  
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>6. 현재 로그인을 반환합니다.  
 다음 예에서는 현재 로그인의 로그인 이름을 반환합니다.  
  
```  
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SUSER_SID &#40; Transact SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [실행 AS &#40; Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  


