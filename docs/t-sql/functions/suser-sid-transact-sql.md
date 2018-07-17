---
title: SUSER_SID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], users
- SIDs [SQL Server]
- security identifiers [SQL Server]
- users [SQL Server], logins
- 15401 (Database Engine error)
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- SUSER_SID function
ms.assetid: 57b42a74-94e1-4326-85f1-701b9de53c7d
caps.latest.revision: 31
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6d74a0a231c58b0b9828b96b902d3cda56a66ded
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785175"
---
# <a name="susersid-transact-sql"></a>SUSER_SID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정된 로그인 이름에 대한 SID(보안 ID)를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SUSER_SID ( [ 'login' ] [ , Param2 ] )   
```  
  
## <a name="arguments"></a>인수  
 **'** *login* **'**  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 사용자의 로그인 이름입니다. *login*은 **sysname**입니다. *login*은 선택 사항이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이나 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 또는 그룹일 수 있습니다. *login*을 지정하지 않은 경우에는 현재 보안 컨텍스트에 대한 정보가 반환됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
 *Param2*  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 로그인 이름의 유효성을 검사할지 여부를 지정합니다. *Param2*는 **int** 형식이며 선택 사항입니다. *Param2*가 0이면 로그인 이름의 유효성을 검사하지 않습니다. *Param2*가 0으로 지정되지 않으면 Windows 로그인 이름이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 로그인 이름과 정확하게 일치하는지 확인합니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary(85)**  
  
## <a name="remarks"></a>Remarks  
 SUSER_SID는 ALTER TABLE 또는 CREATE TABLE에서 DEFAULT 제약 조건으로 사용할 수 있습니다. SUSER_SID는 선택 목록, WHERE 절 및 식이 사용되는 곳은 어디에나 사용될 수 있습니다. SUSER_SID는 매개 변수를 지정하지 않더라도 항상 뒤에 괄호를 필요로 합니다.  
  
 지정된 인수 없이 호출된 경우 SUSER_SID는 현재 보안 컨텍스트의 SID를 반환합니다. EXECUTE AS를 사용하여 컨텍스트를 전환하는 일괄 처리 내에서 지정된 인수 없이 호출된 경우 SUSER_SID는 가장된 컨텍스트의 SID를 반환합니다. 가장된 컨텍스트에서 호출된 경우 SUSER_SID(ORIGINAL_LOGIN())은 원래 컨텍스트의 SID를 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬과 Windows 데이터 정렬이 서로 다르면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows에서 로그인을 서로 다른 형식으로 저장할 때 SUSER_SID가 실패할 수 있습니다. 예를 들어 Windows 컴퓨터인 TestComputer의 로그인이 User이고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 로그인을 TESTCOMPUTER\User로 저장하면 로그인 TestComputer\User 조회에서 로그인 이름을 올바르게 확인하지 못할 수 있습니다. 로그인 이름의 이 유효성 검사를 건너뛰려면 *Param2*를 사용합니다. 데이터 정렬이 서로 다르면 다음과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 15401이 발생하는 경우가 많습니다.  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="examples"></a>예  
  
### <a name="a-using-susersid"></a>1. SUSER_SID 사용  
 다음 예에서는 현재 보안 컨텍스트에 대한 SID(보안 ID)를 반환합니다.  
  
```  
SELECT SUSER_SID();  
```  
  
### <a name="b-using-susersid-with-a-specific-login"></a>2. 특정 로그인에 SUSER_SID 사용  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa` 로그인에 대한 보안 ID를 반환합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
```  
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-susersid-with-a-windows-user-name"></a>3. Windows 사용자 이름과 SUSER_SID 사용  
 다음 예에서는 Windows 사용자 `London\Workstation1`에 대한 보안 ID를 반환합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
```  
SELECT SUSER_SID('London\Workstation1');  
GO  
```  
  
### <a name="d-using-susersid-as-a-default-constraint"></a>4. SUSER_SID를 DEFAULT 제약 조건으로 사용  
 다음 예에서는 `SUSER_SID`를 `DEFAULT` 문의 `CREATE TABLE` 제약 조건으로 사용합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sid_example  
(  
login_sid   varbinary(85) DEFAULT SUSER_SID(),  
login_name  varchar(30) DEFAULT SYSTEM_USER,  
login_dept  varchar(10) DEFAULT 'SALES',  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sid_example DEFAULT VALUES;  
GO  
```  
  
### <a name="e-comparing-the-windows-login-name-to-the-login-name-stored-in-sql-server"></a>5. Windows 로그인 이름을 SQL Server에 저장된 로그인 이름과 비교  
 다음 예에서는 *Param2*를 사용하여 Windows에서 SID를 가져오는 방법을 보여 주고 해당 SID를 `SUSER_SNAME` 함수에 대한 입력으로 사용합니다. 이 예에서는 Windows에 저장된 형식으로 로그인을 제공하고(`TestComputer\User`), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 형식으로 로그인을 반환합니다(`TESTCOMPUTER\User`).  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
```  
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>참고 항목  
 [ORIGINAL_LOGIN&#40;Transact-SQL&#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [binary 및 varbinary&#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
