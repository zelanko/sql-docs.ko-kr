---
title: 데이터 형식 및 내용 유형 지정 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 72484d27-3ef1-4f16-813c-2f43231fc2da
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 583a6fda2dbb4698405a3d69f33955531b3c1c10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62720050"
---
# <a name="specifying-the-data-type-and-content-type-basic-data-mining-tutorial"></a>데이터 형식 및 내용 유형 지정(기본 데이터 마이닝 마법사)
  구조를 구축하고 모델을 학습하는 데 사용할 열을 선택했으므로 마법사에서 설정한 기본 데이터와 내용 유형을 변경해야 합니다.  
  
#### <a name="review-and-modify-content-type-and-data-type-for-each-column"></a>각 열에 대한 내용 유형과 데이터 형식 검토 및 수정  
  
1.  **열 내용 및 데이터 형식 지정** 페이지에서 **검색** 을 클릭 하 여 각 열에 대 한 기본 데이터 및 내용 유형을 결정 하는 알고리즘을 실행 합니다.  
  
2.  **내용 유형** 및 **데이터 형식** 열의 항목을 검토 하 고 필요한 경우 변경 하 여 설정이 다음 표에 나열 된 것과 동일한 지 확인 합니다.  
  
     일반적으로 마법사는 숫자를 검색하고 적절한 숫자 데이터 형식을 할당하지만 사용자가 숫자를 텍스트로 처리하려는 경우도 많이 있습니다. 예를 들어 **Geographykey** 는이 식별자에 대 한 수치 연산을 수행 하기에 적합 하지 않으므로 텍스트로 처리 되어야 합니다.  
  
    |열|콘텐츠 형식|데이터 형식|  
    |------------|------------------|---------------|  
    |**주소 줄 1**|**불연속**|**본문**|  
    |**주소 Line2**|**불연속**|**본문**|  
    |**발전할**|**연속**|**Long**|  
    |**Bike Buyer**|**불연속**|**Long**|  
    |**Commute 거리**|**불연속**|**본문**|  
    |**CustomerKey**|**Key**|**Long**|  
    |**DateLastPurchase**|**연속**|**Date**|  
    |**전자 메일 주소**|**불연속**|**본문**|  
    |**English Education**|**불연속**|**본문**|  
    |**English Occupation**|**불연속**|**본문**|  
    |**FirstName**|**불연속**|**본문**|  
    |**구분**|**불연속**|**본문**|  
    |**Geography Key**|**불연속**|**본문**|  
    |**House Owner Flag**|**불연속**|**본문**|  
    |**성**|**불연속**|**본문**|  
    |**결혼 상태**|**불연속**|**본문**|  
    |**Number Cars Owned**|**불연속**|**Long**|  
    |**Number Children At Home**|**불연속**|**Long**|  
    |**지역**|**불연속**|**본문**|  
    |**Total Children**|**불연속**|**Long**|  
    |**Yearly Income**|**연속**|**Double**|  
  
3.  **다음**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [구조 &#40;기본 데이터 마이닝 자습서에 대 한 테스트 데이터 집합 지정&#41;](../../2014/tutorials/specifying-a-testing-data-set-for-the-structure-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [기본 데이터 마이닝 자습서를 &#40;타겟 메일링 마이닝 모델 구조 만들기&#41;](../../2014/tutorials/creating-a-targeted-mailing-mining-model-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝&#41;&#40;내용 유형](../../2014/analysis-services/data-mining/content-types-data-mining.md)   
 [데이터 마이닝 &#40;데이터 형식&#41;](../../2014/analysis-services/data-mining/data-types-data-mining.md)  
  
  
