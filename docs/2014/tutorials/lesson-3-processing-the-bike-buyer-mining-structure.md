---
title: '3단원: Bike Buyer 마이닝 구조 처리 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e748c2cd-339d-4e82-82f1-be2d0fc41b61
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2e3f85016b32884b9a6b809e28d20d9985f97cd9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025334"
---
# <a name="lesson-3-processing-the-bike-buyer-mining-structure"></a>3단원: Bike Buyer 마이닝 구조 처리
  이 단원에서는 사용 하 여 INSERT INTO 문과의 vTargetMail 뷰를 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 샘플 데이터베이스에서 만든 마이닝 모델과 마이닝 구조를 처리 하는 데 [1 단원: Bike Buyer 마이닝 구조를 만드는](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md) 고 [2 단원: Bike Buyer 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)합니다.  
  
 마이닝 구조를 처리하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 원본 데이터를 읽은 다음 마이닝 모델을 지원하는 구조를 작성합니다. 마이닝 모델을 처리하면 마이닝 구조에서 정의한 데이터가 사용자가 선택한 데이터 마이닝 알고리즘을 통해 전달됩니다. 이 알고리즘에서는 경향 및 패턴을 검색한 다음 마이닝 모델에 이 정보를 저장합니다. 따라서 마이닝 모델은 실제 원본 데이터 대신 알고리즘에서 발견한 정보를 포함합니다. 마이닝 모델을 처리 하는 방법에 대 한 자세한 내용은 참조 하세요. [처리 요구 사항 및 고려 사항 &#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)합니다.  
  
 구조 열이나 원본 데이터를 변경하는 경우에만 마이닝 구조를 다시 처리하면 됩니다. 이미 처리된 마이닝 구조에 마이닝 모델을 추가하는 경우에는 INSERT INTO MINING MODEL 문을 사용하여 새 마이닝 모델을 학습합니다.  
  
## <a name="train-structure-template"></a>구조 템플릿의 학습  
 마이닝 구조 및 연결된 된 마이닝 모델을 학습 하기 위해 사용 합니다 [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) 문입니다. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
-   마이닝 구조 식별  
  
-   마이닝 구조의 열 나열  
  
-   학습 데이터 정의  
  
 다음은 INSERT INTO 문의 일반적인 예입니다.  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 코드의 첫 번째 줄에서는 학습할 마이닝 구조를 식별합니다.  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 코드의 다음 줄에서는 마이닝 구조에서 정의한 열을 지정합니다. 마이닝 구조의 각 열을 나열해야 하며 각 열을 원본 쿼리 데이터 내에 포함된 열에 매핑해야 합니다.  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 코드의 마지막 줄에서는 마이닝 구조의 학습에 사용할 데이터를 정의합니다.  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 이 단원에서는 `OPENQUERY`를 사용하여 원본 데이터를 정의합니다. 원본 쿼리를 정의 하는 다른 방법에 대 한 정보를 참조 하세요 [ &#60;원본 데이터 쿼리&#62;](/sql/dmx/source-data-query)합니다.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   Bike Buyer 마이닝 구조 처리  
  
## <a name="processing-the-predictive-mining-structure"></a>예측 마이닝 구조 처리  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>INSERT INTO를 사용하여 마이닝 구조를 처리하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  INSERT INTO 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    [<mining structure name>]   
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    Bike Buyer  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining structure columns>  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [Customer Key],  
    [Age],  
    [Bike Buyer],  
    [Commute Distance],  
    [Education],  
    [Gender],  
    [House Owner Flag],  
    [Marital Status],  
    [Number Cars Owned],  
    [Number Children At Home],  
    [Occupation],  
    [Region],  
    [Total Children],  
    [Yearly Income]  
    ```  
  
5.  다음 내용을  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
     OPENQUERY 문은 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 데이터 원본을 참조하여 vTargetMail 뷰에 액세스합니다. 이 뷰에는 마이닝 모델의 학습에 사용할 원본 데이터가 포함되어 있습니다.  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    INSERT INTO MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key],  
       [Age],  
       [Bike Buyer],  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]     
    )  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
6.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
7.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Process Bike Buyer Structure.dmx`입니다.  
  
8.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
 다음 단원에서는 이 단원에서 마이닝 구조에 추가한 마이닝 모델의 내용을 탐색합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [4단원: Bike Buyer 마이닝 모델 찾아보기](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
  
  
