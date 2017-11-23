---
title: sp_MSchange_logreader_agent_properties (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords: sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea342cad83b587382ca9e25141facd613263a20e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spmschangelogreaderagentproperties-transact-sql"></a>sp_MSchange_logreader_agent_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  실행 되는 로그 판독기 에이전트 작업의 속성을 변경는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 이상 버전의 배포자입니다. 이 저장 프로시저는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 인스턴스에서 게시자가 실행될 때 속성을 변경하는 데 사용됩니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_MSchange_logreader_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>인수  
 [  **@publisher**  =] **'***게시자***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_security_mode** =] *publisher_security_mode*  
 게시자에 연결할 때 에이전트가 사용하는 보안 모드입니다. *publisher_security_mode* 은 **smallint**, 기본값은 없습니다.  
  
 **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.  
  
 **1** Windows 인증을 지정 합니다.  
  
 [  **@publisher_login** =] **'***publisher_login***'**  
 게시자에 연결할 때 사용하는 로그인입니다. *publisher_login* 은 **sysname**, 기본값은 없습니다. *publisher_login* 지정 해야 *publisher_security_mode* 은 **0**합니다. 경우 *publisher_login* null 및 *publisher_security_mode* 은 **1**에 지정 된 Windows 계정이 *job_login* 사용 됩니다 게시자에 연결 합니다.  
  
 [  **@publisher_password** =] **'***publisher_password***'**  
 게시자에 연결할 때 사용하는 암호입니다. *publisher_password* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@job_login** =] **'***job_login***'**  
 에이전트 실행에 사용되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)**, 기본값은 없습니다. *이 이외에 대 한 변경할 수 없습니다* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *게시자입니다.*  
  
 [  **@job_password** =] **'***job_password***'**  
 에이전트 실행에 사용되는 Windows 계정의 암호입니다. *job_password* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_type** =] **'***publisher_type***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 게시자가 실행되고 있지 않을 때 게시자 유형을 지정합니다. *publisher_type* 은 **sysname**, 다음 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정합니다.|  
|**ORACLE**|표준 Oracle 게시자를 지정합니다.|  
|**ORACLE GATEWAY**|Oracle Gateway 게시자를 지정합니다.|  
  
 Oracle 게시자와 Oracle Gateway 게시자의 차이점에 대 한 자세한 내용은 참조 [Publishing](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)합니다.  
  
## <a name="remarks"></a>주의  
 **sp_MSchange_logreader_agent_properties** 트랜잭션 복제에 사용 됩니다.  
  
 실행할 때는 모든 매개 변수를 지정 해야 **sp_MSchange_logreader_agent_properties**합니다. 실행 [sp_helplogreader_agent &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) 로그 판독기 에이전트 작업의 현재 속성을 반환 합니다.  
  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
 게시자의 인스턴스에서 실행 하는 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 사용할지 또는 [sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md) 로그 판독기 에이전트의 속성을 변경 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할이 배포자에서 실행할 수 있는 **sp_MSchange_logreader_agent_properties**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
