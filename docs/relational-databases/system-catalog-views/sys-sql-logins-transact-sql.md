---
description: sys.sql_logins(Transact-SQL)
title: sys.sql_logins (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_logins_TSQL
- sql_logins_TSQL
- sys.sql_logins
- sql_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_logins catalog view
ms.assetid: 0d9c5b09-86fe-40ff-baab-00b7c051402f
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb0fc659d82024dbbc52dc777b9f6ae5da3062ac
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477334"
---
# <a name="syssql_logins-transact-sql"></a>sys.sql_logins(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|--|**Sys.server_principals** 에서 상속 됩니다.|  
|**is_policy_checked**|**bit**|암호 정책이 확인됩니다.|  
|**is_expiration_checked**|**bit**|암호 만기가 확인됩니다.|  
|**password_hash**|**varbinary(256)**|SQL 로그인 암호의 해시입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 저장된 암호 정보는 솔트 암호의 SHA-512를 사용하여 계산됩니다.|  
  
 이 뷰가 상속 하는 열 목록은 [sys.server_principals &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)을 참조 하십시오. 및 열 `owning_principal_id` 은 `is_fixed_role` sys.server_principals에서 상속 되지 않습니다.
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인증 로그인 및 Windows 인증 로그인을 모두 보려면 [Sys.server_principals &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)를 참조 하세요.  
  
 포함 된 데이터베이스 사용자를 사용 하도록 설정 하면 로그인 없이 연결을 설정할 수 있습니다. 이러한 계정을 식별 하려면  [sys.database_principals &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)를 참조 하세요.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인은 자체 로그인 이름과 sa 로그인을 볼 수 있습니다. 다른 로그인을 보려면 로그인할 때 ALTER ANY LOGIN 또는 사용 권한이 필요합니다.  
 Password_hash 열의 내용을 보려면 CONTROL SERVER 권한이 필요 합니다.
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [암호 정책](../../relational-databases/security/password-policy.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
