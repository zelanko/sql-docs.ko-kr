---
title: 일반 (저장소 옵션 대화 상자) (Analysis Services 다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.storage.f1
ms.assetid: ee1fac79-ae15-4c3c-9a98-33db04388817
author: minewiskan
ms.author: owend
ms.openlocfilehash: f67e3f7a3c9d84c8095286707c3dd6ce2c22c3bd
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544410"
---
# <a name="general-storage-options-dialog-box-analysis-services---multidimensional-data"></a>일반(스토리지 옵션 대화 상자)(Analysis Services - 다차원 데이터)
  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 **스토리지 옵션** 대화 상자의 **일반** 탭을 사용하여 차원, 큐브, 측정값 그룹 또는 파티션에 대해 스토리지 모드와 자동 관리 캐싱 설정을 지정할 수 있습니다.  
  
> [!NOTE]  
>  이러한 설정을 수정하려면 스토리지 모드와 자동 관리 캐싱 기능에 대해 잘 알고 있어야 합니다. 자세한 내용은 [자동 관리 캐싱&#40;파티션&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
  
|용어|정의|  
|----------|----------------|  
|**스토리지 모드**|개체에 사용할 스토리지 모드를 선택합니다.<br /><br /> **MOLAP**<br /> 개체가 MOLAP(다차원 OLAP) 스토리지를 사용합니다.<br /><br /> **HOLAP**<br /> 개체가 HOLAP(하이브리드 OLAP) 스토리지를 사용합니다.<br /><br /> **ROLAP**<br /> 개체가 ROLAP(관계형 OLAP) 스토리지를 사용합니다.|  
|**자동 관리 캐싱을 설정합니다.**|자동 관리 캐싱을 설정합니다.<br /><br /> 참고: 이 옵션을 선택하지 않으면 **스토리지 모드**를 제외한 모든 옵션을 사용할 수 없습니다.|  
|**데이터가 변경되면 캐시 업데이트**|**알림** 탭에서 선택한 알림 방법을 사용하여 알림을 받을 때마다 개체에 대한 MOLAP 이미지를 업데이트할 수 있습니다. **알림** 탭에 대한 자세한 내용은 [알림&#40;스토리지 옵션 대화 상자&#41;&#40;Analysis Services - 다차원 데이터&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)을 참조하세요.<br /><br /> 참고: 이 옵션은 **자동 관리 캐싱 설정** 을 선택한 경우에만 사용할 수 있습니다.|  
|**대기 간격**|자동 관리 캐싱에서 개체에 대한 새 MOLAP 이미지 만들기를 시작하기 전에 개체가 아무런 작업도 수행하지 않을 최소 시간 간격 및 단위를 설정합니다.<br /><br /> 참고: 이 옵션은 **데이터가 변경되면 캐시 업데이트** 를 선택한 경우에만 사용할 수 있습니다.|  
|**대기 대체 간격**|개체에 대한 알림을 받은 후 개체의 현재 작업과 관계없이 자동 관리 캐싱에서 개체에 대한 새 MOLAP 이미지 만들기를 시작할 최대 시간 간격 및 단위를 설정합니다. 이 간격에 도달한 후 받은 알림은 이 간격에 의해 트리거된 MOLAP 이미지 프로세스를 취소하지 않습니다.<br /><br /> 참고: 이 옵션은 **데이터가 변경되면 캐시 업데이트** 를 선택한 경우에만 사용할 수 있습니다. **저장소 모드** 를 **HOLAP**으로 설정한 경우에는이 옵션을 설정 하면 안 됩니다.|  
|**오래된 캐시 삭제**|새 MOLAP 캐시의 생성 시기와 기존 MOLAP 캐시의 제거 시기 간의 기간을 지정합니다.<br /><br /> 참고: 이 옵션은 **자동 관리 캐싱 설정** 을 선택한 경우에만 사용할 수 있습니다. **저장소 모드** 를 HOLAP으로 설정한 경우에는이 옵션을 설정 하면 안 됩니다.|  
|**대기 시간**|새 MOLAP 캐시의 생성 시기와 기존 MOLAP 캐시의 제거 시기 간의 기간에 대한 시간 간격 및 단위를 선택합니다.<br /><br /> 참고: 이 옵션은 **오래된 캐시 삭제** 를 선택한 경우에만 사용할 수 있습니다. **저장소 모드** 를 **HOLAP**으로 설정한 경우에는이 옵션을 설정 하면 안 됩니다.|  
|**주기적으로 캐시 업데이트**|알림과 관계없이 정기적으로 MOLAP 이미지를 업데이트합니다.<br /><br /> 참고: 이 옵션은 **자동 관리 캐싱 설정** 을 선택한 경우에만 사용할 수 있습니다. **저장소 모드** 를 **HOLAP**으로 설정한 경우에는이 옵션을 설정 하면 안 됩니다.|  
|**다시 작성 간격**|새 molap 이미지를 만든 후 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 알림과 관계 없이 개체에 대 한 molap 이미지 프로세스를 다시 시작 하는 기간에 대 한 시간 간격 및 단위를 선택 합니다. 이 간격에 도달한 후 받은 알림은 이 간격에 의해 트리거된 MOLAP 이미지 프로세스를 취소하지 않습니다.<br /><br /> 참고: 이 옵션은 **주기적으로 캐시 업데이트** 를 선택한 경우에만 사용할 수 있습니다. **저장소 모드** 를 **HOLAP**으로 설정한 경우에는이 옵션을 설정 하면 안 됩니다.|  
|**즉시 온라인 상태로 만들기**|개체를 즉시 온라인 상태로 만듭니다. 이 옵션을 설정하면 MOLAP 캐시를 다시 작성하는 동안 개체에서 기본 ROLAP 스토리지를 사용하여 쿼리를 확인합니다. 이 옵션을 설정하지 않으면 개체에 대한 MOLAP 캐시가 완료된 경우에만 개체를 온라인 상태로 만듭니다.|  
|**ROLAP 집계 설정**|기본 데이터 원본에 구체화된 뷰를 사용하여 집계를 저장합니다.<br /><br /> 참고: 기본 데이터 원본에서 구체화된 뷰를 지원하지 않는 경우 개체를 처리할 때 오류가 발생합니다.|  
|**차원에 설정 적용**|연결된 차원에 스토리지 모드와 자동 관리 캐싱 설정을 적용합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [저장소 옵션 대화 상자 &#40;Analysis Services 다차원 데이터&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)   
 [&#40;저장소 옵션 대화 상자&#41; &#40;Analysis Services 다차원 데이터&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)  
  
  
