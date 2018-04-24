---
title: IS_SRVROLEMEMBER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
caps.latest.revision: 65
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1ae1dac9be576e6f1c6c2c83164bd83e2716d658
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="issrvrolemember-transact-sql"></a>IS_SRVROLEMEMBER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 지정된 서버 역할의 멤버인지 여부를 나타냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
## <a name="arguments"></a>인수  
 **'** *role* **'**  
 확인할 서버 역할의 이름입니다. *role*은 **sysname**입니다.  
  
 *role*의 유효한 값은 사용자 정의 서버 역할이며 다음 고정 서버 역할입니다.  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> public|  
|processadmin||  
  
 **'** *login* **'**  
 점검할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름입니다. *login*은 **sysname**이며 기본값은 NULL입니다. 값을 지정하지 않으면 현재의 실행 컨텍스트에 따른 결과를 얻게 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
|반환 값|Description|  
|------------------|-----------------|  
|0|*login*은 *role*의 구성원이 아닙니다.<br /><br /> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 이 문은 항상 0을 반환합니다.|  
|1|*login*은 *role*의 구성원입니다.|  
|NULL|*role* 또는 *login*이 올바르지 않거나 역할 멤버 자격을 볼 수 있는 사용 권한이 없습니다.|  
  
## <a name="remarks"></a>Remarks  
 UseIS_SRVROLEMEMBER를 사용하여 현재 사용자가 서버 역할의 사용 권한이 필요한 동작을 수행할 수 있는지 여부를 확인할 수 있습니다.  
  
 *login*에 Contoso\Mary5와 같은 Windows 로그인이 지정된 경우 해당 로그인에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 직접 액세스가 허용 또는 거부되지 않으면 **IS_SRVROLEMEMBER**가 **NULL**을 반환합니다.  
  
 선택적 *login* 매개 변수를 제공하지 않고 *login*이 Windows 도메인 로그인인 경우 Windows 그룹 멤버 자격을 통해 고정 서버 역할의 멤버가 될 수 있습니다. 이러한 간접 멤버 자격을 확인하기 위해 IS_SRVROLEMEMBER는 도메인 컨트롤러에 Windows 그룹 멤버 자격 정보를 요청합니다. 도메인 컨트롤러에 액세스할 수 없거나 도메인 컨트롤러가 응답하지 않으면 **IS_SRVROLEMEMBER**가 사용자 및 사용자의 로컬 그룹만 고려하여 역할 멤버 자격 정보를 반환합니다. 지정된 사용자가 현재 사용자가 아닌 경우 IS_SRVROLEMEMBER가 반환하는 값이 인증자(예: Active Directory)의 마지막 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 업데이트와 다를 수 있습니다.  
  
 선택적 로그인 매개 변수를 제공하지 않으면 쿼리 중인 Windows 로그인이 sys.server_principals에 있어야 하거나 IS_SRVROLEMEMBER가 NULL을 반환합니다. 이것은 올바른 로그인이 아님을 나타냅니다.  
  
 로그인 매개 변수가 도메인 로그인이거나 Windows 그룹을 기반으로 하고 도메인 컨트롤러에 액세스할 수 없는 경우 IS_SRVROLEMEMBER 호출이 실패하고 올바르지 않거나 불완전한 데이터가 반환될 수 있습니다.  
  
 도메인 컨트롤러를 사용할 수 없으면 IS_SRVROLEMEMBER 호출은 로컬 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 같이 Windows 사용자를 로컬로 인증할 수 있는 경우 정확한 정보를 반환합니다.  
  
 Windows 그룹이 로그인 인수로 사용되는 경우 **IS_SRVROLEMEMBER**는 항상 0을 반환하며, 이 Windows 그룹은 지정된 서버 역할의 멤버인 또 다른 Windows 그룹의 멤버입니다.  
  
 사용자 계정 컨트롤(UAC) 설정도 다른 결과가 반환되는 원인이 될 수 있습니다. 이는 사용자가 Windows 그룹 멤버 또는 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 중 어떤 자격으로 서버에 액세스했는지에 따라 다릅니다.  
  
 이 함수는 기본 사용 권한이 아니라 역할 멤버 자격을 평가합니다. 예를 들어 **sysadmin** 고정 서버 역할에는 **CONTROL SERVER** 권한이 있습니다. 사용자가 **CONTROL SERVER** 권한을 갖고 있지만 역할의 멤버는 아닌 경우 이 함수는 해당 사용자가 동일한 사용 권한을 갖고 있더라도 **sysadmin** 역할의 멤버가 아닌 것으로 올바르게 보고합니다.  
  
## <a name="related-functions"></a>관련 함수  
 현재 사용자가 지정된 Windows 그룹의 멤버인지 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할의 멤버인지 확인하려면 [IS_MEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)를 사용하고, 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 데이터베이스 역할의 멤버인지 여부를 확인하려면 [IS_ROLEMEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md)를 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 서버 역할에 대한 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 사용자의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 `sysadmin` 고정 서버 역할의 멤버인지 여부를 보여 줍니다.  
  
```  
IF IS_SRVROLEMEMBER ('sysadmin') = 1  
   print 'Current user''s login is a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') = 0  
   print 'Current user''s login is NOT a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') IS NULL  
   print 'ERROR: The server role specified is not valid.';  
```  
  
 다음 예에서는 도메인 로그인 Pat가 **diskadmin** 고정 서버 역할의 멤버인지 여부를 보여 줍니다.  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>참고 항목  
 [IS_MEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
