---
title: MSmerge_articlehistory (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_articlehistory
- MSmerge_articlehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_articlehistory system table
ms.assetid: 2870e7ea-dbec-4636-9171-c2cee96018ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 86f2432073b580dfa59b92683d4401cb53296b02
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889883"
---
# <a name="msmerge_articlehistory-transact-sql"></a>MSmerge_articlehistory(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_articlehistory** 테이블은 병합 에이전트 동기화 세션 중에 아티클의 변경 내용을 추적 하 고 변경 된 각 아티클에 대해 한 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|[MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) 시스템 테이블에 있는 병합 에이전트 작업 세션의 ID입니다.|  
|**phase_id**|**int**|동기화 세션의 단계이며 다음 중 하나일 수 있습니다.<br /><br /> **1** = 업로드<br /><br /> **2** = 다운로드<br /><br /> **4** = 정리 합니다.<br /><br /> **5** = 종료<br /><br /> **6** = 스키마 변경<br /><br /> **7** = BCP|  
|**article_name**|**sysname**|변경된 아티클의 이름입니다.|  
|**start_time**|**datetime**|에이전트가 아티클 처리를 시작한 시간입니다.|  
|**duration**|**int**|에이전트가 아티클을 처리하는 데 걸린 시간(초)입니다.|  
|**클립보드**|**int**|동기화 중에 특정 아티클에 적용된 삽입 횟수입니다. 이 값은 동기화 프로세스 중에 증가하며 마지막 값은 전체 값을 나타냅니다.|  
|**업데이트**|**int**|동기화 중에 특정 아티클에 적용된 업데이트 횟수입니다. 이 값은 동기화 프로세스 중에 증가하며 마지막 값은 전체 값을 나타냅니다.|  
|**되며**|**int**|동기화 중에 특정 아티클에 적용된 삭제 횟수입니다. 이 값은 동기화 프로세스 중에 증가하며 마지막 값은 전체 값을 나타냅니다.|  
|**충돌**|**int**|동기화 중에 발생한 충돌 횟수입니다. 이 값은 동기화 프로세스 중에 증가하며 마지막 값은 전체 값을 나타냅니다.|  
|**conflicts_resolved**|**int**|동기화 중에 발생하여 해결된 충돌 횟수입니다. 이 값은 동기화 프로세스 중에 증가하며 마지막 값은 전체 값을 나타냅니다.|  
|**rows_retried**|**int**|동기화 중에 실패하여 다시 시도한 행의 수입니다. 이 값은 동기화 프로세스 중에 증가하며 마지막 값은 전체 값을 나타냅니다.|  
|**percent_complete**|**decimal**|병합 에이전트가 세션 중에 해당 아티클에 사용한 전체 동기화 시간의 백분율입니다. 세션을 완료할 때까지 이 값은 NULL입니다.|  
|**estimated_changes**|**int**|아티클에 적용해야 하는 행 변경 횟수의 추정치입니다.|  
|**relative_cost**|**decimal**|현재 아티클의 변경 사항을 적용하는 데 사용한 시간 대비 전체 세션의 총 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
