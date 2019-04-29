---
title: sp_enum_proxy_for_subsystem (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5beab3dc255e5679191dd6ea5d05bfdd98bef6ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62723827"
---
# <a name="spenumproxyforsubsystem-transact-sql"></a>sp_enum_proxy_for_subsystem(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시가 하위 시스템에 액세스할 수 있는 권한을 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @proxy_id = ] proxy_id` 정보를 나열할 프록시의 id. 합니다 *proxy_id* 됩니다 **int**, 기본값은 NULL 사용 하 여 합니다. 중 하나는 *id* 또는 *proxy_name* 지정할 수 있습니다.  
  
`[ @proxy_name = ] 'proxy_name'` 정보를 나열할 프록시의 이름입니다. 합니다 *proxy_name* 됩니다 **sysname**, 기본값은 NULL 사용 하 여 합니다. 중 하나는 *id* 또는 *proxy_name* 지정할 수 있습니다.  
  
`[ @subsystem_id = ] subsystem_id` 정보를 나열할 하위 시스템의 id. 합니다 *subsystem_id* 됩니다 **int**, 기본값은 NULL 사용 하 여 합니다. 중 하나는 *subsystem_id* 또는 *subsystem_name* 지정할 수 있습니다.  
  
`[ @subsystem_name = ] 'subsystem_name'` 정보를 나열할 하위 시스템의 이름입니다. 합니다 *subsystem_name* 됩니다 **sysname**, 기본값은 NULL 사용 하 여 합니다. 중 하나는 *subsystem_id* 또는 *subsystem_name* 지정할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|하위 시스템의 ID입니다.|  
|**subsystem_name**|**sysname**|하위 시스템의 이름입니다.|  
|**proxy_id**|**int**|프록시 ID입니다.|  
|**proxy_name**|**sysname**|프록시 이름입니다.|  
  
## <a name="remarks"></a>Remarks  
 매개 변수 없이 제공 하는 경우 **sp_enum_proxy_for_subsystem** 모든 하위 시스템에 대 한 인스턴스의 모든 프록시에 대 한 정보를 나열 합니다.  
  
 프록시 id 또는 프록시 이름을 제공 하면 **sp_enum_proxy_for_subsystem** 에 대 한 액세스를 프록시 하는 하위 시스템을 나열 합니다. 하위 시스템 id 또는 하위 시스템 이름을 제공 하면 **sp_enum_proxy_for_subsystem** 해당 하위 시스템에 액세스할 수 있는 프록시를 나열 합니다.  
  
 프록시 정보와 하위 시스템 정보를 모두 제공한 경우 지정한 프록시가 지정한 하위 시스템에 액세스할 수 있으면 결과 집합은 행을 반환합니다.  
  
 이 저장된 프로시저에 위치한 **msdb**합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저 기본의 멤버에 대 한 실행 권한을 합니다 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-all-associations"></a>1. 모든 연결 나열  
 다음 예에서는 현재 인스턴스의 프록시와 하위 시스템 간에 설정된 모든 사용 권한을 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>2. 프록시가 특정 하위 시스템에 액세스할 수 있는지 확인  
 다음 예에서는 프록시 `Catalog application proxy`가 `ActiveScripting` 하위 시스템에 액세스할 수 있는 경우 행을 반환합니다. 그렇지 않으면 빈 결과 집합을 반환합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_grant_proxy_to_subsystem &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
