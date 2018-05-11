---
title: SQL Server XTP 저장소 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8a9d8604b2ab3388008ba11a5ce038ddbbeffea9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-xtp-storage"></a>SQL Server XTP 저장소
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP 저장소 성능 개체에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 메모리 내 OLTP에 대한 디스크에 있는 저장소와 관련된 카운터가 포함됩니다.  
  
 이 표에서는 **SQL Server XTP 저장소** 카운터에 대해 설명합니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|**Checkpoints Closed**|온라인 에이전트에 의해 닫힌 검사점 수입니다.|  
|**Checkpoints Completed**|오프라인 검사점 스레드에서 처리된 검사점 수입니다.|  
|**Core Merges Completed**|병합 작업자 스레드에서 완료한 코어 병합 수입니다. 이러한 병합은 계속 설치되어 있어야 합니다.|  
|**Merge Policy Evaluations**|서버를 시작한 이후 병합 정책 평가 수입니다.|  
|**Merge Requests Outstanding**|서버를 시작한 이후 해결되지 않은 병합 요청 수입니다.|  
|**Merges Abandoned**|오류로 인해 중단된 병합 수입니다.|  
|**Merges Installed**|설치된 병합 수입니다.|  
|**Total Files Merged**|병합된 총 원본 파일 수입니다. 이 카운트는 병합에서 평균 원본 파일 수를 찾는 데 사용할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
