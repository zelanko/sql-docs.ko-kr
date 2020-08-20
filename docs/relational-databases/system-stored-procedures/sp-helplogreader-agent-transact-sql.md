---
description: sp_helplogreader_agent(Transact-SQL)
title: sp_helplogreader_agent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords:
- sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4a5830f73e58925e3935fe554d7467b0582b2b28
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481195"
---
# <a name="sp_helplogreader_agent-transact-sql"></a>sp_helplogreader_agent(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  게시 데이터베이스에 대한 로그 판독기 에이전트 작업의 속성을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|에이전트의 ID입니다.|  
|**name**|**nvarchar (100)**|에이전트의 이름입니다.|  
|**publisher_security_mode**|**smallint**|에이전트가 게시자에 연결할 때 사용하는 보안 모드로서 다음 중 하나일 수 있습니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증|  
|**publisher_login**|**sysname**|게시자에 연결할 때 사용하는 로그인입니다.|  
|**publisher_password**|**nvarchar (524)**|보안상의 이유로 **\*\*\*\*\*\*\*\*\*\*** 항상 값이 반환 됩니다.|  
|**job_id**|**uniqueidentifier**|에이전트 작업의 고유한 ID입니다.|  
|**job_login**|**nvarchar(512)**|로그 판독기 에이전트 실행 되는 Windows 계정으로, *도메인* \\ *사용자 이름*형식으로 반환 됩니다.|  
|**job_password**|**sysname**|보안상의 이유로 **\*\*\*\*\*\*\*\*\*\*** 항상 값이 반환 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helplogreader_agent** 은 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 게시자에서 **sysadmin** 고정 서버 역할의 멤버 또는 게시 데이터베이스에 대 한 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helplogreader_agent**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Transact-sql&#41;sp_addlogreader_agent &#40;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [Transact-sql&#41;sp_changelogreader_agent &#40;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
