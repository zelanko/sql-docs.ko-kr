---
title: 'Analysis Services 자습서 단원 3: 날짜 테이블로 표시 | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 82b4093aa1a46cf1a7bb14b4c689ba6ba09e4d2b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37973170"
---
# <a name="mark-as-date-table"></a>날짜 테이블로 표시

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

단원 2: 데이터 가져오기, 가져온 라는 차원 테이블 **DimDate**합니다. 모델에서이 테이블의 이름이 DimDate 인 것도 수 이라고 있습니다를 *날짜 테이블*, 날짜 및 시간 데이터를 포함 합니다.  
  
나중에 측정값을 만들 때 같은 DAX 시간 인텔리전스 함수를 사용할 때마다 포함 하는 속성을 지정 해야 하는 *날짜 테이블* 및 고유 식별자 *날짜 열* 해당 테이블의 합니다.
  
표시 하면이 단원에서는 **DimDate** 으로 테이블의 *날짜 테이블* 및 **날짜** 는 날짜 테이블의 열으로는 *날짜 열* (고유 식별자)입니다.  

날짜 테이블 및 날짜 열을 표시 하기 전에 모델을 더 쉽게 이해 하려면 약간의 관리 유지 작업을 수행 하는 것이 좋습니다. DimDate 테이블에서 명명 된 열을 확인 **FullDateAlternateKey**합니다. 이 열은 테이블에 포함 된 각 연도의 모든 날에 대 한 하나의 행을 포함 합니다. 이 열 사용 많은 측정값 수식 및 보고서에서. 그러나 FullDateAlternateKey 없는이 열에 대 한 적절 한 식별자. 파일 이름을 **날짜**, 쉽게 식별 하 고 수식에 포함 합니다. 가능 하면 테이블 및 열을 쉽게 SSDT 및 클라이언트 보고 응용 프로그램 식별과 같은 개체의 이름을 바꿀 것이 좋습니다. 
  
이 단원을 완료 하기 위한 예상 시간: **3 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [2 단원: 데이터 가져오기](../tutorial-tabular-1400/as-lesson-2-get-data.md)합니다. 

### <a name="to-rename-the-fulldatealternatekey-column"></a>FullDateAlternateKey 열 이름을 바꾸려면

1.  모델 디자이너에서를 클릭 합니다 **DimDate** 테이블입니다.

2.  에 대 한 헤더를 두 번 클릭 합니다 **FullDateAlternateKey** 열을 이름을 바꿉니다 **날짜**합니다.

  
### <a name="to-set-mark-as-date-table"></a>날짜 테이블로 표시 설정 방법  
  
1.  **Date** 열을 선택한 다음 **속성** 창의 **데이터 형식**에서  **날짜** 가 선택되어 있는지 확인합니다.  
  
2.  **테이블** 메뉴를 클릭한 다음 **Date**, **날짜 테이블로 표시**를 차례로 클릭합니다.  
  
3.  **날짜 테이블로 표시** 대화 상자의 **날짜** 목록 상자에서 **Date** 열을 고유 식별자로 선택합니다. 일반적으로 기본적으로 선택 됩니다. **확인**을 클릭합니다. 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>다음 단계

[4 단원: 관계 만들기](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)합니다.
  
