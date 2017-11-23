---
title: sp_grant_proxy_to_subsystem (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_subsystem_TSQL
- sp_grant_login_to_subsystem
dev_langs: TSQL
helpviewer_keywords: sp_grant_proxy_to_subsystem
ms.assetid: 866aaa27-a1e0-453a-9b1b-af39431ad9c2
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aad59561938886f4fbb1e64dd45e425662c7f4d4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="spgrantproxytosubsystem-transact-sql"></a>sp_grant_proxy_to_subsystem(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하위 시스템에 프록시 액세스 권한을 부여합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_grant_proxy_to_subsystem  
     { [ @proxy_id = ] proxy_id | [ @proxy_name = ] 'proxy_name' },  
     { [ @subsystem_id = ] subsystem_id | [ @subsystem_name = ] 'subsystem_name' }  
```  
  
## <a name="arguments"></a>인수  
 [  **@proxy_id =** ] *id*  
 액세스 권한을 부여할 프록시의 프록시 ID입니다. *proxy_id* 은 **int**, 기본값은 NULL입니다. 어느 *proxy_id* 또는 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [  **@proxy_name =** ] **'***proxy_name***'**  
 액세스 권한을 부여하려는 프록시 이름입니다. *proxy_name* 은 **sysname**, 기본값은 NULL입니다. 어느 *proxy_id* 또는 *proxy_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
 [  **@subsystem_id =** ] *id*  
 액세스 권한을 부여할 하위 시스템의 ID입니다. *subsystem_id* 은 **int**, 기본값은 NULL입니다. 어느 *subsystem_id* 또는 *subsystem_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|설명|  
|-----------|-----------------|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 스크립트<br /><br /> **\*\*중요 한 \* \***  The ActiveX 스크립팅 하위 시스템에서 제거 될 예정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 이후 버전에서 에이전트 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.|  
|**3**|운영 체제(**CmdExec**)|  
|**4**|복제 스냅숏 에이전트|  
|**5**|복제 로그 판독기 에이전트|  
|**6**|복제 배포 에이전트|  
|**7**|복제 병합 에이전트|  
|**8**|복제 큐 판독기 에이전트|  
|**9**|Analysis Services 쿼리|  
|**10**|Analysis Services 명령|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행|  
|**12**|PowerShell 스크립트|  
  
 [  **@subsystem_name =** ] **'***subsystem_name***'**  
 액세스 권한을 부여할 하위 시스템의 이름입니다. **subsystem_name** 은 **sysname**, 기본값은 NULL입니다. 어느 *subsystem_id* 또는 *subsystem_name* 지정 해야 하지만 둘 다 지정할 수 없습니다. 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**ActiveScripting**|ActiveX 스크립트|  
|**CmdExec**|운영 체제(**CmdExec**)|  
|**스냅숏**|복제 스냅숏 에이전트|  
|**LogReader**|복제 로그 판독기 에이전트|  
|**배포**|복제 배포 에이전트|  
|**병합**|복제 병합 에이전트|  
|**QueueReader**|복제 큐 판독기 에이전트|  
|**ANALYSISQUERY**|Analysis Services 쿼리|  
|**ANALYSISCOMMAND**|Analysis Services 명령|  
|**Dts**|SSIS 패키지 실행|  
|**PowerShell**|PowerShell 스크립트|  
  
## <a name="remarks"></a>주의  
 하위 시스템에 프록시 액세스 권한을 부여해도 프록시에 지정된 보안 주체의 권한은 변경되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_grant_proxy_to_subsystem**합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-granting-access-to-a-subsystem-by-id"></a>1. 하위 시스템에 ID별로 액세스 권한 부여  
 다음 예에서는 ActiveX 스크립팅 하위 시스템에 프록시 `Catalog application proxy` 액세스 권한을 부여합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_id = 2;  
GO  
```  
  
### <a name="b-granting-access-to-a-subsystem-by-name"></a>2. 하위 시스템에 이름별로 액세스 권한 부여  
 다음 예에서는 SSIS 패키지 실행 하위 시스템에 프록시 `Catalog application proxy` 액세스 권한을 부여합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = N'Catalog application proxy',  
    @subsystem_name = N'Dts' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 보안 구현](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_revoke_proxy_from_subsystem &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)   
 [sp_add_proxy &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_update_proxy &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)  
  
  
