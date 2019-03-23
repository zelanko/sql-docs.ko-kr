---
title: 데이터 변환을 사용 하 여 데이터를 다른 데이터 형식으로 변환 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 13faac66894298c4d08cd40a1eab9d3d823fd0ee
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394431"
---
# <a name="convert-data-to-a-different-data-type-by-using-the-data-conversion-transformation"></a>데이터 변환을 사용하여 데이터를 다른 데이터 형식으로 변환
  데이터 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 하나의 원본이 이미 들어 있어야 합니다.  
  
### <a name="to-convert-data-to-a-different-data-type"></a>데이터를 다른 데이터 형식으로 변환하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 데이터 변환을 디자인 화면으로 끌어 옵니다.  
  
4.  원본이나 이전 변환에서 연결선을 데이터 변환으로 끌어서 데이터 변환을 데이터 흐름에 연결합니다.  
  
5.  데이터 변환을 두 번 클릭합니다.  
  
6.  **데이터 변환 편집기** 대화 상자의 **사용 가능한 입력 열** 테이블에서 변환하려는 데이터 형식의 열 옆에 있는 확인란을 선택합니다.  
  
    > [!NOTE]  
    >  입력 열에 여러 개의 데이터 변환을 적용할 수 있습니다.  
  
7.  선택적으로 **출력 별칭** 열의 기본값을 수정합니다.  
  
8.  **데이터 형식** 목록에서 열에 사용할 새 데이터 형식을 선택합니다. 기본 데이터 형식은 입력 열의 데이터 형식입니다.  
  
9. 선택한 데이터 형식에 따라 선택적으로 **길이**, **전체 자릿수**, **소수 자릿수**및 **코드 페이지** 열에서 값을 업데이트합니다.  
  
10. 오류 출력을 구성하려면 **오류 출력 구성**을 클릭합니다. 자세한 내용은 [데이터 흐름 구성 요소에서 오류 출력 구성](../../configure-an-error-output-in-a-data-flow-component.md)을 참조하세요.  
  
11. **확인**을 클릭합니다.  
  
12. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Data Conversion Transformation](data-conversion-transformation.md)   
 [Integration Services 변환](integration-services-transformations.md)   
 [Integration Services 경로](../integration-services-paths.md)   
 [Integration Services 데이터 형식](../integration-services-data-types.md)   
 [데이터 흐름 태스크](../../control-flow/data-flow-task.md)  
  
  
