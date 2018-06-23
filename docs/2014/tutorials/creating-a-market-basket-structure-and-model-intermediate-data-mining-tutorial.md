---
title: 시장 바구니 구조 및 모델 (중급 데이터 마이닝 자습서) 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 659b7a4e-f687-44d9-a60a-86490ccbf90f
caps.latest.revision: 48
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 957a55114e5a4fb756c63b63779eed3fbfb5f95b
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312601"
---
# <a name="creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial"></a>시장 바구니 구조 및 모델 만들기(중급 데이터 마이닝 자습서)
  데이터 원본 뷰를 만들었으므로 이제 데이터 마이닝 마법사를 사용하여 새 마이닝 구조를 만듭니다. 이 태스크에서는 [!INCLUDE[msCoName](../includes/msconame-md.md)] 연결 알고리즘을 기반으로 하는 마이닝 구조 및 마이닝 모델을 만듭니다.  
  
> [!NOTE]  
>  vAssocSeqLineItems를 중첩 테이블로 사용할 수 없다는 오류가 발생하면 이 단원의 이전 태스크로 돌아가 vAssocSeqLineItems 테이블(다측)에서 vAssocSeqOrders 테이블(일측)로 끄는 방법으로 다 대 일 조인을 만들어야 합니다. 조인 선을 마우스 오른쪽 단추로 클릭하여 테이블 간의 관계를 편집할 수도 있습니다.  
  
### <a name="to-create-an-association-mining-structure"></a>연결 마이닝 구조를 만들려면  
  
1.  솔루션 탐색기에서 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 마우스 오른쪽 단추로 클릭 **Mining Structures** 선택 **새 마이닝 구조** 데이터 마이닝 마법사를 엽니다.  
  
2.  **데이터 마이닝 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  에 **정의 방법 선택** 페이지에서 **기존 관계형 데이터베이스 또는 데이터 웨어하우스에서** 을 선택한 다음 클릭 **다음**합니다.  
  
4.  에 **데이터 마이닝 구조 만들기** 페이지의 **사용할 데이터 마이닝 기술을 사용 하 시겠습니까?** 선택, **Microsoft 연결 규칙** 클릭 한 다음 확인 하 고 목록에서 **다음**합니다. **데이터 원본 뷰 선택** 페이지가 나타납니다.  
  
5.  선택 **Orders**아래 **사용 가능한 데이터 원본 뷰**, 클릭 하 고 **다음**합니다.  
  
6.  에 **테이블 유형 지정** vAssocSeqLineItems 테이블에 대 한 행에서 페이지를 선택는 **Nested** 확인란을 선택한 중첩된 테이블 vAssocSeqOrders에 대 한 행을 선택 하 고 **대/소문자** 확인란 합니다. **다음**을 클릭합니다.  
  
7.  에 **학습 데이터 지정** 페이지에서 선택 되어 있는 모든 상자의 선택을 취소 합니다. 선택 하 여 사례 테이블 vAssocSeqOrders에에 대 한 키를 설정의 **키** OrderNumber 옆에 있는 확인란 합니다.  
  
     시장 바구니 분석의 목적은 단일 트랜잭션에 포함 되는 제품을 결정 하는 것을 하기 때문에 사용할 필요가 없습니다는 **CustomerKey** 필드입니다.  
  
8.  선택 하 여 중첩된 테이블 vAssocSeqLineItems에 대 한 키를 설정의 **키** 모델 옆에 있는 확인란입니다. **입력** 도 자동으로 선택 되어이 작업을 수행 합니다. 선택 된 **예측 가능** 에 대 한 확인란 `Model` 도 합니다.  
  
     따라서를 포함 하지 않아야 하 고 시장 바구니 모델에서는 시장 바구니의 제품 시퀀스가 중요 하지 않은 **LineNumber** 중첩 테이블 키로 합니다. 사용 하 여 **LineNumber** 순서는 중요 한 모델에만 키로 합니다. 4단원에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] 시퀀스 클러스터링 알고리즘을 사용하는 모델을 만듭니다.  
  
9. IncomeGroup 및 Region 왼쪽의 확인란을 선택하고 다른 항목은 선택하지 않습니다. 맨 왼쪽 열의 확인란을 선택하면 나중에 참조할 수 있도록 해당 열이 구조에 추가되지만 모델에 사용되지는 않습니다. 선택 항목은 다음과 같습니다.  
  
     ![대화 상자 모양](../../2014/tutorials/media/tutorial-configassocmodel.gif "대화 상자의 모양")  
  
10. **다음**을 클릭합니다.  
  
11. 에 **지정 열 내용 및 데이터 형식**페이지에서 다음 표에 나와 있는 것 처럼 고 해야 클릭 하 고 선택 항목 검토 **다음**합니다.  
  
    |열|내용 유형|데이터 형식|  
    |-------------|------------------|---------------|  
    |IncomeGroup|불연속|텍스트 모드|  
    |Order Number|Key|텍스트 모드|  
    |Region|불연속|텍스트 모드|  
    |vAssocSeqLineItems|||  
    |Model|Key|텍스트 모드|  
  
12. 에 **테스트 설정 만들기** 페이지 옵션에 대 한 기본값 **테스트용 데이터 비율** 은 30%입니다. 이를 변경 **0**합니다. **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 모델 정확도를 측정하는 여러 다른 차트를 제공합니다. 그러나 리프트 차트 및 교차 유효성 검사 보고서와 같은 일부 정확도 차트 유형은 분류 및 추정용으로 디자인되었으며 연결 예측에 대해서는 지원되지 않습니다.  
  
13. 에 **마법사 완료** 페이지 **마이닝 구조 이름**, 형식 `Association`합니다.  
  
14. **마이닝 모델 이름**, 형식 `Association`합니다.  
  
15. 옵션을 선택 **드릴스루 허용**, 클릭 하 고 **마침**합니다.  
  
     데이터 마이닝 디자이너가 열리고 표시 하는 `Association` 방금 만든 마이닝 구조입니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [시장 바구니 모델 수정 및 처리 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 연결 알고리즘](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [콘텐츠 형식을 &#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/content-types-data-mining.md)  
  
  