---
title: IS_SRVROLEMEMBER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c26c0c1f4cb6a22f50cdc6a87d7a31f25b65e138
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
 **'** *역할* **'**  
 확인할 서버 역할의 이름입니다. *역할* 은 **sysname**합니다.  
  
 유효한 값에 대 한 *역할* 는 사용자 정의 서버 역할 및 다음 고정 서버 역할:  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지<br /><br /> public|  
|processadmin||  
  
 **'** *로그인* **'**  
 이름인는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 검사할 로그인 합니다. *로그인* 은 **sysname**, 기본값은 NULL입니다. 값을 지정하지 않으면 현재의 실행 컨텍스트에 따른 결과를 얻게 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
|반환 값|Description|  
|------------------|-----------------|  
|0|*로그인* 의 구성원이 아니므로 *역할*합니다.<br /><br /> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)],이 문은 항상 0을 반환 합니다.|  
|1.|*로그인* 의 멤버인 *역할*합니다.|  
|NULL|*역할* 또는 *로그인* 유효 하지 않거나 역할 멤버 자격을 볼 수 있는 권한이 없습니다.|  
  
## <a name="remarks"></a>주의  
 현재 사용자가 서버 역할의 사용 권한이 필요한 동작을 수행할 수 있는지 여부를 확인 하려면 UseIS_SRVROLEMEMBER 합니다.  
  
 Contoso\Mary5, 등으로 Windows 로그인에 대 한 지정 된 경우 *로그인*, **IS_SRVROLEMEMBER** 반환 **NULL**로그인에 부여 되었거나 거부에 대 한 직접 액세스 하지 않는 한, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 경우 선택적 *로그인* 매개 변수가 제공 되지 않고 경우 *로그인* Windows 도메인 로그인, Windows 그룹의 멤버 자격을 통해 고정된 서버 역할의 멤버 수 있습니다. 이러한 간접 멤버 자격을 확인하기 위해 IS_SRVROLEMEMBER는 도메인 컨트롤러에 Windows 그룹 멤버 자격 정보를 요청합니다. 도메인 컨트롤러를 액세스할 수 없거나 응답 하지 않으면 경우 **IS_SRVROLEMEMBER** 사용자 및의 로컬 그룹만 고려 하 여 역할 멤버 자격 정보를 반환 합니다. 지정된 사용자가 현재 사용자가 아닌 경우 IS_SRVROLEMEMBER가 반환하는 값이 인증자(예: Active Directory)의 마지막 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 업데이트와 다를 수 있습니다.  
  
 선택적 로그인 매개 변수를 제공하지 않으면 쿼리 중인 Windows 로그인이 sys.server_principals에 있어야 하거나 IS_SRVROLEMEMBER가 NULL을 반환합니다. 이것은 올바른 로그인이 아님을 나타냅니다.  
  
 로그인 매개 변수가 도메인 로그인이거나 Windows 그룹을 기반으로 하고 도메인 컨트롤러에 액세스할 수 없는 경우 IS_SRVROLEMEMBER 호출이 실패하고 올바르지 않거나 불완전한 데이터가 반환될 수 있습니다.  
  
 도메인 컨트롤러를 사용할 수 없으면 IS_SRVROLEMEMBER 호출은 로컬 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 같이 Windows 사용자를 로컬로 인증할 수 있는 경우 정확한 정보를 반환합니다.  
  
 **IS_SRVROLEMEMBER** Windows 그룹이 로그인 인수로 사용 되 고이 Windows 그룹에 지정된 된 서버 역할의 멤버 차례로 이며 다른 Windows 그룹의 구성원은 항상 0을 반환 합니다.  
  
 사용자 계정 컨트롤 (UAC) 설정을 않을 수 있습니다 다른 결과 반환 합니다. 이는 사용자가 Windows 그룹 멤버 또는 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 중 어떤 자격으로 서버에 액세스했는지에 따라 다릅니다.  
  
 이 함수는 기본 사용 권한이 아니라 역할 멤버 자격을 평가합니다. 예를 들어는 **sysadmin** 고정된 서버 역할에는 **제어 서버** 권한. 사용자에 게 있으면는 **제어 서버** 권한에 포함 있지만 역할의 멤버는 아닌 경우이 함수는 잘못 보고 하 여 사용자의 구성원이 아닙니다는 **sysadmin** 역할을 사용자에 게 동일한 경우에 사용 권한입니다.  
  
## <a name="related-functions"></a>관련 함수  
 현재 사용자 지정된 된 Windows 그룹의 구성원 인지 확인 하려면 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할을 사용 하 여 [IS_MEMBER &#40; Transact SQL &#41; ](../../t-sql/functions/is-member-transact-sql.md). 확인 하려면 여부는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 데이터베이스 역할의 멤버를 사용 하 여 [IS_ROLEMEMBER &#40; Transact SQL &#41; ](../../t-sql/functions/is-rolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
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
  
 다음 예에서는 도메인 로그인 Pat의 멤버 인지를 나타냅니다.는 **diskadmin** 고정된 서버 역할입니다.  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Is_member&#40; Transact SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

