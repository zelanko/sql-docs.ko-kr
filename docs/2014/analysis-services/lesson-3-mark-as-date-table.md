---
title: '4단원: 날짜 테이블로 표시 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26877c4892b050cbf9c8dcc6553530dff513f8fc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078793"
---
# <a name="lesson-4-mark-as-date-table"></a>4단원: 날짜 테이블로 표시
  2 단원: DimDate 라는 차원 테이블을 가져온 데이터를 추가 합니다. 다음 단원 3에서 DimDate 테이블의 이름을 바꾼: 간단히 Date로 열을 이름을 바꿉니다. 해당 모델에서 이제 이 테이블의 이름은 Date이며 날짜 및 시간 데이터를 포함한다는 점에서 *날짜 테이블*이라고 부를 수도 있습니다.  
  
 잠시 후 측정값을 만들면서 해보겠지만, 계산에 시간 인텔리전스 함수를 사용할 때는 항상 *날짜 테이블* 및 이 테이블의 고유 식별자인 *날짜 열* 이 포함되는 날짜 테이블 속성을 지정해야 합니다. 그런 다음 다른 테이블과 Date 테이블 사이에 유효한 관계를 만들 수 있습니다. 이것은 DAX 시간 인텔리전스 함수를 사용하는 계산에 필요합니다.  
  
 이 단원에서는 가져와 이름을 바꾼 Date 테이블을 *날짜 테이블* 로 표시하고 Date 테이블의 Date 열을 *날짜 열* (고유 식별자)로 표시합니다. 날짜는 일종의 혼동을 가져올 수 있습니다 이름을 있지만 모든 사용 겠지만 곧 이해 됩니다.  
  
 예상이 단원을 완료 시간: **3 분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 이전 단원을 완료 해야 합니다. [3단원: 열 이름 바꾸기](rename-columns.md)합니다.  
  
### <a name="to-set-mark-as-date-table"></a>날짜 테이블로 표시 설정 방법  
  
1.  모델 디자이너에서 **Date** 테이블(탭)을 클릭합니다.  
  
2.  **테이블** 메뉴를 클릭한 다음 **Date**, **날짜 테이블로 표시**를 차례로 클릭합니다.  
  
3.  **날짜 테이블로 표시** 대화 상자의 **날짜** 목록 상자에서 **Date** 열을 고유 식별자로 선택합니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 자습서를 계속 하려면 다음 단원으로 이동 합니다. [5단원: 관계를 만들](lesson-4-create-relationships.md)합니다.  
  
  
