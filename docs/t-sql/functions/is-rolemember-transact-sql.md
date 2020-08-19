---
description: IS_ROLEMEMBER(Transact-SQL)
title: IS_ROLEMEMBER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0df369f34c1993132ff6df45b1495c81f6ef6665
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417379"
---
# <a name="is_rolemember-transact-sql"></a>IS_ROLEMEMBER(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지정된 데이터베이스 보안 주체가 지정된 데이터베이스 역할의 멤버인지 여부를 나타냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 **'** *role* **'**  
 확인할 데이터베이스 역할의 이름입니다. *role*은 **sysname**입니다.  
  
 **'** *database_principal* **'**  
 확인할 데이터베이스 사용자, 데이터베이스 역할 또는 애플리케이션 역할의 이름입니다. *database_principal*은 **sysname**이며 기본값은 NULL입니다. 값을 지정하지 않으면 현재의 실행 컨텍스트에 따른 결과를 얻게 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
|반환 값|설명|  
|------------------|-----------------|  
|0|*database_principal*은 *역할*의 구성원이 아닙니다.|  
|1|*database_principal*은 *역할*의 구성원입니다.|  
|NULL|*database_principal* 또는 *역할*이 올바르지 않거나 역할 멤버 자격을 볼 수 있는 사용 권한이 없습니다.|  
  
## <a name="remarks"></a>설명  
 IS_ROLEMEMBER를 사용하여 현재 사용자가 데이터베이스 역할의 사용 권한이 필요한 동작을 수행할 수 있는지 여부를 확인할 수 있습니다.  
  
 *database_principal*에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 직접 액세스가 부여 또는 거부되지 않은 경우 *database_principal*이 Contoso\Mary5 등의 Windows 로그인 기반이면 IS_ROLEMEMBER가 NULL을 반환합니다.  
  
 선택적 *database_principal* 매개 변수가 제공되지 않고 *database_principal*이 Windows 도메인 로그인 기반일 경우 Windows 그룹의 멤버 자격을 통해 데이터베이스 역할의 멤버가 될 수 있습니다. 이러한 간접 멤버 자격을 확인하기 위해 IS_ROLEMEMBER는 도메인 컨트롤러에 Windows 그룹 멤버 자격 정보를 요청합니다. 도메인 컨트롤러에 액세스할 수 없거나 도메인 컨트롤러가 응답하지 않으면 IS_ROLEMEMBER가 사용자 및 사용자의 로컬 그룹만 고려하여 역할 멤버 자격 정보를 반환합니다. 지정된 사용자가 현재 사용자가 아닌 경우 IS_ROLEMEMBER가 반환하는 값이 인증자(예: Active Directory)의 마지막 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 업데이트와 다를 수 있습니다.  
  
 선택적 *database_principal* 매개 변수가 제공되지 않으면 쿼리 중인 데이터베이스 보안 주체가 sys.database_principals에 있어야 하거나 IS_ROLEMEMBER가 NULL을 반환합니다. 이는 *database_principal*이 이 데이터베이스에서 유효하지 않다는 의미입니다.  
  
 *database_principal* 매개 변수가 도메인 로그인 기반 또는 Windows 그룹을 기반으로 하고 도메인 컨트롤러에 액세스할 수 없는 경우 IS_ROLEMEMBER 호출이 실패하고 올바르지 않거나 불완전한 데이터가 반환될 수 있습니다.  
  
 도메인 컨트롤러를 사용할 수 없으면 로컬 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 같이 Windows 사용자를 로컬로 인증할 수 있는 경우 IS_ROLEMEMBER 호출이 정확한 정보를 반환합니다.  
  
 Windows 그룹이 데이터베이스 보안 주체 인수로 사용되는 경우 **IS_ROLEMEMBER**는 항상 0을 반환하며, 이 Windows 그룹은 지정된 데이터베이스 역할의 멤버인 또 다른 Windows 그룹의 멤버입니다.  
  
 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 및 Windows Server 2008의 UAC(사용자 계정 컨트롤)도 다른 결과를 반환할 수 있습니다. 이는 사용자가 Windows 그룹 멤버 또는 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 중 어떤 자격으로 서버에 액세스했는지에 따라 다릅니다.  
  
 이 함수는 기본 사용 권한이 아니라 역할 멤버 자격을 평가합니다. 예를 들어 **db_owner** 고정 데이터베이스 역할에는 **CONTROL DATABASE** 권한이 있습니다. 사용자가 **CONTROL DATABASE** 권한을 갖고 있지만 역할의 멤버는 아닌 경우 이 함수는 해당 사용자가 동일한 사용 권한을 갖고 있더라도 **db_owner** 역할의 멤버가 아닌 것으로 올바르게 보고합니다.  
  
## <a name="related-functions"></a>관련 함수  
 현재 사용자가 지정된 Windows 그룹의 멤버인지 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할의 멤버인지 확인하려면 [IS_MEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)를 사용하고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 서버 역할의 멤버인지 여부를 확인하려면 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)를 사용하세요.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스 역할에 대한 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 현재 사용자가 `db_datareader` 고정 데이터베이스 역할의 멤버인지 여부를 보여 줍니다.  
  
```  
IF IS_ROLEMEMBER ('db_datareader') = 1  
   print 'Current user is a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') = 0  
   print 'Current user is NOT a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') IS NULL  
   print 'ERROR: The database role specified is not valid.';  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [IS_MEMBER&#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
