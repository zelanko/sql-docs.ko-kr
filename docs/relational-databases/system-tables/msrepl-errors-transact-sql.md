---
title: MSrepl_errors (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3a44dd898b4ec4afcf161e398072edfbc3f6f815
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820083"
---
# <a name="msrepl_errors-transact-sql"></a>MSrepl_errors(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_errors** 테이블에는 확장 된 배포 에이전트 및 병합 에이전트 오류 정보가 포함 된 행이 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|오류 ID입니다.|  
|**time**|**datetime**|오류가 발생한 시간입니다.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|오류 원본 유형 ID입니다.|  
|**source_name**|**nvarchar (100)**|오류 출처의 이름입니다.|  
|**error_code**|**sysname**|오류 코드입니다.|  
|**error_text**|**ntext**|오류 메시지입니다.|  
|**xact_seqno**|**varbinary(16)**|실패한 실행 일괄 처리의 시작 트랜잭션 로그 시퀀스 번호입니다. 배포 에이전트에 의해서만 사용되며 실패한 실행 일괄 처리에 있는 첫 번째 트랜잭션의 트랜잭션 로그 시퀀스 번호입니다.|  
|**command_id**|**int**|실패한 실행 일괄 처리의 명령 ID입니다. 배포 에이전트에 의해서만 사용되며 실패한 실행 일괄 처리에 있는 첫 번째 명령의 명령 ID입니다.|  
|**session_id**|**int**|오류가 발생한 에이전트 세션의 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
