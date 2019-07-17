---
title: MSqreader_agents (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSqreader_agents_TSQL
- MSqreader_agents
dev_langs:
- TSQL
helpviewer_keywords:
- MSqreader_agents system table
ms.assetid: dfa1f45e-c531-4385-a097-0a9edd1d7eab
author: stevestein
ms.author: sstein
ms.openlocfilehash: d032552769c32d691a526456cba68aec9ac397e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032568"
---
# <a name="msqreaderagents-transact-sql"></a>MSqreader_agents(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSqreader_agents** 테이블은 로컬 배포자에서 실행 중인 각 큐 판독기 에이전트에 대해 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|큐 판독기 에이전트의 ID입니다.|  
|**name**|**nvarchar(100)**|큐 판독기 에이전트의 이름입니다.|  
|**job_id**|**binary(16)**|고유한 작업 ID 번호 **sysjobs** 테이블입니다.|  
|**profile_id**|**int**|프로필 ID를 **MSagent_profiles** 테이블입니다.|  
|**job_step_uid**|**uniqueidentifier**|에이전트가 시작되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계의 고유 ID입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
