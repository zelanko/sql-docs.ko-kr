---
title: 집계 변환을 사용하여 데이터 세트의 값 집계 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6b6f11ac0a41b52f6b8e197b21279a22df46703d
ms.sourcegitcommit: 6ee40a2411a635daeec83fa473d8a19e5ae64662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "77903755"
---
# <a name="aggregate-values-in-a-dataset-with-the-aggregate-transformation"></a>집계 변환을 사용하여 데이터 세트의 값 집계

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  집계 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 하나의 원본이 이미 들어 있어야 합니다.  
  
### <a name="to-aggregate-values-in-a-dataset"></a>데이터 세트의 값을 집계하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 집계 변환을 디자인 화면으로 끌어 옵니다.  
  
4.  원본이나 이전 변환에서 연결선을 집계 변환으로 끌어서 집계 변환을 데이터 흐름에 연결합니다.  
  
5.  변환을 두 번 클릭합니다.  
  
6.  **집계 변환 편집기** 대화 상자에서 **집계** 탭을 클릭합니다.  
  
7.  **사용 가능한 입력 열** 목록에서 값을 집계하려는 열의 확인란을 선택합니다. 선택한 열이 테이블에 표시됩니다.  
  
    > [!NOTE]  
    >  열에 다중 변환을 사용하면 한 열을 여러 번 선택할 수 있습니다. 집계를 고유하게 식별하기 위해 열의 출력 별칭 기본 이름에 숫자가 붙여집니다.  
  
8.  선택적으로 **출력 별칭** 열의 값을 수정합니다.  
  
9. 기본 집계 작업인 **Group by**를 변경하려면 **작업** 목록에서 다른 작업을 선택합니다.  
  
10. 기본 비교를 변경하려면 **비교 플래그** 열에서 나열된 개별 비교 플래그를 선택합니다. 기본적으로 비교는 대/소문자, 가나 형식, 공백 없는 문자 및 문자 너비를 무시합니다.  
  
11. 선택적으로 **Count distinct** 집계에 대해 **고유 키 수** 열에서 정확한 고유 값 수를 지정하거나 **고유 수 배율** 열에서 대략적인 수를 선택합니다.  
  
    > [!NOTE]  
    >  정확하게든 또는 대략적으로든 고유 값 수를 제공하면 변환을 통해 작업을 수행할 수 있도록 해당 메모리 양을 미리 할당할 수 있으므로 성능이 최적화됩니다.  
  
12. 선택적으로 **고급** 을 클릭하여 집계 변환 출력의 이름을 업데이트합니다. 집계에 **Group By** 작업이 있으면 **키 배율** 열에서 키 값 그룹의 대략적인 개수를 선택하거나 **키** 열에서 키 값 그룹의 정확한 개수를 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  정확하게든 또는 대략적으로든 고유 값 수를 제공하면 변환을 통해 작업을 수행할 수 있도록 해당 메모리 양을 미리 할당할 수 있으므로 성능이 최적화됩니다.  
  
    > [!NOTE]  
    >  **키 배율** 및 **키** 옵션은 상호 배타적입니다. 두 열 모두에 값을 입력하면 **키 배율** 또는 **키** 값 중에서 더 큰 값이 사용됩니다.  
  
13. 선택적으로 **고급** 탭을 클릭하고 집계 변환이 수행하는 모든 작업을 최적화하는 데 적용되는 특성을 설정합니다.  
  
14. **확인**을 클릭합니다.  
  
15. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [집계 변환](../../../integration-services/data-flow/transformations/aggregate-transformation.md)   
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 경로](../../../integration-services/data-flow/integration-services-paths.md)   
 [데이터 흐름 태스크](../../../integration-services/control-flow/data-flow-task.md)  
  
  
