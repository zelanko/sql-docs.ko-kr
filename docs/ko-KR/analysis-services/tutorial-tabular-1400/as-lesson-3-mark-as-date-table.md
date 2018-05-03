---
title: 'Analysis Services 자습서 3 단원: 날짜 테이블로 표시 | Microsoft Docs'
description: Analysis Services tutorial 프로젝트의 날짜 테이블을 표시 하는 방법에 설명 합니다.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 8d15495ef5c1fdfe4150990f5ca24e022b4fe05a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mark-as-date-table"></a>날짜 테이블로 표시

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

2 단원: 데이터 가져오기 가져온 명명 된 차원 테이블 **DimDate**합니다. 모델에서이 테이블의 이름이 DimDate 인 동안 것 수 라고도 *날짜 테이블*날짜 및 시간 데이터를 포함 하는, 합니다.  
  
포함 하는 속성을 지정 해야 나중 측정값을 만들 때와 같은 DAX 시간 인텔리전스 함수를 사용할 때마다 한 *날짜 테이블* 및 고유 식별자 *날짜 열* 해당 테이블의 합니다.
  
이 단원에서는 표시는 **DimDate** 으로 테이블는 *날짜 테이블* 및 **날짜** (테이블 열에 날짜)으로 *날짜 열* (고유 식별자)입니다.  

날짜 테이블 및 날짜 열을 표시 하기 전에 모델을 더 쉽게 이해할 수를 약간 정리 작업을 수행 하는 것이 좋습니다. DimDate 테이블에서 명명 된 열을 알 **FullDateAlternateKey**합니다. 이 열은 테이블에 포함 된 각 calendar year의 모든 날에 대 한 하나의 행을 포함 합니다. 이 열을 너무 많이 측정값 수식에 및 사용 보고서에. 그러나 FullDateAlternateKey이이 열에 대 한 좋은 식별자 또 아닙니다. 파일 이름을 **날짜**, 쉽게 식별 하 고 수식에 포함 합니다. 가능 하면 항상 SSDT 및 클라이언트 보고 응용 프로그램을 식별 하기 쉽게 만들어에 테이블 및 열 같은 개체의 이름을 바꿀 것이 좋습니다. 
  
이 단원에 소요 시간 예상: **3 분**  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 문서는 순서 대로 완료 해야 하는 테이블 형식 모델링 자습서의 일부입니다. 이 단원의 태스크를 수행 하기 전에 완료 해야 이전 단원: [2 단원: 데이터 가져오기](../tutorial-tabular-1400/as-lesson-2-get-data.md)합니다. 

### <a name="to-rename-the-fulldatealternatekey-column"></a>FullDateAlternateKey 열 이름을 바꾸려면

1.  모델 디자이너에서 클릭 된 **DimDate** 테이블입니다.

2.  에 대 한 헤더를 두 번 클릭는 **FullDateAlternateKey** 열 다음에 이름을 **날짜**합니다.

  
### <a name="to-set-mark-as-date-table"></a>날짜 테이블로 표시 설정 방법  
  
1.  **Date** 열을 선택한 다음 **속성** 창의 **데이터 형식**에서  **날짜** 가 선택되어 있는지 확인합니다.  
  
2.  **테이블** 메뉴를 클릭한 다음 **Date**, **날짜 테이블로 표시**를 차례로 클릭합니다.  
  
3.  **날짜 테이블로 표시** 대화 상자의 **날짜** 목록 상자에서 **Date** 열을 고유 식별자로 선택합니다. 일반적으로 기본적으로 선택 됩니다. **확인**을 클릭합니다. 

    ![as-lesson3-date-table](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>다음 단계

[4 단원: 관계 만들기](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)합니다.
  
