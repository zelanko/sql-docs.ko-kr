---
title: 마법사 완료 (파티션 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.finish.f1
ms.assetid: 68a4dd5d-94d9-4a02-be31-949a6da0ef51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 150007626cab59ab7905d369e8e50d7f1b001982
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102229"
---
# <a name="completing-the-wizard-partition-wizard"></a>마법사 완료(파티션 마법사)
  **마법사 완료** 페이지를 사용하여 파티션의 이름을 지정하고, 파티션에 대한 집계 디자인을 정의하고, 필요에 따라 파티션 마법사를 완료한 후 파티션을 배포 및 처리할 수 있습니다.  
  
## <a name="options"></a>변수  
 **이름**  
 새 파티션의 이름을 입력합니다. 여러 테이블에 대한 작업을 수행하는 경우 각 파티션 이름을 만들기 위해 테이블 이름과 결합할 접두사를 입력합니다.  
  
 **집계 옵션**  
 파티션에 대한 집계 옵션을 지정합니다.  
  
 다음 표에서는 사용 가능한 집계 옵션을 나열합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**지금 파티션에 대 한 집계 디자인**|파티션 마법사가 새 파티션을 만든 후 새 파티션에 대한 집계를 디자인합니다. 이 옵션을 선택하면 파티션 마법사에서 **마침** 을 클릭한 후 집계 디자인 마법사가 시작됩니다. 집계 디자인 마법사에 대한 자세한 내용은 [집계 디자인 마법사 F1 도움말](aggregation-design-wizard-f1-help.md)을 참조하세요.|  
|**나중에 집계 디자인**|집계를 지금 디자인하지 않고 파티션을 만듭니다.|  
|**기존 파티션에서 집계 디자인을 복사 합니다.**|측정값 그룹의 기존 파티션에서 새 파티션으로 집계 디자인을 복사합니다. 이 옵션을 클릭하면 **원본** 옵션을 사용할 수 있습니다. **원본** 옵션을 사용하여 집계 디자인을 복사할 파티션을 선택할 수 있습니다.<br /><br /> 나중에 병합할 파티션은 테이블 구조와 집계 디자인이 동일 해야 하는 참고 합니다. 새 파티션을 측정값 그룹의 기존 파티션과 병합할 경우 기존 파티션의 집계 디자인을 새 파티션에 복사해야 합니다.|  
  
 **지금 배포 및 처리**  
 **처리 및 저장소 위치** 페이지에서 지정한 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 파티션을 배포 및 처리합니다. 이 페이지에서 **마침** 을 클릭하면 마법사가 파티션을 배포 및 처리합니다.  
  
## <a name="see-also"></a>관련 항목  
 [파티션 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
