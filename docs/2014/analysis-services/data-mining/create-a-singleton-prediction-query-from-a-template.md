---
title: 템플릿에서 단일 예측 쿼리 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- singleton query predictions [DMX]
ms.assetid: e0a68ab0-bece-4d25-b464-47f1719302e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6bcd9aa80170719a32ff3bf75f0ac36dc83cf021
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399780"
---
# <a name="create-a-singleton-prediction-query-from-a-template"></a>템플릿에서 단일 예측 쿼리 작성
  단일 쿼리는 모델을 예측에 사용 하려고 하지만 외부 입력된 데이터 집합에 매핑하거나 대량 예측을 수행 하지 않으려는 경우에 유용 합니다. 단일 쿼리를 사용하면 모델에 값을 제공하고 바로 예측된 값을 볼 수 있습니다.  
  
 예를 들어 다음 DMX 쿼리는 타겟 메일링 모델인 TM_Decision_Tree에 대한 단일 쿼리를 나타냅니다.  
  
```  
SELECT * FROM [TM_Decision_tree] ;  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 다음 절차에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 템플릿 탐색기를 사용하여 이 쿼리를 빠르게 만드는 방법을 설명합니다.  
  
### <a name="to-open-the-analysis-services-templates-in-sql-server-management-studio"></a>SQL Server Management Studio에서 Analysis Services 템플릿을 열려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **템플릿 탐색기**를 클릭합니다.  
  
2.  큐브 아이콘을 클릭하여 **Analysis Services**템플릿을 엽니다.  
  
### <a name="to-open-a-prediction-query-template"></a>예측 쿼리 템플릿을 열려면  
  
1.  **템플릿 탐색기**의 Analysis Server 템플릿 목록에서 **DMX**, **예측 쿼리**를 차례로 확장합니다.  
  
2.  **단일 예측**을 두 번 클릭합니다.  
  
3.  **Analysis Services에 연결** 대화 상자에서 쿼리할 마이닝 모델을 포함하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 있는 서버의 이름을 입력합니다.  
  
4.  **연결**을 클릭합니다.  
  
5.  데이터 마이닝 함수 및 데이터 마이닝 구조/관련 모델 목록을 포함하는 마이닝 모델 개체 브라우저와 함께 템플릿이 지정 데이터베이스에서 열립니다.  
  
### <a name="to-customize-the-singleton-query-template"></a>단일 쿼리 템플릿을 사용자 지정하려면  
  
1.  템플릿에서 **사용 가능한 데이터베이스** 드롭다운 목록을 클릭한 다음 목록에서 Analysis Services 인스턴스를 선택합니다.  
  
2.  **마이닝 모델** 목록에서 쿼리할 마이닝 모델을 선택합니다.  
  
     마이닝 모델의 열 목록이 개체 브라우저의 **메타데이터** 창에 나타납니다.  
  
3.  **쿼리** 메뉴에서 **템플릿 매개 변수 값 지정**을 선택합니다.  
  
4.  **select list** 행에 *를 입력하여 모든 열을 반환하거나 쉼표로 구분된 열과 식의 목록을 입력하여 특정 열을 반환합니다.  
  
     *를 입력하는 경우 6단계에서 새 값을 제공하는 열과 함께 예측 가능한 열이 반환됩니다.  
  
     이 항목의 시작 부분에 표시된 샘플 코드의 경우 **select list** 행이 *로 설정되었습니다.  
  
5.  **mining model** 행에 **개체 탐색기**에 나타나는 마이닝 모델 목록에 있는 마이닝 모델의 이름을 입력합니다.  
  
     이 항목의 시작 부분에 표시 된 샘플 코드는 **마이닝 모델** 행 이름에 설정 된 `TM_Decision_Tree`합니다.  
  
6.  **value** 행에 예측을 수행할 새 데이터 값을 입력합니다.  
  
     이 항목의 시작 부분에 표시 된 샘플 코드는 **값** 행으로 설정 된 `2` 자전거 구매 양상을 자녀 수를 기준으로 예측을 합니다.  
  
7.  **column** 행에 새 데이터가 매핑되어야 하는 마이닝 모델의 열 이름을 입력합니다.  
  
     이 항목의 시작 부분에 표시 된 샘플 코드는 **열** 행으로 설정 된 `Number Children at Home`합니다.  
  
    > [!NOTE]  
    >  **템플릿 매개 변수 값 지정** 대화 상자를 사용할 때는 열 이름을 대괄호로 묶을 필요가 없습니다. 대괄호는 자동으로 추가됩니다.  
  
8.  유지 된 **입력된 별칭** 으로 `t`입니다.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 쿼리 텍스트 창에서 구문 오류를 나타내는 쉼표 및 줄임표 아래의 빨간색 물결 기호를 찾습니다. 줄임표를 삭제하고 원하는 쿼리 조건을 추가합니다. 다른 조건을 추가하지 않는 경우 쉼표를 삭제합니다.  
  
     이 항목의 시작 부분에 표시된 예제 코드의 경우 추가 쿼리 조건이 `'45' as [Age]`로 설정되었습니다.  
  
11. **실행**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [예측 만들기&#40;기본 데이터 마이닝 자습서&#41;](../../tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
  
