---
title: 계산된 열 (SSAS 테이블 형식) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.as.daxref.CreataCalculatedColumn.f1
ms.assetid: 59440510-2d76-41dc-9b55-edc15259f9da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 40e802ac33c7aa9b97267a725b20eb0d2f00dbb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62794208"
---
# <a name="create-a-calculated-column-ssas-tabular"></a>계산 열 만들기(SSAS 테이블 형식)
  계산 열을 사용하면 모델에 새 데이터를 추가할 수 있습니다. 붙여넣기 또는 열에 값을 가져오는 대신 열 행 수준 값을 정의 하는 DAX 수식을 만듭니다. 유효한 수식을 만든 다음 ENTER 키를 누르면 계산 열의 각 행에서 값이 계산되어 채워집니다. 그런 다음 다른 데이터 열과 마찬가지로 보고 또는 분석 애플리케이션에 계산 열을 추가할 수 있습니다. 이 항목에서는 모델 디자이너의 DAX 수식 입력줄을 사용하여 새 계산 열을 만드는 방법에 대해 설명합니다.  
  
#### <a name="to-create-a-new-calculated-column"></a>새 계산 열을 만들려면  
  
1.  모델 디자이너의 데이터 뷰에서 계산 열을 추가하려는 테이블을 선택한 다음 **열** 메뉴를 클릭하고 **열 추가**를 클릭합니다.  
  
     비어 있는 가장 오른쪽 열에서**열 추가** 가 강조 표시되고 커서가 수식 입력줄로 이동합니다.  
  
     기존의 두 열 사이에 새 열을 만들려면 기존 열을 마우스 오른쪽 단추로 클릭하고 **열 삽입**을 클릭합니다.  
  
2.  수식 입력줄에서 다음 중 하나를 수행합니다.  
  
    -   등호 다음에 수식을 입력합니다.  
  
    -   등호 다음에 DAX 함수 및 함수에 필요한 매개 변수와 인수를 차례로 입력합니다.  
  
    -   함수 단추(**fx**)를 클릭한 다음 **함수 삽입** 대화 상자에서 범주와 함수를 선택한 후 **확인**을 클릭합니다. 수식 입력줄에서 함수에 필요한 나머지 인수 및 매개 변수를 입력합니다.  
  
3.  Enter 키를 눌러 수식을 적용합니다.  
  
     전체 열이 수식으로 채워지고 각 행의 값이 계산됩니다.  
  
> [!TIP]  
>  중첩된 함수가 있는 기존 수식의 중간에 DAX 수식 자동 완성 기능을 사용할 수 있습니다. 삽입 지점 바로 전 텍스트는 드롭다운 목록의 값을 표시하는 데 사용되며 삽입 지점 이후의 모든 텍스트는 변경되지 않은 상태로 유지됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [계산 열&#40;SSAS 테이블 형식&#41;](ssas-calculated-columns.md)   
 [측정값&#40;SSAS 테이블 형식&#41;](measures-ssas-tabular.md)  
  
  
