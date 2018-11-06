---
title: SQL Server XTP 커서 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance-monitor
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a3e77b221937cba536d888d9a1b1e1c2c5af310a
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51031050"
---
# <a name="sql-server-xtp-cursors"></a>SQL Server XTP 커서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP 커서 성능 개체에는 내부 메모리 내 OLTP 엔진 커서와 관련된 카운터가 포함됩니다. 커서는 메모리 내 OLTP 엔진이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 처리하기 위해 사용하는 하위 수준의 기본 구성 요소입니다. 따라서 사용자는 일반적으로 이를 직접 제어하지 않습니다.  
  
 이 표에서는 **SQL Server XTP 커서** 카운터에 대해 설명합니다.  
  
|카운터|설명|  
|-------------|-----------------|  
|**Cursor deletes/sec**|초당 커서 삭제 수입니다(평균).|  
|**Cursor inserts/sec**|초당 커서 삽입 수입니다(평균).|  
|**Cursor scans started /sec**|초당 시작된 커서 검사 수입니다(평균).|  
|**Cursor unique violations/sec**|초당 고유 제약 조건 위반 수입니다(평균).|  
|**Cursor updates/sec**|초당 커서 업데이트 수입니다(평균).|  
|**Cursor write   conflicts/sec**|동일 행 버전에 대한 초당 쓰기-쓰기 충돌 수입니다(평균).|  
|**Dusty corner scan retries/sec (user-issued)**|사용자의 전체 테이블 검사에 의해 실행된 불량 영역 청소(dusty corner sweeps) 중 발생한 초당 검색 재시도 횟수입니다(평균). 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|  
|**Expired rows removed/sec**|커서에 의해 제거된 만료된 초당 행 수입니다(평균).|  
|**Expired rows touched/sec**|커서에 의해 처리된 만료된 초당 행 수입니다(평균).|  
|**Rows returned/sec**|커서에 의해 반환된 초당 행 수입니다(평균).|  
|**Rows touched/sec**|커서에 의해 처리된 초당 행 수입니다(평균).|  
|**Tentatively-deleted rows touched/sec**|커서에 의해 처리된 만료되는 초당 행 수입니다(평균). 만료되는 행은 행을 삭제한 트랜잭션이 여전히 활성 상태인 경우의 행을 의미합니다(즉, 아직 커밋되거나 중단되지 않음).|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
