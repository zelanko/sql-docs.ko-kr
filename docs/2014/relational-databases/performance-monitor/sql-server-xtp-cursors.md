---
title: XTP 커서 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b591aa8e89200ca863b1e8196c383c506401fc3e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151061"
---
# <a name="xtp-cursors"></a>XTP 커서
  XTP 커서 성능 개체에는 내부 XTP 엔진 커서와 관련된 카운터가 포함됩니다. 커서는 XTP 엔진이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 처리하기 위해 사용하는 하위 수준의 기본 구성 요소입니다. 따라서 사용자는 일반적으로 이를 직접 제어하지 않습니다.  
  
 이 테이블에 설명 합니다 **XTP 커서** 카운터입니다.  
  
|카운터|Description|  
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
  
## <a name="see-also"></a>관련 항목  
 [XTP &#40;메모리 내 OLTP&#41; 성능 카운터](../../integration-services/performance/performance-counters.md)  
  
  
