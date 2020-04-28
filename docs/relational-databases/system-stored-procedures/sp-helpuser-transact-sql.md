---
title: sp_helpuser (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpuser
- sp_helpuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpuser
ms.assetid: 9c70b41d-ef4c-43df-92da-bd534c287ca1
author: stevestein
ms.author: sstein
ms.openlocfilehash: a170c5e43329d90a4977db12a98bd9d2e556e91d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68048165"
---
# <a name="sp_helpuser-transact-sql"></a>sp_helpuser(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 데이터베이스에서 데이터베이스 수준의 보안 주체 정보를 보고합니다.  
  
> [!IMPORTANT]  
>  **sp_helpuser** 는에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]도입 된 보안 개체에 대 한 정보를 반환 하지 않습니다. 대신 [database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) 를 사용 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpuser [ [ @name_in_db = ] 'security_account' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @name_in_db = ] 'security_account'`현재 데이터베이스에 있는 데이터베이스 사용자 또는 데이터베이스 역할의 이름입니다. *security_account* 는 현재 데이터베이스에 있어야 합니다. *security_account* 는 **sysname**이며 기본값은 NULL입니다. *Security_account* 지정 하지 않으면 **sp_helpuser** 모든 데이터베이스 보안 주체에 대 한 정보를 반환 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *security_account*에 대해 사용자 계정이 나 또는 Windows 사용자를 모두 지정 하지 않은 경우의 결과 집합을 보여 줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**이름**|**sysname**|현재 데이터베이스의 사용자입니다.|  
|**RoleName**|**sysname**|**사용자 이름이** 속해 있는 역할입니다.|  
|**LoginName**|**sysname**|**UserName**의 로그인입니다.|  
|**DefDBName**|**sysname**|**사용자 이름의**기본 데이터베이스입니다.|  
|**DefSchemaName**|**sysname**|데이터베이스 사용자의 기본 스키마입니다.|  
|**Id**|**smallint**|현재 데이터베이스의 **사용자 이름** ID입니다.|  
|**S**|**smallint**|사용자의 SID(보안 ID)입니다.|  
  
 다음 표에서는 사용자 계정이 지정되어 있지 않고 현재 데이터베이스에 별칭이 있는 경우의 결과 집합을 보여 줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|현재 데이터베이스에서 사용자의 별칭인 로그인입니다.|  
|**UserNameAliasedTo**|**sysname**|현재 데이터베이스에서 로그인을 별칭으로 사용하는 사용자 이름입니다.|  
  
 다음 표에서는 *security_account*에 대해 역할이 지정 된 경우의 결과 집합을 보여 줍니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Role_name**|**sysname**|현재 데이터베이스의 역할 이름입니다.|  
|**Role_id**|**smallint**|현재 데이터베이스에 있는 역할의 역할 ID입니다.|  
|**Users_in_role**|**sysname**|현재 데이터베이스에 있는 역할의 멤버입니다.|  
|**Id**|**smallint**|역할 멤버의 사용자 ID입니다.|  
  
## <a name="remarks"></a>설명  
 데이터베이스 역할의 멤버 자격에 대 한 정보를 보려면 [database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)를 사용 합니다. 서버 역할 구성원에 대 한 정보를 보려면 [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)를 사용 하 고 서버 수준 보안 주체에 대 한 정보를 보려면 [server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)를 사용 하십시오.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
 반환되는 정보는 메타데이터에 대한 액세스 제한 사항에 따라 달라집니다. 보안 주체에 사용 권한이 없는 엔터티는 나타나지 않습니다.  자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-all-users"></a>A. 모든 사용자 나열  
 다음 예에서는 현재 데이터베이스에 있는 사용자를 모두 나열합니다.  
  
```  
EXEC sp_helpuser;  
```  
  
### <a name="b-listing-information-for-a-single-user"></a>B. 단일 사용자에 관한 정보 나열  
 다음 예에서는 사용자 데이터베이스 소유자(`dbo`)에 대한 정보를 나열합니다.  
  
```  
EXEC sp_helpuser 'dbo';  
```  
  
### <a name="c-listing-information-for-a-database-role"></a>C. 데이터베이스 역할에 관한 정보 나열  
 다음 예에서는 `db_securityadmin` 고정 데이터베이스 역할에 대한 정보를 나열합니다.  
  
```  
EXEC sp_helpuser 'db_securityadmin';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [database_principals &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [database_role_members &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [server_principals &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
  
