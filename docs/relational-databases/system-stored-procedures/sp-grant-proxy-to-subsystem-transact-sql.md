---
title: sp_grant_proxy_to_subsystem (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_subsystem_TSQL
- sp_grant_login_to_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_proxy_to_subsystem
ms.assetid: 866aaa27-a1e0-453a-9b1b-af39431ad9c2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 96e044b94244492202058d6dc2b2f048a9c1db6c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123818"
---
# <a name="spgrantproxytosubsystem-transact-sql"></a>sp_grant_proxy_to_subsystem(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하위 시스템에 프록시 액세스 권한을 부여합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_grant_proxy_to_subsystem  
     { [ @proxy_id = ] proxy_id | [ @proxy_name = ] 'proxy_name' },  
     { [ @subsystem_id = ] subsystem_id | [ @subsystem_name = ] 'subsystem_name' }  
```  
  
## <a name="arguments"></a>인수  
`[ @proxy_id = ] id` 에 대 한 액세스 권한을 부여할 프록시의 프록시 id. 합니다 *proxy_id* 됩니다 **int**, 기본값은 NULL 사용 하 여 합니다. 어느 *proxy_id* 하거나 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @proxy_name = ] 'proxy_name'` 에 대 한 액세스 권한을 부여할 프록시의 이름입니다. 합니다 *proxy_name* 됩니다 **sysname**, 기본값은 NULL 사용 하 여 합니다. 어느 *proxy_id* 하거나 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @subsystem_id = ] id` 에 대 한 액세스를 부여할 하위 시스템의 id. 합니다 *subsystem_id* 됩니다 **int**, 기본값은 NULL 사용 하 여 합니다. 어느 *subsystem_id* 하거나 *subsystem_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 스크립트<br /><br /> **\*\* 중요 \* \***  ActiveX 스크립팅 하위 시스템에서 제거 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이후 버전에서 에이전트 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.|  
|**3**|운영 체제(**CmdExec**)|  
|**4**|Replication Snapshot Agent|  
|**5**|복제 로그 판독기 에이전트|  
|**6**|복제 배포 에이전트|  
|**7**|Replication Merge Agent|  
|**8**|복제 큐 판독기 에이전트|  
|**9**|Analysis Services 쿼리|  
|**10**|Analysis Services 명령|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|  
|**12**|PowerShell 스크립트|  
| &nbsp; | &nbsp; |
  
`[ @subsystem_name = ] 'subsystem_name'` 에 대 한 액세스를 부여할 하위 시스템의 이름입니다. 합니다 **subsystem_name** 됩니다 **sysname**, 기본값은 NULL 사용 하 여 합니다. 어느 *subsystem_id* 하거나 *subsystem_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**ActiveScripting**|ActiveX 스크립트|  
|**CmdExec**|운영 체제(**CmdExec**)|  
|**스냅숏**|Replication Snapshot Agent|  
|**LogReader**|복제 로그 판독기 에이전트|  
|**배포**|복제 배포 에이전트|  
|**병합**|Replication Merge Agent|  
|**QueueReader**|복제 큐 판독기 에이전트|  
|**ANALYSISQUERY**|Analysis Services 쿼리|  
|**ANALYSISCOMMAND**|Analysis Services 명령|  
|**Dts**|SSIS 패키지 실행|  
|**PowerShell**|PowerShell 스크립트|  
| &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Remarks  
 하위 시스템에 프록시 액세스 권한을 부여해도 프록시에 지정된 보안 주체의 권한은 변경되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_grant_proxy_to_subsystem**합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-granting-access-to-a-subsystem-by-id"></a>1\. 하위 시스템에 ID별로 액세스 권한 부여  
 다음 예에서는 ActiveX 스크립팅 하위 시스템에 프록시 `Catalog application proxy` 액세스 권한을 부여합니다.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_id = 2;  
GO  
```  
  
### <a name="b-granting-access-to-a-subsystem-by-name"></a>2\. 하위 시스템에 이름별로 액세스 권한 부여  
 다음 예에서는 SSIS 패키지 실행 하위 시스템에 프록시 `Catalog application proxy` 액세스 권한을 부여합니다.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = N'Catalog application proxy',  
    @subsystem_name = N'Dts' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_revoke_proxy_from_subsystem &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)   
 [sp_add_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_update_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)  
  
  
