---
title: 자동 관리 캐싱 (파티션 속성 대화 상자) (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.proactivecaching.f1
ms.assetid: ecba72a3-703f-4ede-9d85-9a3318a749e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67ebcc8bcf5c3219d259e4b29eb5c2c737c11df1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118793"
---
# <a name="proactive-caching-partition-properties-dialog-box-ssms"></a>자동 관리 캐싱(파티션 속성 대화 상자)(SSMS)
  SQL Server Management Studio에서 **파티션 속성** 대화 상자의 **자동 관리 캐싱** 페이지를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스 내 큐브에 대한 측정값 그룹에 있는 파티션의 저장소 및 자동 관리 캐싱 속성을 설정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **표준 설정**  
 **표준 설정 슬라이더** 를 설정하고 저장소 모드 및 자동 관리 캐싱 기능에 대해 미리 정의된 설정을 사용하려면 선택합니다.  
  
 **표준 설정 슬라이더**  
 다음 표에 나열된 미리 정의된 설정 중 하나를 설정합니다.  
  
|설정|Description|  
|-------------|-----------------|  
|**실시간 ROLAP**|다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.<br /><br /> ROLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 대기 시간을 0초로 두고 오래된 캐시를 삭제합니다.<br /><br /> 개체를 즉시 온라인 상태로 만듭니다.|  
|**실시간 HOLAP**|다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.<br /><br /> HOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 대기 시간을 0초로 두고 오래된 캐시를 삭제합니다.<br /><br /> 데이터 변경 시 대체 간격 없이 대기 간격을 0초로 두고 캐시를 업데이트합니다.<br /><br /> 개체를 즉시 온라인 상태로 만듭니다.|  
|**짧은 대기 시간 MOLAP**|다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.<br /><br /> MOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 대기 시간을 30분으로 두고 오래된 캐시를 삭제합니다.<br /><br /> 데이터 변경 시 대기 간격을 10초, 대기 대체 간격을 10분으로 두고 캐시를 업데이트합니다.<br /><br /> 데이터 변경 시 대기 간격을 10초, 대기 대체 간격을 10분으로 두고 캐시를 업데이트합니다.<br /><br /> 개체를 즉시 온라인 상태로 만듭니다.|  
|**보통 대기 시간 MOLAP**|즉시 온라인 useBrings 개체를 선택 합니다.<br /><br /> 다음 저장소 및 자동 관리 캐싱 설정:<br /><br /> MOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 대기 시간을 4시간으로 두고 오래된 캐시를 삭제합니다.<br /><br /> 데이터 변경 시 대기 간격을 10초, 대기 대체 간격을 10분으로 두고 캐시를 업데이트합니다.<br /><br /> 개체를 즉시 온라인 상태로 만듭니다.|  
|**자동 MOLAP**|다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.<br /><br /> MOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 데이터 변경 시 대체 간격 없이 대기 간격을 0초로 두고 캐시를 업데이트합니다.|  
|**예약 된 MOLAP**|다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.<br /><br /> MOLAP 스토리지 모드<br /><br /> 자동 관리 캐싱을 설정합니다.<br /><br /> 다시 작성 간격으로 1일을 사용하여 정기적으로 캐시를 업데이트합니다.|  
|**MOLAP**|다음 스토리지 및 자동 관리 캐싱 설정을 사용하려면 선택합니다.<br /><br /> MOLAP 스토리지 모드|  
  
 **사용자 지정 설정**  
 스토리지 모드, 자동 관리 캐싱 및 알림 옵션을 명시적으로 설정하려면 선택합니다.  
  
 **옵션**  
 스토리지 모드, 자동 관리 캐싱 및 알림 옵션을 명시적으로 설정할 수 있는 **스토리지 옵션** 대화 상자를 표시하려면 클릭합니다. **저장소 옵션** 대화 상자에 대한 자세한 내용은 [저장소 옵션 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [자동 관리 캐싱 &#40;파티션&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [파티션 속성 대화 상자 &#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [선택 &#40;파티션 속성 대화 상자&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [일반 &#40;파티션 속성 대화 상자&#41; &#40;SSMS&#41;](general-partition-properties-dialog-box-ssms.md)   
 [큐브, 파티션 및 차원 처리에 대 한 오류 구성 &#40;&AMP;#40;SSAS-다차원&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
