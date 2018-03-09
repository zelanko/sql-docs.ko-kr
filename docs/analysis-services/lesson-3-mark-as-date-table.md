---
title: "4 단원: 날짜 테이블로 표시 | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: e463f148b07d8fbe7061dca0eed66bba1b0fee94
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-3-mark-as-date-table"></a>3 단원: 날짜 테이블로 표시
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

에서는 이름이 DimDate 인 차원 테이블을 가져온 2 단원: 데이터를 추가 합니다. 모델에서이 테이블의 이름이 DimDate 인 동안 것 수 라고도 *날짜 테이블*날짜 및 시간 데이터를 포함 하는, 합니다.  
  
만들 때 측정값 약간 나중에 작업으로 계산에 DAX 시간 인텔리전스 함수를 사용할 때마다 포함 하는 날짜 테이블 속성을 지정 해야 합니다는 *날짜 테이블* 및 고유 식별자 *날짜 열* 해당 테이블의 합니다.
  
이 단원에서는 DimDate 테이블을 표시 합니다는 *날짜 테이블* (날짜 테이블)에서 날짜 열으로 *날짜 열* (고유 식별자)입니다.  

날짜 테이블 및 날짜 열을 표시 하는 것 전에 예제의 모델을 더 쉽게 이해할 수를 약간 정리 작업을 수행 해야 합니다. 라는 열 DimDate 테이블의 알 수 **FullDateAlternateKey**합니다. 테이블에 포함 된 각 달력 연도의 모든 날에 대 한 한 행을 포함 합니다. 와 보고서 측정값 수식에이 열 많은 사용해 보겠습니다. 그러나 FullDateAlternateKey 실제로이 열에 대 한 좋은 식별자가 아닙니다. 되 게 바꾼 것 **날짜**, 쉽게 식별 하 고 수식에 포함 합니다. 가능 하면 항상 같은 테이블 및 열을 쉽게 Power BI 및 Excel 같은 응용 프로그램을 보고 클라이언트에서 식별 하는 개체의 이름을 바꿀 것이 좋습니다. 
  
이 단원에 소요되는 예상 시간: **3분**  
  
## <a name="prerequisites"></a>사전 요구 사항  
이 항목은 순서대로 완료해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [2 단원: 데이터 추가](../analysis-services/lesson-2-add-data.md)합니다. 

### <a name="to-rename-the-fulldatealternatekey-column"></a>FullDateAlternateKey 열 이름을 바꾸려면

1.  모델 디자이너에서 클릭 된 **DimDate** 테이블입니다.

2.  두 번 클릭에 대 한 헤더는 **FullDateAlternateKey** 열을 이름을 바꿉니다 **날짜**합니다.

  
### <a name="to-set-mark-as-date-table"></a>날짜 테이블로 표시 설정 방법  
  
1.  **Date** 열을 선택한 다음 **속성** 창의 **데이터 형식**에서  **날짜** 가 선택되어 있는지 확인합니다.  
  
2.  **테이블** 메뉴를 클릭한 다음 **Date**, **날짜 테이블로 표시**를 차례로 클릭합니다.  
  
3.  **날짜 테이블로 표시** 대화 상자의 **날짜** 목록 상자에서 **Date** 열을 고유 식별자로 선택합니다. 일반적으로 기본적으로 선택 됩니다. **확인**을 클릭합니다. 

    ![-테이블 형식-lesson3-날짜-테이블로](../analysis-services/media/as-tabular-lesson3-date-table.png)
  

## <a name="whats-next"></a>다음 단계
다음 단원으로 이동: [4 단원: 관계 만들기](../analysis-services/lesson-4-create-relationships.md)합니다.
  
