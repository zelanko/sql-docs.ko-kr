---
title: MSagentparameterlist (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSagentparameterlist_TSQL
- MSagentparameterlist
dev_langs:
- TSQL
helpviewer_keywords:
- Msagentparameterlist system table
ms.assetid: 4ea571a0-078d-4e13-95ee-f3d4bbd4dfb2
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf4ba519e2fef4a297e7406689aa33f489c01805
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101261"
---
# <a name="msagentparameterlist-transact-sql"></a>MSagentparameterlist(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSagentparameterlist** 테이블 복제 에이전트 매개 변수 정보를 포함 하며 지정된 된 에이전트 유형에 설정할 수 있는 매개 변수를 지정 하는 데 사용 됩니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**agent_type**|**tinyint**|에이전트의 유형입니다.<br /><br /> **1** = 스냅숏 에이전트입니다.<br /><br /> **2** = 로그 판독기 에이전트입니다.<br /><br /> **3** = 배포 에이전트입니다.<br /><br /> **4** = 병합 에이전트입니다.<br /><br /> **9** = 큐 판독기 에이전트입니다.|  
|**parameter_name**|**sysname**|유효한 에이전트 매개 변수의 이름입니다.|  
|**default_value**|**nvarchar(4000)**|에이전트 매개 변수의 기본값입니다. NULL은 기본값이 없음을 나타냅니다.|  
|**min_value**|**int**|에이전트 매개 변수의 하한을 설정합니다. NULL은 하한이 없음을 나타냅니다.|  
|**max_value**|**int**|에이전트 매개 변수의 상한을 설정합니다. NULL은 상한이 없음을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
