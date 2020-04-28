---
title: sp_revoke_proxy_from_subsystem (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 8901c46c5654b6c633e03d62e8eaec2a3e903e02
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68022273"
---
# <a name="sp_revoke_proxy_from_subsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  프록시의 하위 시스템 액세스 권한을 해제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @proxy_id = ] id`액세스 권한을 취소할 프록시의 프록시 id입니다. *Proxy_id* 은 **int**이며 기본값은 NULL입니다. *Proxy_id* 또는 *proxy_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @proxy_name = ] 'proxy_name'`액세스 권한을 취소할 프록시의 이름입니다. *Proxy_name* 는 **sysname**이며 기본값은 NULL입니다. *Proxy_id* 또는 *proxy_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다.  
  
`[ @subsystem_id = ] id`액세스 권한을 취소할 하위 시스템의 id 번호입니다. *Subsystem_id* 은 **int**이며 기본값은 NULL입니다. *Subsystem_id* 또는 *subsystem_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**2**|ActiveX 스크립트<br /><br /> ** \* 중요 \* \* ** [!INCLUDE[msCoName](../../includes/msconame-md.md)]의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이후 버전에서는 에이전트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ActiveX 스크립팅 하위 시스템이 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요.|  
|**3**|운영 체제(CmdExec)|  
|**4**|Replication Snapshot Agent|  
|**5**|복제 로그 판독기 에이전트|  
|**6**|복제 배포 에이전트|  
|**7**|Replication Merge Agent|  
|**20cm(8**|복제 큐 판독기 에이전트|  
|**9**|Analysis Services 명령|  
|**10**|Analysis Services 쿼리|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|  
|**12**|PowerShell 스크립트|  
  
`[ @subsystem_name = ] 'subsystem_name'`액세스 권한을 취소할 하위 시스템의 이름입니다. *Subsystem_name* 는 **sysname**이며 기본값은 NULL입니다. *Subsystem_id* 또는 *subsystem_name* 를 지정 해야 하지만 둘 다 지정할 수는 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|ActiveScripting|ActiveX 스크립트|  
|CmdExec|운영 체제(CmdExec)|  
|스냅샷|Replication Snapshot Agent|  
|LogReader|복제 로그 판독기 에이전트|  
|배포|복제 배포 에이전트|  
|병합|Replication Merge Agent|  
|QueueReader|복제 큐 판독기 에이전트|  
|ANALYSISQUERY|Analysis Services 명령|  
|ANALYSISCOMMAND|Analysis Services 쿼리|  
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|  
|PowerShell|PowerShell 스크립트|  
  
## <a name="remarks"></a>설명  
 하위 시스템 액세스 권한을 해제해도 프록시에 지정된 보안 주체의 권한은 변경되지 않습니다.  
  
> [!NOTE]  
>  프록시를 참조 하는 작업 단계를 확인 하려면 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **SQL Server 에이전트** 에서 **프록시** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다. **프록시 계정 속성** 대화 상자에서 **참조** 페이지를 선택 하 여이 프록시를 참조 하는 모든 작업 단계를 확인 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_revoke_proxy_from_subsystem**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssIS](../../includes/ssis-md.md)]에 대한 `Catalog application proxy` 프록시의 액세스 권한을 해제합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;저장 프로시저 SQL Server 에이전트](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)   
 [Transact-sql&#41;sp_grant_proxy_to_subsystem &#40;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
