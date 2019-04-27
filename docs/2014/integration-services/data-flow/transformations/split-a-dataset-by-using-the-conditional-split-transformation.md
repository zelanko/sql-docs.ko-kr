---
title: 조건부 분할 변환을 사용하여 데이터 세트 분할 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Conditional Split transformation
- splitting dataset
- datasets [Integration Services], splitting
ms.assetid: 23b3e84f-9296-4dc9-81c0-c7f06ae3f1ff
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6585733a4b864e14815990189fd6924e217de546
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770690"
---
# <a name="split-a-dataset-by-using-the-conditional-split-transformation"></a>조건부 분할 변환을 사용하여 데이터 세트 분할
  조건부 분할 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 하나의 원본이 이미 들어 있어야 합니다.  
  
### <a name="to-conditionally-split-a-dataset"></a>데이터 세트를 조건적으로 분할하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭하고 **도구 상자**에서 조건부 분할 변환을 디자인 화면으로 끌어 옵니다.  
  
4.  데이터 원본이나 이전 변환에서 연결선을 조건부 분할 변환으로 끌어서 조건부 분할 변환을 데이터 흐름에 연결합니다.  
  
5.  조건부 분할 변환을 두 번 클릭합니다.  
  
6.  **조건부 분할 변환 편집기**에서 변수, 열, 함수 및 연산자를 표의 **조건** 열로 끌어서 조건에 따라 사용할 식을 작성합니다. 또는 **조건** 열에 식을 직접 입력할 수 있습니다.  
  
    > [!NOTE]  
    >  변수 또는 열은 여러 식에서 사용될 수 있습니다.  
  
    > [!NOTE]  
    >  식이 올바르지 않으면 식 텍스트가 강조 표시되고 열의 도구 설명에 오류에 대한 설명이 제공됩니다.  
  
7.  선택적으로 **출력 이름** 열의 값을 수정합니다. 기본 이름은 사례 1, 사례 2 등과 같습니다.  
  
8.  조건이 평가되는 순서를 수정하려면 위 또는 아래 화살표를 클릭합니다.  
  
    > [!NOTE]  
    >  발생할 가능성이 가장 높은 조건을 목록의 위쪽에 두십시오.  
  
9. 선택적으로 어떤 조건에도 부합되지 않는 데이터 행에 대한 기본 출력의 이름을 수정합니다.  
  
10. 오류 출력을 구성하려면 **오류 출력 구성**을 클릭합니다. 자세한 내용은 [데이터 흐름 구성 요소에서 오류 출력 구성](../../configure-an-error-output-in-a-data-flow-component.md)을 참조하세요.  
  
11. **확인**을 클릭합니다.  
  
12. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Conditional Split Transformation](conditional-split-transformation.md)   
 [Integration Services 변환](integration-services-transformations.md)   
 [Integration Services 경로](../integration-services-paths.md)   
 [Integration Services 데이터 형식](../integration-services-data-types.md)   
 [데이터 흐름 태스크](../../control-flow/data-flow-task.md)   
 [Integration Services&#40;SSIS&#41; 식](../../expressions/integration-services-ssis-expressions.md)  
  
  
