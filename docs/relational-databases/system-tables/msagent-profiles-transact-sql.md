---
title: MSagent_profiles (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c7e5033c5fd66141a7d6bc656f33dd5720bae016
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47700401"
---
# <a name="msagentprofiles-transact-sql"></a>MSagent_profiles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSagent_profiles** 각 정의 된 복제 에이전트 프로필에 대해 하나의 행을 포함 하는 테이블입니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|프로필 ID입니다.|  
|**profile_name**|**sysname**|에이전트 유형에 대한 고유한 프로필 이름입니다.|  
|**agent_type**|**int**|에이전트의 유형입니다.<br /><br /> **1** = 스냅숏 에이전트<br /><br /> **2** = 로그 판독기 에이전트<br /><br /> **3** = 배포 에이전트<br /><br /> **4** = 병합 에이전트<br /><br /> **9** = 큐 판독기 에이전트|  
|**type**|**int**|프로필의 유형입니다.<br /><br /> **0** = 시스템**1** = 사용자 지정|  
|**description**|**nvarchar(3000)**|프로필에 대한 설명입니다.|  
|**def_profile**|**bit**|해당 프로필이 해당 에이전트 유형에 대한 기본값인지 여부를 지정합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
