---
title: MSmerge_replinfo (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a84027787de68ec407df91ef294ed1787739e6f9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784801"
---
# <a name="msmerge_replinfo-transact-sql"></a>MSmerge_replinfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_replinfo** 테이블에는 각 구독에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 구독에 대한 정보를 추적합니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|복제에 대한 고유 ID입니다.|  
|**use_interactive_resolver**|**bit**|조정하는 동안 대화형 해결 프로그램을 사용할지 여부를 지정합니다.<br /><br /> **0** = 대화형 해결 프로그램을 사용 하지 않습니다.<br /><br /> **1** = 대화형 해결 프로그램을 사용 합니다.|  
|**validation_level**|**int**|구독에서 실행할 유효성 검사의 유형입니다. 지정한 유효성 검사 수준은 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **0** = 유효성 검사 안 함<br /><br /> **1** = 행 개수만 유효성 검사입니다.<br /><br /> **2** = 행 개수 및 체크섬 유효성 검사를 수행 합니다.<br /><br /> **3** = 행 개수 및 이진 체크섬 유효성 검사|  
|**resync_gen**|**bigint**|구독을 다시 동기화하는 데 사용되는 생성 번호입니다. **-1** 값은 구독이 다시 동기화 하도록 표시 되지 않았음을 나타냅니다.|  
|**login_name**|**sysname**|구독을 만든 사용자의 이름입니다.|  
|**hostname**|**sysname**|구독에 대한 파티션을 생성할 때 매개 변수가 있는 행 필터에서 사용되는 값입니다.|  
|**merge_jobid**|**binary(16)**|이 구독에 대한 병합 작업 ID입니다.|  
|**sync_info**|**int**|내부적으로만 사용됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
