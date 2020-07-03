---
title: sp_MSchange_logreader_agent_properties (T-sql)
description: SQL Server 복제 토폴로지의 로그 판독기 에이전트 속성을 변경 하는 데 사용 되는 sp_MSchange_logreader_agent_properties 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords:
- sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 76a3f657600ed2f8f545dd95c1ba85fa682d51c4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891561"
---
# <a name="sp_mschange_logreader_agent_properties-transact-sql"></a>sp_MSchange_logreader_agent_properties(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이상 버전의 배포자에서 실행 되는 로그 판독기 에이전트 작업의 속성을 변경 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . 이 저장 프로시저는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 인스턴스에서 게시자가 실행될 때 속성을 변경하는 데 사용됩니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_security_mode = ] publisher_security_mode`게시자에 연결할 때 에이전트가 사용 하는 보안 모드입니다. *publisher_security_mode* 은 **smallint**이며 기본값은 없습니다.  
  
 **0** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 합니다.  
  
 **1** 은 Windows 인증을 지정 합니다.  
  
`[ @publisher_login = ] 'publisher_login'`게시자에 연결할 때 사용 되는 로그인입니다. *publisher_login* 는 **sysname**이며 기본값은 없습니다. *publisher_security_mode* **0**인 경우 *publisher_login* 를 지정 해야 합니다. *PUBLISHER_LOGIN* NULL이 고 *publisher_security_mode* 가 **1**이면 게시자에 연결할 때 *job_login* 에 지정 된 Windows 계정이 사용 됩니다.  
  
`[ @publisher_password = ] 'publisher_password'`게시자에 연결할 때 사용 되는 암호입니다. *publisher_password* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @job_login = ] 'job_login'`에이전트가 실행 되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)** 이며 기본값은 없습니다. *이를 변경할* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 수 없습니다. *게시자.*  
  
`[ @job_password = ] 'job_password'`에이전트를 실행 하는 Windows 계정의 암호입니다. *job_password* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_type = ] 'publisher_type'`인스턴스에서 게시자가 실행 되 고 있지 않을 때 게시자 유형을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher_type* 는 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**MSSQLSERVER**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정합니다.|  
|**ORACLE**|표준 Oracle 게시자를 지정합니다.|  
|**ORACLE GATEWAY**|Oracle Gateway 게시자를 지정합니다.|  
  
 Oracle 게시자와 Oracle Gateway 게시자 간의 차이점에 대 한 자세한 내용은 [Oracle 게시 개요](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)를 참조 하세요.  
  
## <a name="remarks"></a>설명  
 **sp_MSchange_logreader_agent_properties** 은 트랜잭션 복제에 사용 됩니다.  
  
 **Sp_MSchange_logreader_agent_properties**를 실행 하는 경우 모든 매개 변수를 지정 해야 합니다. [Transact-sql&#41;&#40;sp_helplogreader_agent](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) 를 실행 하 여 로그 판독기 에이전트 작업의 현재 속성을 반환 합니다.  
  
 에이전트 로그인 또는 암호를 변경한 후 에이전트를 중지하고 다시 시작해야 변경 내용이 적용됩니다.  
  
 게시자가 이상 버전의 인스턴스에서 실행 되는 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md) 를 사용 하 여 로그 판독기 에이전트 속성을 변경 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버만 **sp_MSchange_logreader_agent_properties**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
