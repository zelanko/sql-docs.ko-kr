---
title: 저장소 설정 대화 상자 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.f1
- sql12.asvs.cubeeditor.cubebuilder.measuregroupstoragesettings.f1
ms.assetid: 80c41c71-226c-45fe-b9cf-af824b592fe1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd796d2fb2bc37c4c2ad6d9fac00ef4258ec038
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068024"
---
# <a name="storage-settings-dialog-box-analysis-services---multidimensional-data"></a>스토리지 설정 대화 상자(Analysis Services - 다차원 데이터)
  **의** 저장소 설정 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 사용하여 차원, 큐브, 측정값 그룹 또는 파티션에 대해 자동 관리 캐싱, 저장소 및 알림 설정을 지정할 수 있습니다. 다음을 수행하여 **에서** 스토리지 설정 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 대화 상자를 표시할 수 있습니다.  
  
-   줄임표 단추를 클릭 ( **...** )에 대 한 합니다 `ProactiveCaching` 속성은 차원, 큐브, 측정값 그룹 또는 파티션에 합니다 **속성** 기간 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]합니다.  
  
-   **큐브 디자이너** 의 **파티션** 탭에서 측정값 그룹을 확장하고 **저장소 설정**을 클릭합니다.  
  
-   **큐브 디자이너** 의 **파티션** 탭에서 측정값 그룹을 확장하고 해당 측정값 그룹에 대한 표에서 파티션을 선택한 다음  **설정**을 클릭합니다.  
  
-   **큐브 디자이너** 의 **파티션** 탭에서 측정값 그룹을 확장하고 해당 측정값 그룹에 대한 표에서 파티션을 선택한 다음 **큐브 디자이너** 의 **파티션** 탭에 있는 **도구 모음** 창에서 **저장소 설정**을 클릭합니다.  
  
## <a name="options"></a>변수  
  
|용어|정의|값|  
|----------|----------------|------------|  
|**표준 설정**|**표준 설정 슬라이더** 를 설정하고 저장소 모드 및 자동 관리 캐싱 기능에 대해 미리 정의된 설정을 사용하려면 선택합니다.||  
|**표준 설정 슬라이더**|다음 미리 정의된 설정 중 하나로 설정합니다.<br /><br /> **실시간 ROLAP**<br /><br /> 다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.|ROLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 대기 시간을 0초로 두고 오래된 캐시를 삭제합니다.<br /><br /> 개체를 즉시 온라인 상태로 만듭니다.|  
||**실시간 HOLAP**<br /><br /> 다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.|HOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 대기 시간을 0초로 두고 오래된 캐시를 삭제합니다.<br /><br /> 데이터 변경 시 대기 대체 간격 없이 대기 간격을 0초로 두고 캐시를 업데이트합니다.<br /><br /> 개체를 즉시 온라인 상태로 만듭니다.|  
||**짧은 대기 시간 MOLAP**<br /><br /> 다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.|MOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 대기 시간을 30분으로 두고 오래된 캐시를 삭제합니다.<br /><br /> 데이터 변경 시 대기 간격을 10초, 대기 대체 간격을 10분으로 두고 캐시를 업데이트합니다.<br /><br /> 개체를 즉시 온라인 상태로 만듭니다.|  
||**보통 대기 시간 MOLAP**<br /><br /> 다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.|MOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 대기 시간을 4시간으로 두고 오래된 캐시를 삭제합니다.<br /><br /> 데이터 변경 시 대기 간격을 10초, 대기 대체 간격을 10분으로 두고 캐시를 업데이트합니다.<br /><br /> 개체를 즉시 온라인 상태로 만듭니다.|  
||**자동 MOLAP**<br /><br /> 다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.|MOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 데이터 변경 시 대기 대체 간격 없이 대기 간격을 0초로 두고 캐시를 업데이트합니다.|  
||**예약 된 MOLAP**<br /><br /> 다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.|MOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 다시 작성 간격으로 1일을 사용하여 정기적으로 캐시를 업데이트합니다.|  
||**MOLAP**<br /><br /> 다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.|MOLAP 스토리지 모드|  
|**사용자 지정 설정**|스토리지 모드, 자동 관리 캐싱 및 알림 옵션을 명시적으로 설정하려면 선택합니다.||  
|**옵션**|스토리지 모드, 자동 관리 캐싱 및 알림 옵션을 명시적으로 설정할 수 있는 **스토리지 옵션** 대화 상자를 표시하려면 클릭합니다. **저장소 옵션** 대화 상자에 대한 자세한 내용은 [저장소 옵션 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.||  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [자동 관리 캐싱 &#40;파티션&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [큐브 저장소 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)  
  
  
