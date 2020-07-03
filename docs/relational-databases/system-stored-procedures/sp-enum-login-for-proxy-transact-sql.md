---
title: sp_enum_login_for_proxy (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: cd65937894956ff008a08ea6f15222d6d020ba2e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891951"
---
# <a name="sp_enum_login_for_proxy-transact-sql"></a>sp_enum_login_for_proxy(Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  보안 주체와 프록시 간 연결을 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @name = ] 'name'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]프록시를 나열할 보안 주체, 로그인, 서버 역할 또는 **msdb** 데이터베이스 역할의 이름입니다. 이름은 **nvarchar (256)** 이며 기본값은 NULL입니다.  
  
`[ @proxy_id = ] id`정보를 나열할 프록시의 프록시 id입니다. *Proxy_id* 은 **int**이며 기본값은 NULL입니다. *Id* 또는 *proxy_name* 지정할 수 있습니다.  
  
`[ @proxy_name = ] 'proxy_name'`정보를 나열할 프록시의 이름입니다. *Proxy_name* 는 **sysname**이며 기본값은 NULL입니다. *Id* 또는 *proxy_name* 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|프록시 ID입니다.|  
|**proxy_name**|**sysname**|프록시 이름입니다.|  
|**name**|**sysname**|연결할 보안 주체의 이름입니다.|  
|**flags**|**int**|보안 주체의 유형입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인<br /><br /> **1** = 고정 시스템 역할<br /><br /> **2** = **msdb** 의 데이터베이스 역할|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>설명  
 매개 변수를 제공 하지 않으면 모든 프록시에 대 한 인스턴스의 모든 로그인에 대 한 정보가 **sp_enum_login_for_proxy** 나열 됩니다.  
  
 프록시 id 또는 프록시 이름이 제공 되는 경우 **sp_enum_login_for_proxy** 는 프록시에 대 한 액세스 권한이 있는 로그인을 나열 합니다. 로그인 이름이 제공 되는 경우 **sp_enum_login_for_proxy** 로그인에 액세스할 수 있는 프록시를 나열 합니다.  
  
 프록시 정보와 로그인 이름을 모두 제공하는 경우 지정한 로그인이 지정한 프록시에 액세스할 수 있으면 결과 집합은 행을 반환합니다.  
  
 이 저장 프로시저는 **msdb**에 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-all-associations"></a>A. 모든 연결 나열  
 다음 예에서는 현재 인스턴스의 로그인과 프록시 간에 설정된 모든 사용 권한을 나열합니다.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. 특정 로그인에 대한 프록시 나열  
 다음 예에서는 `terrid` 로그인이 액세스할 수 있는 프록시를 나열합니다.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_help_proxy &#40;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [Transact-sql&#41;sp_grant_login_to_proxy &#40;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [Transact-sql&#41;sp_revoke_login_from_proxy &#40;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
