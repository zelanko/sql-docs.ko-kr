---
title: XTP 저장소 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: 3
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 897a3a2e9e3cc592281be87593aa6356ce474c56
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172626"
---
# <a name="xtp-storage"></a>XTP 저장소
  XTP 저장소 성능 개체에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 XTP 저장소와 관련된 카운터가 포함되어 있습니다.  
  
 이 표에서는 **XTP 저장소** 카운터에 대해 설명합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [XTP &#40;메모리 내 OLTP&#41; 성능 카운터](../../integration-services/performance/performance-counters.md)  
  
  