---
title: 구독 뷰 형식(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ff1e2566-ac8f-467d-a6d9-12c3f13879b9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 27d0f3f85117812719a642c947fda71b71c4e32c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488008"
---
# <a name="subscription-view-formats-master-data-services"></a>구독 뷰 형식(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  선택한 엔터티 또는 파생 계층을 기준으로, 다음 형식을 구독 뷰에 사용할 수 있습니다.  
  
## <a name="subscription-view-formats"></a>구독 뷰 형식  
  
|이름|Description|  
|----------|-----------------|  
|**리프 멤버**|리프 멤버 및 해당 특성 값을 포함합니다.|  
|**리프 멤버 기록**|리프 멤버 기록 데이터 및 관련 특성 값을 포함합니다. 보기 형식은 느린 변경 차원 유형 4 스타일입니다.|  
|**리프 멤버 SCD 유형 2**|리프 멤버 기록 데이터, 현재 데이터 및 관련 특성 값을 포함합니다. 보기 형식은 느린 변경 차원 유형 2 스타일입니다.|  
|**통합 멤버**|통합 멤버 및 해당 특성 값을 포함합니다.|  
|**통합 멤버 기록**|통합 멤버 기록 데이터 및 관련 특성 값을 포함합니다. 보기 형식은 느린 변경 차원 유형 4 스타일입니다.|  
|**통합 멤버 SCD 유형 2**|통합 멤버 기록 데이터 및 현재 데이터, 관련 특성 값을 포함합니다. 보기 형식은 느린 변경 차원 유형 2 스타일입니다.|  
|**컬렉션 멤버 자격**|컬렉션 목록 및 해당 특성 값을 포함합니다.|  
|**컬렉션**|컬렉션 목록 및 각 멤버를 가중치 및 정렬 순서와 함께 포함합니다.|  
|**컬렉션 멤버 기록**|컬렉션 멤버 기록 데이터 및 관련 특성 값을 포함합니다. 보기 형식은 느린 변경 차원 유형 4 스타일입니다.|  
|**컬렉션 멤버 SCD 유형 2**|컬렉션 멤버 기록 데이터 및 현재 데이터, 관련 특성 값을 포함합니다. 보기 형식은 느린 변경 차원 유형 2 스타일입니다.|  
|**명시적 부모 자식**|엔터티의 명시적 계층 구조를 부모 자식 형식으로 포함합니다.|  
|**명시적 수준**|엔터티의 명시적 계층 구조를 수준 형식으로 포함합니다.|  
|**파생 부모 자식(파생 계층 뷰)**|파생 계층 구조를 부모 자식 형식으로 포함합니다.|  
|**파생 수준(파생 계층 뷰)**|파생 계층 구조를 수준 형식으로 포함합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [개요: 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [구독 뷰를 만들어 데이터 내보내기&#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
  
