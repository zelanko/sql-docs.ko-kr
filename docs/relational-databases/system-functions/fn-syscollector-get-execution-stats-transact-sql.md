---
title: fn_syscollector_get_execution_stats (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_stats
- fn_syscollector_get_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_stats function
ms.assetid: 793ad72c-a992-4a8d-8584-bcb6b3b476f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 71a070de7c74d353be395628566c0bd3f63fd99a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042739"
---
# <a name="fn_syscollector_get_execution_stats-transact-sql"></a>fn_syscollector_get_execution_stats(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  패키지의 데이터 흐름 태스크에서 기록한 오류 행 수를 포함하여 컬렉션 집합 또는 패키지에 대한 자세한 통계를 반환합니다. 데이터 흐름 태스크는 데이터를 처리하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소입니다. 이 데이터는 관계형 형식으로 되어 있으므로 행으로 이루어진 입력 및 출력 데이터 세트을 가집니다.  
  
 이 통계는 syscollector_execution_stats 뷰의 항목에서 계산됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_syscollector_get_execution_stats ( log_id )  
```  
  
## <a name="arguments"></a>인수  
 *log_id*  
 실행 로그의 고유한 로컬 식별자입니다. *log_id* 됩니다 **int**합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|avg_row_count_in|**int**|패키지의 데이터 흐름 태스크에 들어간 평균 행 수입니다.<br /><br /> 참고: 데이터 흐름 태스크는 데이터를 처리하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소입니다. 이 데이터는 관계형 형식으로 되어 있으므로 행으로 이루어진 입력 데이터 세트을 가집니다. 이는 태스크에 들어간 행의 수입니다. 데이터는 변환된 후에 행으로 이루어진 결과 집합으로 출력됩니다. 데이터 흐름 태스크는 데이터를 변환하고 행으로 이루어진 결과 집합을 출력합니다. 이 출력은 태스크에서 빠져나간 행의 수입니다.|  
|min_row_count_in|**int**|패키지의 데이터 흐름 태스크에 들어간 최소 행 수입니다.|  
|max_row_count_in|**int**|패키지의 데이터 흐름 태스크에 들어간 최대 행 수입니다.|  
|avg_row_count_out|**int**|패키지의 데이터 흐름 태스크에서 빠져나간 평균 행 수입니다.|  
|min_row_count_out|**int**|패키지의 데이터 흐름 태스크에서 빠져나간 최소 행 수입니다.|  
|max_row_count_out|**int**|패키지의 데이터 흐름 태스크에서 빠져나간 최대 행 수입니다.|  
|avg_duration|**int**|패키지의 데이터 흐름 구성 요소에 소요된 평균 시간(밀리초)입니다.|  
|min_duration|**int**|패키지의 데이터 흐름 구성 요소에 소요된 최소 시간(밀리초)입니다.|  
|max_duration|**int**|패키지의 데이터 흐름 구성 요소에 소요된 최대 시간(밀리초)입니다.|  
  
## <a name="permissions"></a>사용 권한  
 에 대 한 SELECT가 필요 **dc_operator**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [syscollector_execution_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
