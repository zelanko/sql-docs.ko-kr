---
title: sp_helpqreader_agent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b1162939039470cdf8e7283950c342e1555c5c78
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824475"
---
# <a name="sp_helpqreader_agent-transact-sql"></a>sp_helpqreader_agent(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  큐 판독기 에이전트의 속성을 반환합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자 또는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>인수  
`[ @frompublisher = ] frompublisher`저장 프로시저가 게시자에서 호출 되는지 또는 배포자에서 호출 되는지 여부를 지정 합니다. *frompublisher* 는 bit 이며 기본값은 0입니다. **1** 은 저장 프로시저가 게시자에서 호출 됨을 의미 하 고 **0** 은 저장 프로시저가 배포자에서 호출 됨을 의미 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|에이전트의 ID입니다.|  
|**name**|**nvarchar (100)**|에이전트의 이름입니다.|  
|**job_id**|**uniqueidentifier**|에이전트 작업의 고유한 ID입니다.|  
|**job_login**|**nvarchar(512)**|배포 에이전트가 실행 되는 Windows 계정으로, *도메인* \\ *사용자 이름*형식으로 반환 됩니다.|  
|**job_password**|**sysname**|보안상의 이유로 **\*\*\*\*\*\*\*\*\*\*** 항상 값이 반환 됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpqreader_agent** 은 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>권한  
 *Frompublisher* 의 값이 **1**인 경우 게시자에서 **sysadmin** 고정 서버 역할의 멤버 또는 게시 데이터베이스에 대 한 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helpqreader_agent**을 실행할 수 있습니다. 그렇지 않으면 배포자에서 **sysadmin** 고정 서버 역할의 멤버 또는 배포 데이터베이스에 대 한 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helpqreader_agent**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
