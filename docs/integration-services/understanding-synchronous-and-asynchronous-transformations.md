---
description: 동기 및 비동기 변환 이해
title: 동기 및 비동기 변환 이해 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], synchronous and asynchronous
- asynchronous transformations [Integration Services]
- data flow components [Integration Services], synchronous and asynchronous
- synchronous transformations [Integration Services]
ms.assetid: 0bc2bda5-3f8a-49c2-aaf1-01dbe4c3ebba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 849f01ba00bddd67ca2de2c16b6953cff9b06c36
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88495169"
---
# <a name="understanding-synchronous-and-asynchronous-transformations"></a>동기 및 비동기 변환 이해

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 동기 변환과 비동기 변환의 차이점을 가장 쉽게 이해하려면 먼저 동기 변환을 이해해야 합니다. 동기 변환이 개발자의 요구에 맞지 않으면 디자인에 비동기 변환을 사용해야 합니다.  
  
## <a name="synchronous-transformations"></a>동기 변환  
 동기 변환은 들어오는 행을 처리한 후 데이터 흐름에서 한 번에 한 행씩 전달합니다. 출력은 입력과 동기적으로, 즉 동시에 발생합니다. 따라서 이 변환에서는 특정 행을 처리하는 데 데이터 집합의 다른 행에 대한 정보가 필요하지 않습니다. 실제 구현에서 행은 한 구성 요소에서 다음 구성 요소로 전달될 때 버퍼로 그룹화되지만 버퍼는 사용자가 인식할 수 있으므로 각 행이 개별적으로 처리되는 것으로 가정할 수 있습니다.  
  
 동기 변환의 예로는 데이터 변환이 있습니다. 이 변환에서는 들어오는 각 행에 대해 지정된 열의 값을 변환하고 해당 행을 개별적으로 보냅니다. 각각의 불연속 변환 작업은 데이터 집합의 다른 모든 행과 독립적으로 이루어집니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 스크립팅 및 프로그래밍에서 구성 요소 입력의 ID를 검색하고 이를 구성 요소 출력의 **SynchronousInputID** 속성에 할당하여 동기 변환을 지정합니다. 이렇게 하면 데이터 흐름 엔진에서는 입력의 각 행을 처리하고 자동으로 각 행을 지정된 출력으로 보내게 됩니다. 모든 행을 모든 출력으로 보내려는 경우에는 데이터를 출력하기 위한 추가 코드를 작성할 필요가 없습니다. **ExclusionGroup** 속성을 사용하여 조건부 분할 변환에서처럼 행을 출력 그룹 중 하나 또는 다른 행으로만 보내도록 지정하려는 경우 **DirectRow** 메서드를 호출하여 각 행에 대한 적절한 대상을 선택해야 합니다. 오류 출력이 있으면 **DirectErrorRow** 를 호출하여 문제가 있는 행을 기본 출력 대신 오류 출력으로 보내야 합니다.  
  
## <a name="asynchronous-transformations"></a>비동기 변환  
 각 행을 다른 모든 행에 독립적으로 처리할 수 없는 경우 디자인에 비동기 변환을 사용해야 할 수 있습니다. 즉, 각 행을 처리할 때 데이터 흐름에 따라 전달할 수 없지만 대신 데이터를 비동기적으로 출력하거나 입력과는 다른 시기에 출력해야 합니다. 예를 들어 다음과 같은 경우에는 비동기 변환이 필요합니다.  
  
-   구성 요소에서 처리를 수행하기 전에 여러 개의 데이터 버퍼를 확보해야 하는 경우. 예를 들어 구성 요소에서 전체 행 집합을 한 번의 작업으로 처리해야 하는 정렬 변환의 경우가 이에 해당합니다.  
  
-   구성 요소에서 여러 입력의 행을 결합해야 하는 경우. 예를 들어 구성 요소에서 각 입력의 여러 행을 검사한 다음 정렬된 순서로 병합해야 하는 병합 변환의 경우가 이에 해당합니다.  
  
-   입력 행과 출력 행은 일 대 일로 대응하지 않는 경우. 예를 들어 구성 요소에서 출력에 행을 추가하여 계산된 집계 값을 저장해야 하는 집계 변환의 경우가 이에 해당합니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 스크립팅 및 프로그래밍에서 구성 요소 출력의 **SynchronousInputID** 속성에 0 값을 할당하여 비동기 변환을 지정합니다. . 이렇게 하면 데이터 흐름 엔진에서는 자동으로 각 행을 출력으로 보내지 않게 됩니다. 그런 다음 각 행을 비동기 변환의 출력을 위해 만들어진 새 출력 버퍼에 추가하여 해당 행을 명시적으로 적절한 출력으로 보내는 코드를 작성해야 합니다.  
  
> [!NOTE]  
>  원본 구성 요소에서도 데이터 원본에서 읽어 온 각 행을 해당 출력 버퍼에 명시적으로 추가해야 하므로 비동기 출력을 사용할 경우에는 원본과 변환이 유사하게 됩니다.  
  
 각 입력 행을 출력에 명시적으로 복사하여 동기 변환을 에뮬레이트하는 비동기 변환을 만들 수도 있습니다. 이 방법을 사용하면 열 이름을 바꾸거나 데이터 형식을 변환할 수 있습니다. 그러나 성능은 저하됩니다. 열 복사 또는 데이터 변환과 같은 기본 제공 Integration Services 구성 요소를 사용하면 보다 나은 성능으로 동일한 결과를 얻을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [스크립트 구성 요소를 사용하여 비동기 변환 만들기](../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)   
 [동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [비동기 출력을 사용하여 사용자 지정 변환 구성 요소 개발](../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
