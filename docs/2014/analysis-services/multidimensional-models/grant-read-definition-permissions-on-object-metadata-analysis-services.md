---
title: 정의 읽기 권한 부여 개체 메타 데이터 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- metadata [Analysis Services]
- permissions [Analysis Services], read metadata
- read metadata permissions
ms.assetid: c857e48e-64b0-4ffe-900d-a0a3ddafcefb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dca06ce28f496c2ac85417c9ca4326d2ff66cf7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62725897"
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>개체 메타데이터에 대한 정의 읽기 권한 부여(Analysis Services)
  선택한 개체에 대한 개체 정의 또는 메타데이터를 읽을 수 있는 권한을 통해 관리자는 개체 정의를 수정하거나 개체 구조를 수정하거나 개체에 대한 실제 데이터를 볼 수 있는 권한을 부여하지 않고도 개체 정보를 볼 수 있는 권한을 부여할 수 있습니다. `Read Definition` 데이터베이스, 데이터 원본, 차원, 마이닝 구조 및 마이닝 모델 수준에서 권한은 부여할 수 있습니다. 필요한 경우 `Read Definition` 큐브에 대 한 권한을 설정한 다음 `Read Definition` 데이터베이스에 대 한 합니다. 사용 권한은 가산적입니다. 예를 들어 한 역할이 큐브에 대한 메타데이터를 읽을 수 있는 권한을 부여하고 두 번째 역할은 동일한 사용자에게 차원에 대한 메타데이터를 읽을 수 있는 권한을 부여합니다. 이 경우 두 역할의 사용 권한이 결합하여 사용자는 큐브에 대한 메타데이터와 해당 데이터베이스 내의 차원에 대한 메타데이터를 읽을 수 있는 권한을 동시에 부여받습니다.  
  
> [!NOTE]  
>  데이터베이스의 메타데이터를 읽을 수 있는 권한은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]데이터베이스에 연결하는 데 필요한 최소 사용 권한입니다. 메타데이터를 읽을 권한이 있는 사용자는 DISCOVER_XML_METADATA 스키마 행 집합을 사용하여 개체를 쿼리하고 해당 메타데이터를 볼 수도 있습니다. 자세한 내용은 [DISCOVER_XML_METADATA 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset)을 참조하세요.  
  
## <a name="set-read-definition-permissions-on-a-database"></a>데이터베이스에 대한 정의 읽기 권한 설정  
 데이터베이스 메타데이터를 읽을 수 있는 권한을 부여하면 데이터베이스 내 모든 개체의 메타데이터를 읽을 수 있는 권한도 부여됩니다.  
  
 포함 하는 것이 좋습니다는 `Read Definition` 전용된 처리에 대 한 역할을 설정 하는 때마다 데이터베이스 수준 권한. 것 `Read Definition` 관리자가 아닌 모델의 개체 계층에서 보고를 사용 하면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 후속 처리를 위해 개별 개체로 이동할입니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 개체 탐색기에서 해당 데이터베이스에 대한 **역할** 을 확장한 다음 데이터베이스 역할을 클릭하거나 새 데이터베이스 역할을 만듭니다.  
  
2.  에 **일반** 탭을 선택 합니다 `Read Definition` 옵션입니다.  
  
3.  **멤버 자격** 창에서 이 역할을 사용하여 Analysis Services에 연결하는 Windows 사용자 및 그룹 계정을 입력합니다.  
  
4.  **확인** 을 클릭하여 역할 만들기를 마칩니다.  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>개별 개체에 대한 정의 읽기 권한 설정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 **데이터베이스** 폴더를 열고 데이터베이스를 선택하고 개체 탐색기에서 해당 데이터베이스에 대한 **역할** 을 확장한 다음 데이터베이스 역할을 클릭하거나 새 데이터베이스 역할을 만듭니다.  
  
2.  에 **일반적인** 창에 대 한 데이터베이스 권한을 제거 `Read Definition`합니다. 이 단계는 사용 권한 상속을 제거하므로, 개별 개체에 대한 사용 권한을 설정할 수 있습니다.  
  
3.  지정 하는 개체를 선택 `Read Definition` 속성:  
  
    -   에 **데이터 원본** 창 클릭는 `Read Definition` 해당 데이터 원본에 대 한 확인란 합니다. 역할 구성원은 서버 이름 및 사용자 이름(가능한 경우)을 비롯하여 데이터 원본에 대한 연결 문자열을 볼 수 있습니다. 연결 문자열 정보를 제공하려는 경우 연결 문자열을 수정하거나 임의의 기타 개체 정의를 볼 수 있는 권한을 부여하지 않고 이 사용 권한을 사용할 수 있습니다.  
  
    -   에 **차원을** 창 클릭는 `Read Definition` 해당 차원에 대 한 확인란 합니다. 숙련된 분석가 및 개발자는 정의를 수정하거나 다른 개체(예: 다른 차원, 큐브 개체 또는 마이닝 구조 및 모델)의 정의를 볼 수 있는 권한이 없어도 정의를 볼 수 있어야 합니다.  
  
    -   마이닝 구조 창에서 클릭 된 `Read Definition` 데이터 마이닝 구조 또는 모델에 대 한 확인란 합니다. `Read Definition` 데이터 모델을 찾아보기에 필요 합니다. 자세한 내용은 [데이터 마이닝 구조 및 모델에 대한 권한 부여&#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)를 참조하세요.  
  
4.  **멤버 자격** 창에서 이 역할을 사용하여 Analysis Services에 연결하는 Windows 사용자 및 그룹 계정을 입력합니다.  
  
5.  **확인** 을 클릭하여 역할 만들기를 마칩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 권한 부여&#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)   
 [처리 권한 부여&#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
  
