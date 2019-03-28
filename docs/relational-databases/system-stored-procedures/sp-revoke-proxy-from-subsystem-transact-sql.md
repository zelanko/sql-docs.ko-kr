---
title: sp_revoke_proxy_from_subsystem (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 4079a6afda1f303369a2d8b9defc8bbeb3c4608d
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527236"
---
# <a name="sprevokeproxyfromsubsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  프록시의 하위 시스템 액세스 권한을 해제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @proxy_id = ] id` 액세스 권한을 해제할 프록시의 프록시 id. 합니다 *proxy_id* 됩니다 **int**, 기본값은 NULL 사용 하 여 합니다. 어느 *proxy_id* 하거나 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @proxy_name = ] 'proxy_name'` 액세스 권한을 해제할 프록시의 이름입니다. 합니다 *proxy_name* 됩니다 **sysname**, 기본값은 NULL 사용 하 여 합니다. 어느 *proxy_id* 하거나 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
`[ @subsystem_id = ] id` 액세스 권한을 해제할 하위 시스템의 id. 합니다 *subsystem_id* 됩니다 **int**, 기본값은 NULL 사용 하 여 합니다. 어느 *subsystem_id* 하거나 *subsystem_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**2**|ActiveX 스크립트<br /><br /> **\*\* 중요 \* \***  ActiveX 스크립팅 하위 시스템에서 제거 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이후 버전에서 에이전트 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.|  
|**3**|운영 체제(CmdExec)|  
|**4**|복제 스냅숏 에이전트|  
|**5**|복제 로그 판독기 에이전트|  
|**6**|복제 배포 에이전트|  
|**7**|Replication Merge Agent|  
|**8**|복제 큐 판독기 에이전트|  
|**9**|Analysis Services 명령|  
|**10**|Analysis Services 쿼리|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|  
|**12**|PowerShell 스크립트|  
  
`[ @subsystem_name = ] 'subsystem_name'` 액세스 권한을 해제할 하위 시스템의 이름입니다. 합니다 *subsystem_name* 됩니다 **sysname**, 기본값은 NULL 사용 하 여 합니다. 어느 *subsystem_id* 하거나 *subsystem_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|ActiveScripting|ActiveX 스크립트|  
|CmdExec|운영 체제(CmdExec)|  
|스냅숏|복제 스냅숏 에이전트|  
|LogReader|복제 로그 판독기 에이전트|  
|배포|복제 배포 에이전트|  
|병합|Replication Merge Agent|  
|QueueReader|복제 큐 판독기 에이전트|  
|ANALYSISQUERY|Analysis Services 명령|  
|ANALYSISCOMMAND|Analysis Services 쿼리|  
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|  
|PowerShell|PowerShell 스크립트|  
  
## <a name="remarks"></a>Remarks  
 하위 시스템 액세스 권한을 해제해도 프록시에 지정된 보안 주체의 권한은 변경되지 않습니다.  
  
> [!NOTE]  
>  프록시를 참조 하는 작업 단계를 확인 하려면 마우스 오른쪽 단추로 클릭 합니다 **프록시** 노드 아래의 **SQL Server 에이전트** microsoft에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 클릭 하 고 **속성**. 에 **프록시 계정 속성** 대화 상자를 선택 합니다 **참조** 이 프록시를 참조 하는 모든 작업 단계를 보려면 페이지.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_revoke_proxy_from_subsystem**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssIS](../../includes/ssis-md.md)]에 대한 `Catalog application proxy` 프록시의 액세스 권한을 해제합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_grant_proxy_to_subsystem &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
