---
title: sp_help_proxy (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f7053bfc6ccbca71783d0bbcdb8b9b5544f9d20
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpproxy-transact-sql"></a>sp_help_proxy(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하나 이상의 프록시에 대한 정보를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>인수  
 [ **@proxy_id** = ] *id*  
 정보를 나열할 프록시의 프록시 ID입니다. *proxy_id* 은 **int**, 기본값은 NULL입니다. 중 하나는 *id* 또는 *proxy_name* 지정할 수 있습니다.  
  
 [ **@proxy_name** = ] **'***proxy_name***'**  
 정보를 나열할 프록시의 이름입니다. *proxy_name* 은 **sysname**, 기본값은 NULL입니다. 중 하나는 *id* 또는 *proxy_name* 지정할 수 있습니다.  
  
 [ **@subsystem_name** =] '*subsystem_name*'  
 프록시를 나열할 하위 시스템의 이름입니다. *subsystem_name* 은 **sysname**, 기본값은 NULL입니다. 때 *subsystem_name* 지정 된 *이름* 도 지정 해야 합니다.  
  
 다음 표에서는 각 하위 시스템에 대한 값을 나열합니다.  
  
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
|Dts|SSIS 패키지 실행|  
|PowerShell|PowerShell 스크립트|  
  
 [ **@name** =] '*이름*'  
 프록시를 나열할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름입니다. 이름은 **nvarchar (256)**, 기본값은 NULL입니다. 때 *이름* 지정 된 *subsystem_name* 도 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|프록시 ID입니다.|  
|**name**|**sysname**|프록시 이름입니다.|  
|**credential_identity**|**sysname**|프록시와 연관된 자격 증명의 Microsoft Windows 도메인 이름 및 사용자 이름입니다.|  
|**enabled**|**tinyint**|이 프록시가 사용되는지 여부입니다. { **0** = 사용 안 함, **1** = 사용}|  
|**설명**|**nvarchar(1024)**|이 프록시에 대한 설명입니다.|  
|**user_sid**|**varbinary(85)**|이 프록시에 대한 Windows 사용자의 Windows 보안 ID입니다.|  
|**credential_id**|**int**|이 프록시와 연관된 자격 증명의 식별자입니다.|  
|**credential_identity_exists**|**int**|credential_identity가 있는지 여부입니다. { 0 = 없음, 1 = 있음 }|  
  
## <a name="remarks"></a>주의  
 매개 변수를 제공 **sp_help_proxy** 인스턴스의 모든 프록시에 대 한 정보를 나열 합니다.  
  
 지정된 된 하위 시스템에 있는 프록시 로그인을 사용할 수를 확인 하려면 지정 *이름* 및 *subsystem_name*합니다. 이러한 인수를 제공 하는 경우 **sp_help_proxy** 프록시에 액세스 하 고 있는 수에 사용할 수 지정한 하위 시스템 지정 된 로그인을 나열 합니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 **msdb** 데이터베이스의 **SQLAgentOperatorRole** 고정 데이터베이스 역할을 부여 받아야 합니다.  
  
 에 대 한 내용은 **SQLAgentOperatorRole**, 참조 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)합니다.  
  
> [!NOTE]  
>  **credential_identity** 및 **user_sid** 열에 정보만 반환 됩니다 경우의 결과 집합의 멤버 **sysadmin** 이 저장된 프로시저를 실행 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-listing-information-for-all-proxies"></a>1. 모든 프록시에 대한 정보 나열  
 다음 예에서는 인스턴스의 모든 프록시에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>2. 특정 작업에 대한 정보 나열  
 다음 예에서는 `Catalog application proxy`라는 프록시에 대한 정보를 나열합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 에이전트 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
