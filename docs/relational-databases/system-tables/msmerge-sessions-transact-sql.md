---
title: MSmerge_sessions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_sessions
- MSmerge_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_sessions system table
ms.assetid: 09ada8fc-c148-4379-9524-7826b1b0216c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3906e38fbcce8edccf9e0a7bda3be0ed93e110b0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784817"
---
# <a name="msmerge_sessions-transact-sql"></a>MSmerge_sessions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_sessions** 테이블에는 이전 병합 에이전트 작업 세션의 결과가 포함 된 기록 행이 포함 됩니다. 병합 에이전트가 실행될 때마다 이 테이블에 새 행이 추가됩니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|병합 에이전트 작업 세션의 ID입니다.|  
|**agent_id**|**int**|병합 에이전트의 ID입니다.|  
|**start_time**|**datetime**|작업 실행이 시작된 시간입니다.|  
|**end_time**|**datetime**|작업 실행이 완료된 시간입니다.|  
|**duration**|**int**|이 작업 세션의 총 소요 시간(초)입니다.|  
|**delivery_time**|**int**|변경 사항을 일괄적으로 적용하는 데 걸린 시간(초)입니다.|  
|**upload_time**|**int**|변경 사항을 게시자에 업로드하는 데 걸린 시간(초)입니다.|  
|**download_time**|**int**|변경 사항을 구독자에 다운로드하는 데 걸린 시간(초)입니다.|  
|**delivery_rate**|**float**|초당 배달된 평균 명령 수입니다.|  
|**time_remaining**|**int**|활성 세션에 남은 예상 시간(초)입니다.|  
|**percent_complete**|**decimal**|활성 세션에 이미 배달된 전체 변경 사항의 예상 백분율입니다.|  
|**upload_inserts**|**int**|게시자에서 적용된 삽입 수입니다.|  
|**upload_updates**|**int**|게시자에서 적용된 업데이트 수입니다.|  
|**upload_deletes**|**int**|게시자에서 적용된 삭제 수입니다.|  
|**upload_conflicts**|**int**|게시자에서 변경 사항을 적용하는 동안 발생한 충돌 수입니다.|  
|**upload_conflicts_resolved**|**int**|게시자에서 변경 사항을 적용하는 중 일어나 해결된 충돌 수입니다.|  
|**upload_rows_retried**|**int**|다시 시도하여 게시자에 업로드된 행 수입니다.|  
|**download_inserts**|**int**|구독자에서 적용된 삽입 수입니다.|  
|**download_updates**|**int**|구독자에서 적용된 업데이트 수입니다.|  
|**download_deletes**|**int**|구독자에서 적용된 삭제 수입니다.|  
|**download_conflicts**|**int**|구독자에서 변경 사항을 적용하는 동안 발생한 충돌 수입니다.|  
|**download_conflicts_resolved**|**int**|구독자에서 변경 사항을 적용하는 중 일어나 해결된 충돌 수입니다.|  
|**download_rows_retried**|**int**|다시 시도하여 구독자에 다운로드된 행 수입니다.|  
|**schema_changes**|**int**|세션 중 적용된 스키마 변경의 수입니다.|  
|**metadata_rows_cleanedup**|**int**|세션 중 정리된 메타데이터의 행 수입니다.|  
|**runstatus**|**int**|실행 상태는 다음과 같습니다.<br /><br /> **1** = 시작<br /><br /> **2** = 성공<br /><br /> **3** = 진행 중<br /><br /> **4** = 유휴 상태입니다.<br /><br /> **5** = 다시 시도<br /><br /> **6** = 실패|  
|**estimated_upload_changes**|**int**|게시자에서 적용되어야 하는 예상 변경 수입니다.|  
|**estimated_download_changes**|**int**|구독자에서 적용되어야 하는 예상 변경 수입니다.|  
|**connection_type**|**int**|업로드 중 사용된 연결은 다음과 같습니다.<br /><br /> **1** = lan (local area network).<br /><br /> **2** = 전화 접속 네트워크 연결<br /><br /> **3** = 웹 동기화.|  
|**timestamp**|**timestamp**|이 테이블의 타임스탬프 열입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
