---
title: 모델 열의 별칭 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- mining models [Analysis Services], columns
- column names [Analysis Services]
ms.assetid: c80ebe66-a8f8-4f24-9fe8-8288de9d13bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1df04621d87aa028a2aea43d758fa613dcedccf2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085323"
---
# <a name="create-an-alias-for-a-model-column"></a>모델 열의 별칭 만들기
  
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 모델 열의 별칭을 만들 수 있습니다. 이것은 마이닝 구조 이름이 너무 길어서 쉽게 사용할 수 없거나 모델에서 열의 내용과 사용을 잘 설명하도록 열 이름을 변경할 경우에 유용합니다. 예를 들어 구조 열의 복사본을 만든 다음 특정 모델과 다르게 열을 불연속화한 경우 내용을 보다 정확하게 나타내도록 열의 이름을 바꿀 수 있습니다.  
  
 모델 열의 별칭을 만들려면 **속성** 창을 사용하여 열의 [Name](https://docs.microsoft.com/bi-reference/assl/properties/name-element-assl) 속성을 설정합니다.  
  
 데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 별칭은 열 사용 레이블 옆 괄호 안에 표시됩니다.  
  
 마이닝 모델의 속성을 설정하는 방법은 [마이닝 모델 열](mining-model-columns.md)을 참조하세요.  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>마이닝 모델 열에 별칭을 추가하려면  
  
1.  데이터 마이닝 디자이너의 **마이닝 모델** 탭에서 변경할 마이닝 열의 마이닝 모델에 있는 셀을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  화면 오른쪽의 **속성** 창에서 이름 속성 옆의 셀을 클릭하고 현재 값을 삭제합니다. 열의 새 이름을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
 [마이닝 모델 태스크 및 방법](mining-model-tasks-and-how-tos.md)   
 [마이닝 모델 속성](mining-model-properties.md)  
  
  
