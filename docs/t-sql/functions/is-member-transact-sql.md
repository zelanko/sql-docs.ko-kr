---
title: IS_MEMBER (Transact SQL) | Microsoft Docs
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 472d8f1cc258fdc57ef454fbb35f51e3f83b288d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="ismember-transact-sql"></a>IS_MEMBER(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 사용자가 지정된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 그룹 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할의 멤버인지 여부를 표시합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>인수  
 **'** *그룹* **'**  
**적용 대상**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 통해[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 검사할 Windows 그룹의 이름 형식에 있어야 *도메인*\\*그룹*합니다. *그룹* 은 **sysname**합니다.  
  
 **'** *역할* **'**  
 이름인는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 역할 확인 하는 중입니다. *역할* 은 **sysname** 데이터베이스 역할 또는 사용자 정의 역할 있으 나 서버 역할 하지 고정 포함 될 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>주의  
 IS_MEMBER는 다음과 같은 값을 반환합니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|0|현재 사용자의 구성원이 아닙니다. *그룹* 또는 *역할*합니다.|  
|1.|현재 사용자가 멤버인 *그룹* 또는 *역할*합니다.|  
|NULL|어느 *그룹* 또는 *역할* 올바르지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 응용 프로그램 역할을 사용하는 로그인에서 쿼리하는 경우 Windows 그룹에 대해 NULL을 반환합니다.|  
  
 IS_MEMBER는 Windows에서 만든 액세스 토큰을 검사하여 Windows 그룹 멤버를 결정합니다. 액세스 토큰은 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 후에 변경된 그룹 멤버 변경 내용을 반영하지 않습니다. Windows 그룹 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램 역할에서 쿼리할 수 없습니다.  
  
 추가 하 고 데이터베이스 역할에서 구성원 제거을 사용 하 여 [ALTER role&#40; Transact SQL &#41; ](../../t-sql/statements/alter-role-transact-sql.md). 추가 하 고 서버 역할에서 구성원 제거을 사용 하 여 [ALTER SERVER role&#40; Transact SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 이 함수는 기본 사용 권한이 아니라 역할 멤버 자격을 평가합니다. 예를 들어는 **db_owner** 고정된 데이터베이스 역할에는 **제어 데이터베이스** 권한. 사용자에 게 있으면는 **제어 데이터베이스** 권한에 포함 있지만 역할의 멤버는 아닌 경우이 함수는 잘못 보고 하 여 사용자의 구성원이 아닙니다는 **db_owner** 역할을 사용자에 게 동일한 경우에 사용 권한입니다.  
  
 멤버는 **sysadmin** 으로 모든 데이터베이스를 입력 하는 고정된 서버 역할의 **dbo** 사용자입니다. 멤버에 대 한 사용 권한을 확인 하는 **sysadmin** 고정된 서버 역할에 대 한 권한을 확인 **dbo**, 원래 로그인 하지 않습니다. 이후 **dbo** 데이터베이스 역할에 추가할 수 없습니다 및 Windows 그룹에 존재 하지 않는 **dbo** 0 또는 NULL 역할 존재 하지 않는 경우 항상 반환 됩니다.  
  
## <a name="related-functions"></a>관련 함수  
 여부를 확인 하려면 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 데이터베이스 역할의 멤버를 사용 하 여 [IS_ROLEMEMBER &#40; Transact SQL &#41; ](../../t-sql/functions/is-rolemember-transact-sql.md). 확인 하려면 여부는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 서버 역할의 멤버를 사용 하 여 [IS_SRVROLEMEMBER &#40; Transact SQL &#41; ](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Is_srvrolemember&#40; Transact SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

