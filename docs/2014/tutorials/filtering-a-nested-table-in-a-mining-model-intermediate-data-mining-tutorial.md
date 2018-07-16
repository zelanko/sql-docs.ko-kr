---
title: 마이닝 모델 (중급 데이터 마이닝 자습서)에 중첩된 테이블 필터링 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0a3ae0e5-897b-4898-a60d-5455eec3d305
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d39ec6f60a9d281f6e1a76f26da585b555066dcc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273799"
---
# <a name="filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial"></a>마이닝 모델의 중첩 테이블 필터링(중급 데이터 마이닝 자습서)
  모델을 만들고 탐색한 후 고객 데이터의 하위 집합에 초점을 맞추기로 결정합니다. 예를 들어 특정 항목을 포함하는 바구니만 분석하거나 특정 기간 동안 아무 것도 구매하지 않은 고객에 대한 인구 통계를 분석할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 마이닝 모델에 사용되는 데이터를 필터링하는 기능을 제공합니다. 이 기능은 새 데이터 원본 뷰를 다른 데이터를 사용 하도록 설정 해야 하기 때문에 유용 합니다. 기본 데이터 마이닝 자습서에서는 사례 테이블에 조건을 적용하여 플랫 테이블의 데이터를 필터링하는 방법을 배웠습니다. 이 태스크에서는 중첩 테이블에 적용되는 필터를 만듭니다.  
  
## <a name="filters-on-nested-vs-case-tables"></a>중첩 테이블 및 사례 테이블에 대한 필터  
 Association 모델에 사용되는 데이터 원본 뷰와 같이 데이터 원본 뷰에 사례 테이블 및 중첩 테이블이 포함되어 있는 경우 사례 테이블의 값, 중첩 테이블에서의 값 존재 여부 또는 이 둘을 조합한 조건을 기준으로 필터링할 수 있습니다.  
  
 이 태스크에서는 먼저 Association 모델의 복사본을 만든 다음 사례 테이블에서 IncomeGroup 및 Region 특성을 기준으로 필터링할 수 있도록 해당 특성을 새 관련 모델에 추가합니다.  
  
#### <a name="to-create-and-modify-a-copy-of-the-association-model"></a>Association 모델의 복사본을 만들고 수정하려면  
  
1.  에 **마이닝 모델** 탭 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 마우스 오른쪽 단추로 클릭 합니다 `Association` 모델을 선택한 **새 마이닝 모델**.  
  
2.  에 대 한 **Model Name**, 형식 `Association Filtered`합니다. 에 대 한 **알고리즘 이름**를 선택 **Microsoft 연결 규칙**합니다. **확인**을 클릭합니다.  
  
3.  Association Filtered 모델에 대 한 열에서 IncomeGroup 행을 클릭 하 고 값에서 변경 **무시** 하 **입력**합니다.  
  
 다음으로 새 연결 모델의 사례 테이블에 대한 필터를 만듭니다. 모델에서 대상 지역에 있거나 대상 소득 수준을 가진 고객만 필터를 통과하게 됩니다. 그런 다음 두 번째 필터 조건 집합을 추가하여 시장 바구니에 하나 이상의 항목이 포함된 고객만 모델에 사용되도록 지정합니다.  
  
#### <a name="to-add-a-filter-to-a-mining-model"></a>마이닝 모델에 필터를 추가하려면  
  
1.  에 **마이닝 모델** 탭, Association Filtered 모델을 마우스 오른쪽 단추로 **모델 필터 설정**합니다.  
  
2.  **모델 필터** 대화 상자의 **마이닝 구조 열** 입력란에서 표의 첫 행을 클릭합니다.  
  
3.  에 **마이닝 구조 열** 입력란에서 IncomeGroup 선택 합니다.  
  
     입력란 왼쪽에 있는 아이콘이 변경되어 선택한 항목이 열임을 나타냅니다.  
  
4.  클릭 합니다 **연산자** 입력란을 선택 합니다 **=** 목록에서 연산자.  
  
5.  클릭 합니다 **값** 텍스트 상자 및 형식 `High` 상자에서.  
  
6.  표에서 다음 행을 클릭합니다.  
  
7.  클릭 합니다 **및/또는** 표 형태 창 및 선택의 다음 행에서 입력란 **또는**합니다.  
  
8.  에 **마이닝 구조 열** 입력란에서 IncomeGroup 선택 합니다. 에 **값** 텍스트 상자에서 `Moderate`합니다.  
  
     만든 필터 조건이 자동으로 추가 됩니다는 **식** 입력란 및 다음과 같이 나타납니다.  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate'`  
  
9. 기본적으로 연산자에서 나가는 표의 다음 행을 클릭 **AND**합니다.  
  
10. 에 대 한 **연산자**, 기본값을 그대로 두고 **Contains**합니다. 클릭 합니다 **값** 입력란입니다.  
  
11. 에 **필터** 대화 상자의 첫 번째 행에서 **마이닝 구조 열**선택, `Model`합니다.  
  
12. 에 대 한 **연산자**를 선택 **IS NOT NULL**합니다. 유지 된 **값** 입력란을 비워 합니다. **확인**을 클릭합니다.  
  
     필터 조건에는 **식** 텍스트 상자를 **모델 필터** 대화 상자의 중첩된 테이블에 새 조건을 포함 하도록 자동으로 업데이트 됩니다. 전체 식은  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate' AND EXISTS SELECT * FROM [vAssocSeqLineItems] WHERE [Model] <> NULL).`  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)] ``  
  
#### <a name="to-enable-drillthrough-and-to-process-the-filtered-model"></a>드릴스루를 사용하고 필터링된 모델을 처리하려면  
  
1.  에 **마이닝 모델** 탭을 마우스 오른쪽 단추로 클릭 합니다 `Association Filtered` 모델을 선택한 **속성**합니다.  
  
2.  변경 된 **AllowDrillThrough** 속성을 **True**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 합니다 `Association Filtered` 선택한 마이닝 모델을 **프로세스 모델**합니다.  
  
4.  클릭 **Yes** 새 모델을 배포 하려면 오류 메시지에는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스입니다.  
  
5.  에 **마이닝 구조 처리** 대화 상자, 클릭 **실행**합니다.  
  
6.  처리가 완료 되 면 클릭 **닫기** 종료 합니다 **처리 진행률** 대화 상자를 클릭 **닫기** 종료를 다시는 **마이닝 구조 처리**  대화 상자.  
  
 Microsoft 일반 콘텐츠 트리 뷰어를 사용하여 NODE_SUPPORT에 대한 값을 확인함으로써 필터링된 모델에 원래 모델보다 적은 사례가 포함되어 있음을 확인할 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 방금 만든 중첩 테이블 필터는 중첩 테이블에 하나 이상의 행이 있는지 여부만 확인하지만 특정 제품이 있는지 여부를 확인하는 필터 조건을 만들 수도 있습니다.  예를 들어 다음과 같은 필터를 만들 수 있습니다.  
  
```  
[IncomeGroup] = 'High' AND  
 EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] = 'Water Bottle' )   
```  
  
 이 문은 사례 테이블의 고객을 물병을 구매한 고객으로만 제한함을 의미합니다. 그러나 중첩 테이블 특성의 수는 잠재적으로 제한이 없기 때문에 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 선택 가능한 값 목록을 제공하지 않습니다. 대신 정확한 값을 입력해야 합니다.  
  
 클릭할 수 **쿼리 편집** 필터 식을 수동으로 변경 합니다. 그러나 필터 식의 임의 부분을 수동으로 변경하면 표가 비활성화되어 텍스트 편집 모드에서만 필터 식 작업을 수행할 수 있습니다. 표 편집 모드를 복원하려면 해당 필터 식을 지우고 다시 시작해야 합니다.  
  
> [!WARNING]  
>  중첩 테이블 필터에는 LIKE 연산자를 사용할 수 없습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [연결 예측 &#40;중급 데이터 마이닝 자습서&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>관련 항목  
 [모델 필터 구문 및 예제 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [마이닝 모델에 대 한 필터 &#40;Analysis Services-데이터 마이닝&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
