---
title: IS_ROLEMEMBER (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_ROLEMEMBER
- IS_ROLEMEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_ROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 73efa688-ae91-4014-98bc-1cabe47321f7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fd8574c27bea00127096dc1f0040c8c3f93e96cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="isrolemember-transact-sql"></a>IS_ROLEMEMBER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  지정된 데이터베이스 보안 주체가 지정된 데이터베이스 역할의 멤버인지 여부를 나타냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
## <a name="arguments"></a>인수  
 **'** *역할* **'**  
 확인할 데이터베이스 역할의 이름입니다. *역할* 은 **sysname**합니다.  
  
 **'** *데이터베이스 _ 보안 주체* **'**  
 확인할 데이터베이스 사용자, 데이터베이스 역할 또는 응용 프로그램 역할의 이름입니다. *데이터베이스 _ 보안 주체* 은 **sysname**, 기본값은 NULL입니다. 값을 지정하지 않으면 현재의 실행 컨텍스트에 따른 결과를 얻게 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
|반환 값|Description|  
|------------------|-----------------|  
|0|*데이터베이스 _ 보안 주체* 의 구성원이 아니므로 *역할*합니다.|  
|1.|*데이터베이스 _ 보안 주체* 의 멤버인 *역할*합니다.|  
|NULL|*데이터베이스 _ 보안 주체* 또는 *역할* 유효 하지 않거나 역할 멤버 자격을 볼 수 있는 권한이 없습니다.|  
  
## <a name="remarks"></a>주의  
 IS_ROLEMEMBER를 사용하여 현재 사용자가 데이터베이스 역할의 사용 권한이 필요한 동작을 수행할 수 있는지 여부를 확인할 수 있습니다.  
  
 경우 *데이터베이스 _ 보안 주체* Contoso\Mary5, IS_ROLEMEMBER는 NULL을 반환 하지 않는 한와 같은 Windows 로그인 기반는 *데이터베이스 _ 보안 주체* 부여 하거나 직접 액세스를 거부 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 경우 선택적 *데이터베이스 _ 보안 주체* 매개 변수가 제공 되지 않고 경우는 *데이터베이스 _ 보안 주체* 기반 Windows 도메인 로그인에는 Windows 그룹의 멤버 자격을 통해 데이터베이스 역할의 멤버는 것 . 이러한 간접 멤버 자격을 확인하기 위해 IS_ROLEMEMBER는 도메인 컨트롤러에 Windows 그룹 멤버 자격 정보를 요청합니다. 도메인 컨트롤러에 액세스할 수 없거나 도메인 컨트롤러가 응답하지 않으면 IS_ROLEMEMBER가 사용자 및 사용자의 로컬 그룹만 고려하여 역할 멤버 자격 정보를 반환합니다. 지정된 사용자가 현재 사용자가 아닌 경우 IS_ROLEMEMBER가 반환하는 값이 인증자(예: Active Directory)의 마지막 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 업데이트와 다를 수 있습니다.  
  
 경우 선택적 *데이터베이스 _ 보안 주체* 매개 변수를 제공 하 고, 쿼리 되는 데이터베이스 보안 주체는 sys.database_principals에 존재 해야 합니다. 또는 IS_ROLEMEMBER가 NULL을 반환 합니다. 이 나타내는 *데이터베이스 _ 보안 주체* 이 데이터베이스에서 유효 하지 않습니다.  
  
 경우는 *데이터베이스 _ 보안 주체* 매개 변수가 도메인 로그인 기반 또는 Windows 그룹 기반 및 도메인 컨트롤러에 액세스할 수 없으면, IS_ROLEMEMBER에 대 한 호출에 실패 하 고 올바르지 않거나 불완전 한 데이터를 반환할 수 있습니다.  
  
 도메인 컨트롤러를 사용할 수 없으면 로컬 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 같이 Windows 사용자를 로컬로 인증할 수 있는 경우 IS_ROLEMEMBER 호출이 정확한 정보를 반환합니다.  
  
 **IS_ROLEMEMBER** Windows 그룹이 데이터베이스 보안 주체 인수로 사용 되 고이 Windows 그룹에 지정된 된 데이터베이스 역할의 멤버 차례로 이며 다른 Windows 그룹의 구성원은 항상 0을 반환 합니다.  
  
 사용자 계정 컨트롤 (UAC)에서 찾은 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 및 Windows Server 2008도 다른 결과 반환할 수 있습니다. 이는 사용자가 Windows 그룹 멤버 또는 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 중 어떤 자격으로 서버에 액세스했는지에 따라 다릅니다.  
  
 이 함수는 기본 사용 권한이 아니라 역할 멤버 자격을 평가합니다. 예를 들어는 **db_owner** 고정된 데이터베이스 역할에는 **제어 데이터베이스** 권한. 사용자에 게 있으면는 **제어 데이터베이스** 권한에 포함 있지만 역할의 멤버는 아닌 경우이 함수는 잘못 보고 하 여 사용자의 구성원이 아닙니다는 **db_owner** 역할을 사용자에 게 동일한 경우에 사용 권한입니다.  
  
## <a name="related-functions"></a>관련 함수  
 현재 사용자 지정된 된 Windows 그룹의 구성원 인지 확인 하려면 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할을 사용 하 여 [IS_MEMBER &#40; Transact SQL &#41; ](../../t-sql/functions/is-member-transact-sql.md). 확인 하려면 여부는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 서버 역할의 멤버를 사용 하 여 [IS_SRVROLEMEMBER &#40; Transact SQL &#41; ](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 데이터베이스 역할에 대한 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 사용자가 `db_datareader` 고정 데이터베이스 역할의 멤버인지 여부를 보여 줍니다.  
  
```  
IF IS_ROLEMEMBER ('db_datareader') = 1  
   print 'Current user is a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') = 0  
   print 'Current user is NOT a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') IS NULL  
   print 'ERROR: The database role specified is not valid.';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER role&#40; Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP role&#40; Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [서버 역할 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER role&#40; Transact SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [DROP SERVER role&#40; Transact SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Is_member&#40; Transact SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [Is_srvrolemember&#40; Transact SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
