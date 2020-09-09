---
description: MSagent_profiles(Transact-SQL)
title: MSagent_profiles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2f9b44e872ef5175d07a679c330b7662ff9e5bf6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540921"
---
# <a name="msagent_profiles-transact-sql"></a>MSagent_profiles(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSagent_profiles** 테이블에는 정의 된 각 복제 에이전트 프로필에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|프로필 ID입니다.|  
|**profile_name**|**sysname**|에이전트 유형에 대한 고유한 프로필 이름입니다.|  
|**agent_type**|**int**|에이전트의 유형입니다.<br /><br /> **1** = 스냅숏 에이전트<br /><br /> **2** = 로그 판독기 에이전트<br /><br /> **3** = 배포 에이전트<br /><br /> **4** = 병합 에이전트<br /><br /> **9** = 큐 판독기 에이전트|  
|**type**|**int**|프로필의 유형입니다.<br /><br /> **0** = 시스템**1** = 사용자 지정|  
|**description**|**nvarchar (3000)**|프로필에 대한 설명입니다.|  
|**def_profile**|**bit**|해당 프로필이 해당 에이전트 유형에 대한 기본값인지 여부를 지정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
