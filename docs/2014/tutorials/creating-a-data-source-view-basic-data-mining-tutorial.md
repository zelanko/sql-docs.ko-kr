---
title: 데이터 원본 뷰 만들기 (기본 데이터 마이닝 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1e68a88-0f82-415d-becc-78d180d4f845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ac7730e8437eaed304ed69c40e45fc93ee9b5531
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68888644"
---
# <a name="creating-a-data-source-view-basic-data-mining-tutorial"></a>데이터 원본 뷰 만들기(기본 데이터 마이닝 자습서)
  데이터 원본 뷰는 데이터 원본을 기반으로 하고, 마이닝 구조에 사용할 수 있는 데이터 하위 집합을 정의합니다. 데이터 원본 뷰를 사용하여 열을 추가하고 계산 열 및 집계를 만들고 명명된 뷰를 추가할 수도 있습니다. 데이터 원본 뷰를 사용하면 원래 데이터 원본을 수정하지 않고도 프로젝트와 관련된 테이블을 선택하고 테이블 간의 관계를 설정하며 데이터 구조를 수정할 수 있습니다. 자세한 내용은 [다차원 모델의 데이터 원본 뷰](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)를 참조하세요.  
  
### <a name="to-create-a-data-source-view"></a>데이터 원본 뷰를 만들려면  
  
1.  **솔루션 탐색기**에서 **데이터 원본 뷰**를 마우스 오른쪽 단추로 클릭하고 **새 데이터 원본 뷰**를 선택합니다.  
  
2.  **데이터 원본 뷰 마법사 시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **데이터 원본 선택** 페이지의 **관계형 데이터 원본**아래에서 이전 태스크에서 만든 Adventure Works DW 2012 데이터 원본을 선택합니다. **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  데이터 원본을 만들려면 **데이터 원본** 을 마우스 오른쪽 단추로 클릭하고 **새 데이터 원본** 을 클릭하여 데이터 원본 마법사를 시작합니다.  
  
4.  **테이블 및 뷰 선택** 페이지에서 다음 개체를 선택하고 오른쪽 화살표를 클릭하여 새 데이터 원본 뷰에 포함합니다.  
  
    -   **ProspectiveBuyer (dbo)** - 잠재 자전거 구매 고객의 테이블  
  
    -   **vTargetMail (dbo)** - 자전거 구매 고객에 대한 기록 데이터의 뷰  
  
5.  **다음**을 클릭합니다.  
  
6.  **마법사 완료** 페이지에서는 기본적으로 데이터 원본 뷰의 이름이 Adventure Works DW 2012로 지정되어 있습니다. 이름을로 `Targeted Mailing`변경 하 고 **마침**을 클릭 합니다.  
  
     **Targeted Mailing.dsv [디자인]** 탭에 새 데이터 원본 뷰가 열립니다.  
  
## <a name="previous-task-in-lesson"></a>단원의 이전 태스크  
 [기본 데이터 마이닝 &#40;데이터 원본 만들기 자습서&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>다음 단원  
 [2 단원: 기본 데이터 마이닝 자습서 &#40;대상 메일링 구조 구축&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 원본 뷰 정의&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/defining-a-data-source-view-analysis-services)  
  
  
