---
title: MSrepl_errors (Transact SQL) | Microsoft Docs
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
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 48346fe7e8beb4c1885507de48d14889bd6ffee6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005400"
---
# <a name="msreplerrors-transact-sql"></a>MSrepl_errors(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_errors** 테이블 확장된 배포 에이전트 및 병합 에이전트 실패 정보가 있는 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|오류 ID입니다.|  
|**time**|**datetime**|오류가 발생한 시간입니다.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|오류 원본 유형 ID입니다.|  
|**source_name**|**nvarchar(100)**|오류 출처의 이름입니다.|  
|**error_code**|**sysname**|오류 코드입니다.|  
|**error_text**|**ntext**|오류 메시지.|  
|**xact_seqno**|**varbinary(16)**|실패한 실행 일괄 처리의 시작 트랜잭션 로그 시퀀스 번호입니다. 배포 에이전트에 의해서만 사용되며 실패한 실행 일괄 처리에 있는 첫 번째 트랜잭션의 트랜잭션 로그 시퀀스 번호입니다.|  
|**command_id**|**int**|실패한 실행 일괄 처리의 명령 ID입니다. 배포 에이전트에 의해서만 사용되며 실패한 실행 일괄 처리에 있는 첫 번째 명령의 명령 ID입니다.|  
|**session_id**|**int**|오류가 발생한 에이전트 세션의 ID입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
