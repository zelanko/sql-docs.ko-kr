---
title: '1 단원: 시장 바구니 마이닝 구조 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a817c8d1-aff4-42b4-b194-ad9cc1c60f35
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a6a6e123e525512a72d70bcc8ca2eba549d1347e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62676272"
---
# <a name="lesson-1-creating-the-market-basket-mining-structure"></a>1단원: Market Basket 마이닝 구조 만들기
  이 단원에서는 고객이 동시에 구입하는 경향이 있는 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 제품을 예측할 수 있는 마이닝 구조를 만듭니다. 마이닝 구조 및 데이터 마이닝의 해당 역할에 익숙하지 않은 경우 [마이닝 구조 &#40;Analysis Services 데이터 마이닝&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)를 참조 하세요.  
  
 이 단원에서 만들 연결 마이닝 구조는 [Microsoft 연결 알고리즘](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)기반 마이닝 모델 추가 작업을 지원합니다. 이후 단원에서는 마이닝 모델을 사용하여 고객이 동시에 구입하는 경향이 있는 제품 유형을 예측합니다. 이를 시장 바구니 분석이라고 합니다. 예를 들어 고객이 산악 자전거, 자전거 타이어 및 헬멧을 동시에 구입하는 경향이 있음을 알게 될 수 있습니다.  
  
 이 단원에서는 중첩 테이블을 사용하여 마이닝 구조를 정의합니다. 구조에서 정의하는 데이터 도메인이 두 개의 다른 원본 테이블 내에 있으므로 중첩 테이블을 사용합니다. 중첩 테이블에 대 한 자세한 내용은 [데이터 마이닝&#41;Analysis Services &#40;중첩 테이블 ](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)을 참조 하십시오.  
  
## <a name="create-mining-structure-statement"></a>CREATE MINING STRUCTURE 문  
 중첩 테이블이 포함 된 마이닝 구조를 만들려면 [CREATE 마이닝 structure &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx) 문을 사용 합니다. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
-   구조 이름 지정  
  
-   키 열 정의  
  
-   마이닝 열 정의  
  
-   중첩 테이블 열 정의  
  
 다음은 CREATE MINING STRUCTURE 문의 일반적인 예입니다.  
  
```  
CREATE MINING STRUCTURE [<Mining Structure Name>]  
(  
   <key column>,  
   <mining structure columns>,  
   <table columns>  
   (  <nested key column>,  
      <nested mining structure columns> )  
)  
  
```  
  
 코드의 첫 번째 줄에서는 구조의 이름을 정의합니다.  
  
```  
CREATE MINING STRUCTURE [Mining Structure Name]  
```  
  
 DMX에서 개체의 이름을 지정 하는 방법에 대 한 자세한 내용은 [id &#40;dmx&#41;](/sql/dmx/identifiers-dmx)를 참조 하세요.  
  
 코드의 다음 줄에서는 원본 데이터의 엔터티를 고유하게 식별하는 마이닝 구조에 대한 키 열을 정의합니다.  
  
```  
<key column>  
```  
  
 코드의 다음 줄은 마이닝 구조와 연결된 마이닝 모델에서 사용할 마이닝 열을 정의하는 데 사용됩니다.  
  
```  
<mining structure columns>  
```  
  
 코드의 다음 줄에서는 중첩 테이블 열을 정의합니다.  
  
```  
<table columns>  
(  <nested key column>,  
   <nested mining structure columns> )  
```  
  
 정의할 수 있는 마이닝 구조 열 유형에 대한 자세한 내용은 [Mining Structure Columns](../../2014/analysis-services/data-mining/mining-structure-columns.md)을 참조하십시오.  
  
> [!NOTE]  
>  기본적으로 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서는 각 마이닝 구조에 대해 30%의 홀드아웃 데이터 집합을 만들지만 DMX를 사용하여 마이닝 구조를 만들 때 필요한 경우 홀드아웃 데이터 집합을 수동으로 추가해야 합니다.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   비어 있는 새 쿼리 만들기  
  
-   마이닝 구조를 만들기 위해 쿼리 변경  
  
-   쿼리 실행  
  
## <a name="creating-the-query"></a>쿼리 만들기  
 첫 번째 단계는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결하고 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 새 DNX 쿼리를 만드는 것입니다.  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>SQL Server Management Studio에서 새 DMX 쿼리를 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  **서버에 연결** 대화 상자에서 **서버 유형**으로 **Analysis Services**를 선택합니다. **서버 이름**,를 입력 `LocalHost`하거나이 단원에서 연결할 인스턴스의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이름을 입력 합니다. **연결**을 클릭합니다.  
  
3.  **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **DMX**를 클릭합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
## <a name="altering-the-query"></a>쿼리 변경  
 다음 단계는 Market Basket 마이닝 구조를 만들기 위해 위에서 설명한 CREATE MINING STRUCTURE 문을 수정하는 것입니다.  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>CREATE MINING STRUCTURE 문을 사용자 지정하려면  
  
1.  쿼리 편집기에서 CREATE MINING STRUCTURE 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
2.  다음 내용을  
  
    ```  
    [mining structure name]   
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    [Market Basket]  
    ```  
  
3.  다음 내용을  
  
    ```  
    <key column>  
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    OrderNumber TEXT KEY  
    ```  
  
4.  다음 내용을  
  
    ```  
    <table columns>  
    (  <nested key column>,  
       <nested mining structure columns> )  
    ```  
  
     다음으로 바꿉니다.  
  
    ```  
    [Products] TABLE (  
        [Model] TEXT KEY  
    )  
    ```  
  
     TEXT KEY 언어는 Model 열이 중첩 테이블에 대한 키 열임을 지정합니다.  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    CREATE MINING STRUCTURE [Market Basket] (  
        OrderNumber TEXT KEY,  
        [Products] TABLE (  
            [Model] TEXT KEY  
        )  
    )  
    ```  
  
5.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
6.  다른 이름 **으로 저장** 대화 상자에서 해당 폴더로 이동한 다음 파일 `Market Basket Structure.dmx`이름을로 합니다.  
  
## <a name="executing-the-query"></a>쿼리 실행  
 마지막 단계는 쿼리를 실행하는 것입니다. 쿼리를 만들어 저장한 다음 서버에 마이닝 구조를 만들려면 해당 쿼리를 실행해야 합니다. 즉, 해당 문을 실행해야 합니다. 쿼리 편집기에서 쿼리를 실행 하는 방법에 대 한 자세한 내용은 [데이터베이스 엔진 쿼리 편집기 &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)를 참조 하세요.  
  
#### <a name="to-execute-the-query"></a>쿼리를 실행하려면  
  
-   쿼리 편집기의 도구 모음에서 **실행**을 클릭합니다.  
  
     문의 실행이 끝나면 쿼리 상태가 쿼리 편집기 아래쪽의 **메시지** 탭에 표시됩니다. 메시지는 다음과 같아야 합니다.  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     이제 **Market Basket** 이라는 새 구조가 서버에 있습니다.  
  
 다음 단원에서는 방금 만든 Market Basket 마이닝 구조에 마이닝 모델을 추가합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [2단원: Market Basket 마이닝 구조에 마이닝 모델 추가](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
  
  
