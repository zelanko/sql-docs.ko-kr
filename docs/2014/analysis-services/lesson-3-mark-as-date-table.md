---
title: '4 단원: 날짜 테이블로 표시 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26eb4f82b97d745f6269d57a76c479d677d6cc2c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177533"
---
# <a name="lesson-4-mark-as-date-table"></a>4단원: 날짜 테이블로 표시
  DimDate 라는 차원 테이블을 가져온 2 단원: 데이터를 추가 합니다. 바꾼 DimDate 테이블의 3 단원: 열 이름 바꾸기 간단히 Date로 합니다. 해당 모델에서 이제 이 테이블의 이름은 Date이며 날짜 및 시간 데이터를 포함한다는 점에서 *날짜 테이블*이라고 부를 수도 있습니다.  
  
 잠시 후 측정값을 만들면서 해보겠지만, 계산에 시간 인텔리전스 함수를 사용할 때는 항상 *날짜 테이블* 및 이 테이블의 고유 식별자인 *날짜 열* 이 포함되는 날짜 테이블 속성을 지정해야 합니다. 그런 다음 다른 테이블과 Date 테이블 사이에 유효한 관계를 만들 수 있습니다. 이것은 DAX 시간 인텔리전스 함수를 사용하는 계산에 필요합니다.  
  
 이 단원에서는 가져와 이름을 바꾼 Date 테이블을 *날짜 테이블* 로 표시하고 Date 테이블의 Date 열을 *날짜 열* (고유 식별자)로 표시합니다. 모두 이름에 Date(날짜)를 사용해서 약간 혼란스럽겠지만 곧 이해하게 될 것입니다.  
  
 이 단원에 소요되는 예상 시간: **3분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행하려면 이전 단원인 [3단원: 열 이름 바꾸기](rename-columns.md)를 완료해야 합니다.  
  
### <a name="to-set-mark-as-date-table"></a>날짜 테이블로 표시 설정 방법  
  
1.  모델 디자이너에서 **Date** 테이블(탭)을 클릭합니다.  
  
2.  **테이블** 메뉴를 클릭한 다음 **Date**, **날짜 테이블로 표시**를 차례로 클릭합니다.  
  
3.  **날짜 테이블로 표시** 대화 상자의 **날짜** 목록 상자에서 **Date** 열을 고유 식별자로 선택합니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 자습서를 계속하려면 다음 단원인 [5단원: 관계 만들기](lesson-4-create-relationships.md)로 이동하세요.  
  
  
