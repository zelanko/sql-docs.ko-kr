---
title: sp_revoke_proxy_from_subsystem (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c80739e4a888316837b22838b92f6d5919c998d0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261863"
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
 [ **@proxy_id** = ] *id*  
 액세스 권한을 해제할 프록시의 ID입니다. *proxy_id* 은 **int**, 기본값은 NULL입니다. 어느 *proxy_id* 또는 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@proxy_name** = ] **'***proxy_name***'**  
 액세스 권한을 해제할 프록시의 이름입니다. *proxy_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *proxy_id* 또는 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [ **@subsystem_id** = ] *id*  
 액세스 권한을 해제할 하위 시스템의 ID입니다. *subsystem_id* 은 **int**, 기본값은 NULL입니다. 어느 *subsystem_id* 또는 *subsystem_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**2**|ActiveX 스크립트<br /><br /> **\*\* 중요 한 \* \***  The ActiveX 스크립팅 하위 시스템에서 제거 될 예정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이후 버전에서 에이전트 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.|  
|**3**|운영 체제(CmdExec)|  
|**4**|복제 스냅숏 에이전트|  
|**5**|복제 로그 판독기 에이전트|  
|**6**|복제 배포 에이전트|  
|**7**|복제 병합 에이전트|  
|**8**|복제 큐 판독기 에이전트|  
|**9**|Analysis Services 명령|  
|**10**|Analysis Services 쿼리|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|  
|**12**|PowerShell 스크립트|  
  
 [ **@subsystem_name**= ] **'***subsystem_name***'**  
 액세스 권한을 해제할 하위 시스템의 이름입니다. *subsystem_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *subsystem_id* 또는 *subsystem_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|ActiveScripting|ActiveX 스크립트|  
|CmdExec|운영 체제(CmdExec)|  
|스냅숏|복제 스냅숏 에이전트|  
|LogReader|복제 로그 판독기 에이전트|  
|배포|복제 배포 에이전트|  
|병합|복제 병합 에이전트|  
|QueueReader|복제 큐 판독기 에이전트|  
|ANALYSISQUERY|Analysis Services 명령|  
|ANALYSISCOMMAND|Analysis Services 쿼리|  
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|  
|PowerShell|PowerShell 스크립트|  
  
## <a name="remarks"></a>주의  
 하위 시스템 액세스 권한을 해제해도 프록시에 지정된 보안 주체의 권한은 변경되지 않습니다.  
  
> [!NOTE]  
>  프록시를 참조 하는 작업 단계를 확인 하려면 마우스 오른쪽 단추로 클릭는 **프록시** 노드 아래의 **SQL Server 에이전트** microsoft에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 클릭 하 고 **속성**합니다. 에 **프록시 계정 속성** 대화 상자는 **참조** 이 프록시를 참조 하는 모든 작업 단계를 확인할 페이지를 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_revoke_proxy_from_subsystem**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssIS](../../includes/ssis-md.md)]에 대한 `Catalog application proxy` 프록시의 액세스 권한을 해제합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [SQL Server 에이전트 보안 구현](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_grant_proxy_to_subsystem &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
