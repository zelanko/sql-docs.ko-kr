---
title: "특정 유형의 스크립트 구성 요소 개발 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: dfbbe959-6b4e-4b47-b9dd-bcc31929482d
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 458ba4be689ed976a5948380d35f38020f7dd4dd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="developing-specific-types-of-script-components"></a>특정 유형의 스크립트 구성 요소 개발
  스크립트 구성 요소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 원본, 변환 및 대상이 충족시키지 않는 거의 모든 요구 사항을 충족시키기 위해 패키지의 데이터 흐름에서 사용할 수 있는 구성 가능한 도구입니다. 이 섹션에는 스크립트 구성 요소를 구성하는 네 가지 옵션을 보여 주는 스크립트 구성 요소 코드 예제가 들어 있습니다.  
  
-   원본으로 구성  
  
-   동기 출력을 사용하는 변환으로 구성  
  
-   비동기 출력을 사용하는 변환으로 구성  
  
-   대상으로 구성  
  
 스크립트 구성 요소 추가 예제를 참조 하십시오. [Additional Script Component Examples](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [스크립트 구성 요소를 사용하여 원본 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)  
 스크립트 구성 요소를 사용하여 데이터 흐름 원본을 만드는 방법을 설명하고 예로 보여 줍니다.  
  
 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 스크립트 구성 요소를 사용하여 동기 출력을 사용하는 데이터 흐름 변환을 만드는 방법을 설명하고 예로 보여 줍니다. 이러한 종류의 변환에서는 데이터 행이 구성 요소를 통해 전달될 때 현재 위치에서 해당 행을 수정합니다.  
  
 [스크립트 구성 요소를 사용하여 비동기 변환 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
 스크립트 구성 요소를 사용하여 비동기 출력을 사용하는 데이터 흐름 변환을 만드는 방법을 설명하고 예로 보여 줍니다. 이러한 종류의 변환에서는 모든 데이터 행을 읽은 후에만 계산된 집계와 같은 추가 정보를 구성 요소를 통해 전달되는 데이터에 추가할 수 있습니다.  
  
 [스크립트 구성 요소를 사용하여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
 스크립트 구성 요소를 사용하여 데이터 흐름 대상을 만드는 방법을 설명하고 예로 보여 줍니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 솔루션과 사용자 지정 개체를 비교합니다.](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [개발 특정 유형의 데이터 흐름 구성 요소](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
  
  

