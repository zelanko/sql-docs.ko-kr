---
description: sp_enum_proxy_for_subsystem(Transact-SQL)
title: sp_enum_proxy_for_subsystem (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: f484764e05a23594c32494934a9c366154e02aeb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489446"
---
# <a name="sp_enum_proxy_for_subsystem-transact-sql"></a>sp_enum_proxy_for_subsystem(Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시가 하위 시스템에 액세스할 수 있는 권한을 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @proxy_id = ] proxy_id` 정보를 나열할 프록시의 id입니다. *Proxy_id* 은 **int**이며 기본값은 NULL입니다. *Id* 또는 *proxy_name* 지정할 수 있습니다.  
  
`[ @proxy_name = ] 'proxy_name'` 정보를 나열할 프록시의 이름입니다. *Proxy_name* 는 **sysname**이며 기본값은 NULL입니다. *Id* 또는 *proxy_name* 지정할 수 있습니다.  
  
`[ @subsystem_id = ] subsystem_id` 정보를 나열할 하위 시스템의 id입니다. *Subsystem_id* 은 **int**이며 기본값은 NULL입니다. *Subsystem_id* 또는 *subsystem_name* 를 지정할 수 있습니다.  
  
`[ @subsystem_name = ] 'subsystem_name'` 정보를 나열할 하위 시스템의 이름입니다. *Subsystem_name* 는 **sysname**이며 기본값은 NULL입니다. *Subsystem_id* 또는 *subsystem_name* 를 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|하위 시스템의 ID입니다.|  
|**subsystem_name**|**sysname**|하위 시스템의 이름입니다.|  
|**proxy_id**|**int**|프록시 ID입니다.|  
|**proxy_name**|**sysname**|프록시 이름입니다.|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>설명  
 매개 변수를 제공 하지 않으면 모든 하위 시스템에 대 한 인스턴스의 모든 프록시에 대 한 정보가 **sp_enum_proxy_for_subsystem** 나열 됩니다.  
  
 프록시 id 또는 프록시 이름이 제공 되는 경우 **sp_enum_proxy_for_subsystem** 는 프록시가 액세스할 수 있는 하위 시스템을 나열 합니다. 하위 시스템 id 또는 하위 시스템 이름을 제공 하면 **sp_enum_proxy_for_subsystem** 해당 하위 시스템에 대 한 액세스 권한이 있는 프록시가 나열 됩니다.  
  
 프록시 정보와 하위 시스템 정보를 모두 제공한 경우 지정한 프록시가 지정한 하위 시스템에 액세스할 수 있으면 결과 집합은 행을 반환합니다.  
  
 이 저장 프로시저는 **msdb**에 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-listing-all-associations"></a>A. 모든 연결 나열  
 다음 예에서는 현재 인스턴스의 프록시와 하위 시스템 간에 설정된 모든 사용 권한을 나열합니다.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. 프록시가 특정 하위 시스템에 액세스할 수 있는지 확인  
 다음 예에서는 프록시 `Catalog application proxy`가 `ActiveScripting` 하위 시스템에 액세스할 수 있는 경우 행을 반환합니다. 그렇지 않으면 빈 결과 집합을 반환합니다.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_grant_proxy_to_subsystem &#40;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
