---
title: sp_help_proxy (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 051f41139627420e825feffb292a02905917705d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891700"
---
# <a name="sp_help_proxy-transact-sql"></a>sp_help_proxy(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  하나 이상의 프록시에 대한 정보를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>인수  
`[ @proxy_id = ] id`정보를 나열할 프록시의 프록시 id입니다. *Proxy_id* 은 **int**이며 기본값은 NULL입니다. *Id* 또는 *proxy_name* 지정할 수 있습니다.  
  
`[ @proxy_name = ] 'proxy_name'`정보를 나열할 프록시의 이름입니다. *Proxy_name* 는 **sysname**이며 기본값은 NULL입니다. *Id* 또는 *proxy_name* 지정할 수 있습니다.  
  
`[ @subsystem_name = ] 'subsystem_name'`프록시를 나열할 하위 시스템의 이름입니다. *Subsystem_name* 는 **sysname**이며 기본값은 NULL입니다. *Subsystem_name* 지정 된 경우에도 *이름을* 지정 해야 합니다.  
  
 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|설명|  
|-----------|-----------------|  
|ActiveScripting|ActiveX 스크립트|  
|CmdExec|운영 체제(CmdExec)|  
|스냅샷|Replication Snapshot Agent|  
|LogReader|복제 로그 판독기 에이전트|  
|분포|복제 배포 에이전트|  
|병합|Replication Merge Agent|  
|QueueReader|복제 큐 판독기 에이전트|  
|ANALYSISQUERY|Analysis Services 명령|  
|ANALYSISCOMMAND|Analysis Services 쿼리|  
|Dts|SSIS 패키지 실행|  
|PowerShell|PowerShell 스크립트|  
  
`[ @name = ] 'name'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]프록시를 나열할 로그인의 이름입니다. 이름은 **nvarchar (256)** 이며 기본값은 NULL입니다. *Name* 을 지정 하면 *subsystem_name* 도 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|프록시 ID입니다.|  
|**name**|**sysname**|프록시 이름입니다.|  
|**credential_identity**|**sysname**|프록시와 연관된 자격 증명의 Microsoft Windows 도메인 이름 및 사용자 이름입니다.|  
|**사용**|**tinyint**|이 프록시가 사용되는지 여부입니다. { **0** = 사용 안 함, **1** = 사용}|  
|**한**|**nvarchar(1024)**|이 프록시에 대한 설명입니다.|  
|**user_sid**|**varbinary(85)**|이 프록시에 대한 Windows 사용자의 Windows 보안 ID입니다.|  
|**credential_id**|**int**|이 프록시와 연관된 자격 증명의 식별자입니다.|  
|**credential_identity_exists**|**int**|credential_identity가 있는지 여부입니다. { 0 = 없음, 1 = 있음 }|  
  
## <a name="remarks"></a>설명  
 매개 변수를 제공 하지 않으면 **sp_help_proxy** 는 인스턴스의 모든 프록시에 대 한 정보를 나열 합니다.  
  
 지정 된 하위 시스템에 대해 로그인에서 사용할 수 있는 프록시를 확인 하려면 *이름* 및 *subsystem_name*를 지정 합니다. 이러한 인수를 제공 하면 **sp_help_proxy** 는 지정 된 로그인이 액세스할 수 있고 지정 된 하위 시스템에 사용할 수 있는 프록시를 나열 합니다.  
  
## <a name="permissions"></a>사용 권한  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 **msdb** 데이터베이스의 **SQLAgentOperatorRole** 고정 데이터베이스 역할을 부여 받아야 합니다.  
  
 **SQLAgentOperatorRole**에 대 한 자세한 내용은 [고정 데이터베이스 역할 SQL Server 에이전트](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조 하세요.  
  
> [!NOTE]  
>  **Sysadmin** 의 멤버가이 저장 프로시저를 실행 하는 경우에만 **credential_identity** 및 **user_sid** 열이 결과 집합에 반환 됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-information-for-all-proxies"></a>A. 모든 프록시에 대한 정보 나열  
 다음 예에서는 인스턴스의 모든 프록시에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. 특정 작업에 대한 정보 나열  
 다음 예에서는 `Catalog application proxy`라는 프록시에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_add_proxy &#40;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [Transact-sql&#41;sp_delete_proxy &#40;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
