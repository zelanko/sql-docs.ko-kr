---
title: 데이터베이스 속성 대화 상자 (SSAS-다차원) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.databaseproperties.f1
ms.assetid: 70f000b7-917f-4699-b142-7a0d13ff767c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: be4133aa143ecf0e1fb9b50c40a38a73b4207f30
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082316"
---
# <a name="database-properties-dialog-box-ssas---multidimensional"></a>데이터베이스 속성 대화 상자(SSAS - 다차원)
  **의** 데이터베이스 속성 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 데이터베이스 속성을 설정할 수 있습니다. 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택하면 **데이터베이스 속성**대화 상자가 표시됩니다.  
  
## <a name="options"></a>변수  
  
|용어|정의|  
|----------|----------------|  
|**이름**|데이터베이스 이름을 변경하려면 입력합니다.|  
|**ID**|데이터베이스의 식별자를 표시합니다.|  
|**설명**|데이터베이스에 대한 설명을 변경하려면 입력합니다.|  
|**생성된 타임스탬프**|데이터베이스를 만든 날짜와 시간을 표시합니다.|  
|**최종 스키마 업데이트**|데이터베이스에 대한 메타데이터를 마지막으로 업데이트한 날짜와 시간을 표시합니다.|  
|**마지막 업데이트**|데이터베이스에 대한 데이터를 마지막으로 업데이트한 날짜와 시간을 표시합니다.|  
|**데이터 원본 가장 정보**|데이터베이스에 포함된 데이터 원본에 연결하고 상호 작용할 때 데이터베이스에서 사용할 가장 정보를 선택합니다. 유효한 값은 다음과 같습니다.<br /><br /> **ImpersonateAccount** : 특정 Windows 사용자 이름 및 암호를 사용합니다.<br /><br /> **ImpersonateService** : 서비스 계정을 사용합니다.<br /><br /> **ImpersonateCurrentUser** : 현재 사용자의 자격 증명을 사용합니다.<br /><br /> **Default** : MOLAP 작업에는 서비스 계정을 사용하고 데이터 마이닝에는 현재 사용자를 사용합니다.<br /><br /> 데이터베이스 수준에서 데이터 원본 가장 설정을 지정할 수 있지만 이렇게 하면 해당 가장 설정에 대해 **상속** 을 지정하는 데이터 원본만 영향을 받습니다. 데이터 원본에 직접 지정된 가장 설정은 항상 데이터베이스 수준에서 지정된 설정보다 우선합니다.<br /><br /> 가장 옵션을 선택할 때는 지원해야 하는 작업의 유형을 고려해야 합니다. 처리와 같은 일부 작업은 수행할 수 없습니다.|  
|**마지막으로 처리**|데이터베이스를 마지막으로 처리한 날짜와 시간을 표시합니다.|  
|**예상된 크기**|데이터베이스의 예상 크기를 표시합니다.|  
|**저장소 위치**|데이터베이스의 위치를 지정합니다. 데이터베이스가 기본 데이터 디렉터리에 있으면 이 값은 비어 있게 됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [다차원 model 데이터베이스&#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
