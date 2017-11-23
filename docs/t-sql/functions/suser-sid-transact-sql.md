---
title: SUSER_SID (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs: TSQL
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
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 77c7ab84b6fe936722f0b0c18ca889922485f1fd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
 **'** *로그인* **'**  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 사용자의 로그인 이름입니다. *로그인* 은 **sysname**합니다. *로그인*은, 선택 사항이 될 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 또는 그룹입니다. 경우 *로그인* 은 지정 하지 않으면 현재 보안 컨텍스트에 대 한 정보가 반환 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
 *매개 변수 2가*  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 로그인 이름의 유효성을 검사할지 여부를 지정합니다. *매개 변수 2가* 유형의 **int** 며 선택 사항입니다. 때 *매개 변수 2가* 가 0 이면 로그인 이름을 유효성이 검사 되지 않습니다. 때 *매개 변수 2가* Windows 로그인 이름 확인에 저장 된 동일 하 게 정확 하 게 로그인 이름으로 0으로 지정 하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary(85)**  
  
## <a name="remarks"></a>주의  
 SUSER_SID는 ALTER TABLE 또는 CREATE TABLE에서 DEFAULT 제약 조건으로 사용할 수 있습니다. SUSER_SID는 선택 목록, WHERE 절 및 식이 사용되는 곳은 어디에나 사용될 수 있습니다. SUSER_SID는 매개 변수를 지정하지 않더라도 항상 뒤에 괄호를 필요로 합니다.  
  
 지정된 인수 없이 호출된 경우 SUSER_SID는 현재 보안 컨텍스트의 SID를 반환합니다. EXECUTE AS를 사용하여 컨텍스트를 전환하는 일괄 처리 내에서 지정된 인수 없이 호출된 경우 SUSER_SID는 가장된 컨텍스트의 SID를 반환합니다. 가장된 컨텍스트에서 호출된 경우 SUSER_SID(ORIGINAL_LOGIN())은 원래 컨텍스트의 SID를 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬과 Windows 데이터 정렬이 서로 다르면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows에서 로그인을 서로 다른 형식으로 저장할 때 SUSER_SID가 실패할 수 있습니다. 예를 들어 Windows 컴퓨터인 TestComputer의 로그인이 User이고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 로그인을 TESTCOMPUTER\User로 저장하면 로그인 TestComputer\User 조회에서 로그인 이름을 올바르게 확인하지 못할 수 있습니다. 로그인 이름의 유효성이 검사를 건너뛰려면를 사용 하 여 *매개 변수 2가*합니다. 데이터 정렬이 서로 다르면 다음과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 15401이 발생하는 경우가 많습니다.  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="examples"></a>예  
  
### <a name="a-using-susersid"></a>1. SUSER_SID 사용  
 다음 예에서는 현재 보안 컨텍스트에 대한 SID(보안 ID)를 반환합니다.  
  
```  
SELECT SUSER_SID('sa');  
```  
  
### <a name="b-using-susersid-with-a-specific-login"></a>2. 특정 로그인에 SUSER_SID 사용  
 에 대 한 보안 id 번호를 반환 하는 다음 예제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa` 로그인 합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-susersid-with-a-windows-user-name"></a>3. Windows 사용자 이름과 SUSER_SID 사용  
 다음 예에서는 Windows 사용자 `London\Workstation1`에 대한 보안 ID를 반환합니다.  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
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
 다음 예제에서는 사용 하는 방법을 보여 줍니다. *매개 변수 2가* Windows에서 SID를 얻을 수 및 해당 SID에 대 한 입력으로 사용 하 여는 `SUSER_SNAME` 함수입니다. 이 예에서는 Windows에 저장된 형식으로 로그인을 제공하고(`TestComputer\User`), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장된 형식으로 로그인을 반환합니다(`TESTCOMPUTER\User`).  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>관련 항목:  
 [ORIGINAL_LOGIN &#40; Transact SQL &#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [binary 및 varbinary&#40; Transact SQL &#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [시스템 함수 &#40; Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
