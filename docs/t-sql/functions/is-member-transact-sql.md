---
title: IS_MEMBER(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IS_MEMBER
- IS_MEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], members
- current member status
- roles [SQL Server], members
- testing member status
- members [SQL Server]
- checking member status
- IS_MEMBER function
- verifying member status
- groups [SQL Server], members
- members [SQL Server], verifying
ms.assetid: 77cb68a0-19b7-4fe1-ab17-e5587699631b
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c94ef5422af2e659a679c3377e7bcea63800b14c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33054590"
---
# <a name="ismember-transact-sql"></a>IS_MEMBER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 사용자가 지정된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 그룹 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할의 멤버인지 여부를 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>인수  
 **'** *group* **'**  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지
  
 검사할 Windows 그룹의 이름으로 *도메인*\\*그룹* 형식이어야 합니다. *그룹*은 **sysname**입니다.  
  
 **'** *role* **'**  
 확인할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할의 이름입니다. *역할*은 **sysname**이며 데이터베이스 고정 역할이나 사용자 정의 역할은 포함할 수 있으나 서버 역할은 포함할 수 없습니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>Remarks  
 IS_MEMBER는 다음과 같은 값을 반환합니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|0|현재 사용자가 *그룹* 또는 *역할*의 멤버가 아닙니다.|  
|1|현재 사용자가 *그룹* 또는 *역할*의 멤버입니다.|  
|NULL|*그룹* 또는 *역할*이 유효하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 응용 프로그램 역할을 사용하는 로그인에서 쿼리하는 경우 Windows 그룹에 대해 NULL을 반환합니다.|  
  
 IS_MEMBER는 Windows에서 만든 액세스 토큰을 검사하여 Windows 그룹 멤버를 결정합니다. 액세스 토큰은 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 후에 변경된 그룹 멤버 변경 내용을 반영하지 않습니다. Windows 그룹 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램 역할에서 쿼리할 수 없습니다.  
  
 데이터베이스 역할에서 멤버를 추가하고 제거하려면 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)를 사용합니다. 모든 서버 역할에서 멤버를 추가하고 제거하려면 [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)를 사용합니다.  
  
 이 함수는 기본 사용 권한이 아니라 역할 멤버 자격을 평가합니다. 예를 들어 **db_owner** 고정 데이터베이스 역할에는 **CONTROL DATABASE** 권한이 있습니다. 사용자가 **CONTROL DATABASE** 권한을 갖고 있지만 역할의 멤버는 아닌 경우 이 함수는 해당 사용자가 동일한 사용 권한을 갖고 있더라도 **db_owner** 역할의 멤버가 아닌 것으로 올바르게 보고합니다.  
  
 **sysadmin** 고정 서버 역할의 멤버는 모든 데이터베이스를 **dbo** 사용자로 입력합니다. **sysadmin** 고정 서버 역할의 멤버에 대한 사용 권한을 확인하려면 원래의 로그인이 아닌 **dbo**에 대한 사용 권한을 확인합니다. **dbo**는 데이터베이스 역할에 추가될 수 없으며 Windows 그룹에 존재하지 않으므로 **dbo**는 항상 0을 반환합니다.(또는 역할이 존재하지 않으면 NULL을 반환합니다)  
  
## <a name="related-functions"></a>관련 함수  
 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 데이터베이스 역할의 멤버인지 여부를 확인하려면 [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md)를 사용하고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 서버 역할의 멤버인지 여부를 확인하려면 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)를 사용하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 사용자가 데이터베이스 역할 또는 Windows 도메인 그룹의 멤버인지 확인합니다.  
  
```  
-- Test membership in db_owner and print appropriate message.  
IF IS_MEMBER ('db_owner') = 1  
   PRINT 'Current user is a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') = 0  
   PRINT 'Current user is NOT a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') IS NULL  
   PRINT 'ERROR: Invalid group / role specified';  
GO  
  
-- Execute SELECT if user is a member of ADVWORKS\Shipping.  
IF IS_MEMBER ('ADVWORKS\Shipping') = 1  
   SELECT 'User ' + USER + ' is a member of ADVWORKS\Shipping.';   
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
