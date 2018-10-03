---
title: '3 단원: Market Basket 마이닝 구조 처리 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 979738186c9af128087049e71fa248d41fd27b50
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192253"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>3단원: Market Basket 마이닝 구조 처리
  이 단원에서는 사용할 합니다 [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) 문을 vAssocSeqLineItems 및 vAssocSeqOrders를 합니다 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 샘플 데이터베이스를 처리할 마이닝 구조 및 마이닝 모델을 만든 [1 단원: Market Basket 마이닝 구조 만들기](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md) 하 고 [Lesson 2: Adding Mining Models to Market Basket 마이닝 구조](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)합니다.  
  
 마이닝 구조를 처리하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 원본 데이터를 읽은 다음 마이닝 모델을 지원하는 구조를 작성합니다. 마이닝 모델을 처리하면 마이닝 구조에서 정의한 데이터가 사용자가 선택한 데이터 마이닝 알고리즘을 통해 전달됩니다. 이 알고리즘에서는 경향 및 패턴을 검색한 다음 마이닝 모델에 이 정보를 저장합니다. 따라서 마이닝 모델은 실제 원본 데이터 대신 알고리즘에서 발견한 정보를 포함합니다. 마이닝 모델을 처리 하는 방법에 대 한 자세한 내용은 참조 하세요. [처리 요구 사항 및 고려 사항 &#40;데이터 마이닝&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)합니다.  
  
 구조 열이나 원본 데이터를 변경하는 경우에만 마이닝 구조를 다시 처리하면 됩니다. 이미 처리된 마이닝 구조에 마이닝 모델을 추가하는 경우에는 `INSERT INTO MINING MODEL` 문을 사용하여 기존 데이터를 기반으로 새 마이닝 모델을 학습합니다.  
  
 Market Basket 마이닝 구조에 중첩 테이블이 있으므로 중첩 테이블 구조를 사용하여 학습할 마이닝 열을 정의하고 `SHAPE` 명령을 사용하여 원본 테이블에서 학습 데이터를 가져오는 쿼리를 정의해야 합니다.  
  
## <a name="insert-into-statement"></a>INSERT INTO 문  
 Market Basket 마이닝 구조 및 연결된 된 마이닝 모델을 학습 하기 위해 사용 합니다 [INSERT INTO &#40;DMX&#41; ](/sql/dmx/insert-into-dmx) 문입니다. 이 문의 코드는 다음 부분으로 나눌 수 있습니다.  
  
-   마이닝 구조 식별  
  
-   마이닝 구조의 열 나열  
  
-   `SHAPE`을 사용하여 학습 데이터 정의  
  
 다음은 `INSERT INTO` 문의 일반적인 예입니다.  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],'<nested SELECT statement>')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 코드의 첫 번째 줄에서는 학습할 마이닝 구조를 식별합니다.  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 코드의 다음 줄에서는 마이닝 구조에서 정의한 열을 지정합니다. 마이닝 구조의 각 열을 나열해야 하며 각 열을 원본 쿼리 데이터 내에 포함된 열에 매핑해야 합니다. `SKIP`을 사용하여 원본 데이터에는 있지만 마이닝 구조에는 없는 열을 무시할 수 있습니다. 사용 하는 방법에 대 한 자세한 내용은 `SKIP`를 참조 하세요 [삽입 &#40;DMX&#41;](/sql/dmx/insert-into-dmx).  
  
```  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
```  
  
 코드의 마지막 줄에서는 마이닝 구조의 학습에 사용할 데이터를 정의합니다. 원본 데이터가 두 개의 테이블에 포함되어 있으므로 `SHAPE`을 사용하여 테이블을 연결합니다.  
  
```  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],''<nested SELECT statement>'')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 이 단원에서는 `OPENQUERY`를 사용하여 원본 데이터를 정의합니다. 원본 데이터에서 쿼리를 정의 하는 다른 메서드에 대 한 정보를 참조 하세요 [ &#60;원본 데이터 쿼리&#62;](/sql/dmx/source-data-query)합니다.  
  
## <a name="lesson-tasks"></a>단원 태스크  
 이 단원에서는 다음 태스크를 수행합니다.  
  
-   Market Basket 마이닝 구조 처리  
  
## <a name="processing-the-market-basket-mining-structure"></a>Market Basket 마이닝 구조 처리  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>INSERT INTO를 사용하여 마이닝 구조를 처리하려면  
  
1.  **개체 탐색기**의 인스턴스를 마우스 오른쪽 단추로 클릭 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]를 가리킨 **새 쿼리**를 클릭 하 고 **DMX**합니다.  
  
     비어 있는 새 쿼리가 포함된 쿼리 편집기가 열립니다.  
  
2.  INSERT INTO 문의 일반적인 예를 빈 쿼리에 복사합니다.  
  
3.  다음 내용을  
  
    ```  
    [<mining structure>]  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    Market Basket  
    ```  
  
4.  다음 내용을  
  
    ```  
    <mining structure columns>  
    [<nested table>]  
    ( SKIP, <skipped column> )  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    [OrderNumber],  
    [Products]   
    (SKIP, [Model])  
    ```  
  
     구문 중 `Products`는 SHAPE 문에 의해 정의된 Products 테이블을 참조합니다. `SKIP`은 원본 데이터에 키로 존재하는 Model 열을 무시하는 데 사용되지만 마이닝 구조에서는 사용되지 않습니다.  
  
5.  다음 내용을  
  
    ```  
    SHAPE {  
      OPENQUERY([<datasource>],'<SELECT statement>') }  
    APPEND  
    (   
      {OPENQUERY([<datasource>],'<nested SELECT statement>')  
    }  
    RELATE [<case key>] TO [<foreign key>]  
    ) AS [<nested table>]  
    ```  
  
     다음 구문으로 바꿉니다.  
  
    ```  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
     원본 쿼리 참조를 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 에 정의 된 데이터 소스는 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 샘플 프로젝트입니다. 이 쿼리는 이 데이터 원본을 사용하여 vAssocSeqLineItems 및 vAssocSeqOrders 뷰에 액세스합니다. 이러한 뷰에는 마이닝 모델의 학습에 사용할 원본 데이터가 포함되어 있습니다. 이 프로젝트나 이러한 뷰를 만들지 않은 경우 [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md)합니다.  
  
     `SHAPE` 명령 내에서 `OPENQUERY`를 사용하여 두 개의 쿼리를 정의합니다. 첫 번째 쿼리는 부모 테이블을 정의하고 두 번째 쿼리는 중첩 테이블을 정의합니다. 이 두 개의 테이블은 두 테이블 모두에 있는 OrderNumber 열을 사용하여 연결됩니다.  
  
     이제 전체 문이 다음과 같아야 합니다.  
  
    ```  
    INSERT INTO MINING STRUCTURE [Market Basket]  
    (  
       [OrderNumber],[Products] (SKIP, [Model])  
    )  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
6.  **파일** 메뉴에서 **다른 이름으로 DMXQuery1.dmx 저장**을 클릭합니다.  
  
7.  에 **다른 이름으로 저장** 대화 상자에서 적절 한 폴더로 이동 하 고 파일 이름을 `Process Market Basket.dmx`입니다.  
  
8.  도구 모음에서 **실행** 단추를 클릭합니다.  
  
 쿼리 실행이 종료된 다음에는 찾은 패턴 및 항목 집합을 보고 연결을 보며 항목 집합, 확률 또는 중요도별로 필터링합니다. 이 정보를 보려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]데이터 모델의 이름을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **찾아보기**합니다.  
  
 다음 단원에서는 Market Basket 구조에 추가한 마이닝 모델을 기반으로 여러 예측을 만듭니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [4단원: Market Basket 예측 실행](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  
