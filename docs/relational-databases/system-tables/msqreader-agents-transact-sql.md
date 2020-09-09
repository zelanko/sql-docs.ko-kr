---
description: MSqreader_agents(Transact-SQL)
title: MSqreader_agents (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 22792d4f3d2c6d0042f3dcb0af86e63581f5dea7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540300"
---
# <a name="msqreader_agents-transact-sql"></a>MSqreader_agents(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSqreader_agents** 테이블에는 로컬 배포자에서 실행 되는 각 큐 판독기 에이전트에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|큐 판독기 에이전트의 ID입니다.|  
|**name**|**nvarchar (100)**|큐 판독기 에이전트의 이름입니다.|  
|**job_id**|**binary(16)**|**Sysjobs** 테이블의 고유 작업 ID 번호입니다.|  
|**profile_id**|**int**|**MSagent_profiles** 테이블의 프로필 ID입니다.|  
|**job_step_uid**|**uniqueidentifier**|에이전트가 시작되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계의 고유 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
