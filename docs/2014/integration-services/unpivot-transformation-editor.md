---
title: 피벗 해제 변환 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottransformation.f1
helpviewer_keywords:
- Unpivot Transformation Editor
ms.assetid: 72a36ef0-4070-4f6c-9c74-0720109617dd
caps.latest.revision: 34
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2864345230b02bc16756c82116dc40a53b2a7264
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37199663"
---
# <a name="unpivot-transformation-editor"></a>피벗 해제 변환 편집기
  **피벗 해제 변환 편집기** 대화 상자를 사용하여 행에 피벗할 열을 선택하고 데이터 열 및 새 피벗 값 출력 열을 지정할 수 있습니다.  
  
> [!NOTE]  
>  이 항목에서는 [피벗 해제 변환](data-flow/transformations/unpivot-transformation.md) 에 설명된 피벗 해제 시나리오를 사용하여 옵션 사용법을 보여 줍니다.  
  
 피벗 해제 변환에 대한 자세한 내용은 [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **사용 가능한 입력 열**  
 확인란을 사용하여 행에 피벗할 열을 지정합니다.  
  
 **이름**  
 사용 가능한 입력 열의 이름을 표시합니다.  
  
 **통과**  
 열을 피벗 해제된 출력에 포함할지 여부를 나타냅니다.  
  
 **입력 열**  
 각 행에 대해 사용 가능한 입력 열 목록에서 선택합니다. 선택 내용에 따라 **사용 가능한 입력 열** 테이블의 확인란이 달라집니다.  
  
 [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md)에 설명된 피벗 해제 시나리오에서 입력 열은 **햄**, **탄산음료**, **우유**, **맥주**및 **칩** 열입니다.  
  
 **대상 열**  
 데이터 열에 사용할 이름을 제공합니다.  
  
 [피벗 해제 변환](data-flow/transformations/unpivot-transformation.md)에 설명된 피벗 해제 시나리오에서 대상 열은 수량(**Qty**) 열입니다.  
  
 **피벗 키 값**  
 피벗 값에 사용할 이름을 제공합니다. 기본값은 입력 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.  
  
 [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md)에 설명된 피벗 해제 시나리오에서 피벗 값은 **피벗 키 값 열 이름** 옵션으로 지정한 새 제품 열에 **햄**, **탄산음료**, **우유**, **맥주**및 **칩**과 같은 텍스트 값으로 나타납니다.  
  
 **피벗 키 값 열 이름**  
 피벗 값 열에 사용할 이름을 제공합니다. 기본값은 "피벗 키 값"이지만 알기 쉬운 임의의 고유 이름을 선택할 수 있습니다.  
  
 [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md)에 설명된 피벗 해제 시나리오에서 피벗 키 값 열 이름은 **제품** 이며 **제품** , **탄산음료**, **우유**, **맥주**, **칩**열이 피벗 해제되는 새 **제품** 열을 지정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [피벗 변환](data-flow/transformations/pivot-transformation.md)  
  
  
