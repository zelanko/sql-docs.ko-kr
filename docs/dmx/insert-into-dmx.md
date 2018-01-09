---
title: INSERT INTO (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INSERT INTO
- INSERT
- INSERT_INTO
dev_langs: DMX
helpviewer_keywords:
- SKIP (DMX)
- mapped model columns element
- source data query element
- <mapped model columns> element
- <source data query> element
- INSERT INTO statement
- mining models [Analysis Services], processing
- training mining models
- mining structures [DMX], processing
ms.assetid: 85eed207-396c-4a95-a74e-2acc1abc7e2c
caps.latest.revision: "49"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 70b2acdd5370be93f4fca9a5270a5b9951305248
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="insert-into-dmx"></a>INSERT INTO(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 데이터 마이닝 개체를 처리합니다. 마이닝 모델 및 마이닝 구조를 처리 하는 방법에 대 한 자세한 내용은 참조 [처리 요구 사항 및 고려 사항 &#40; 데이터 마이닝 &#41;](../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)합니다.  
  
 마이닝 구조가 지정된 경우 이 문은 마이닝 구조 및 연결된 모든 마이닝 모델을 처리합니다. 마이닝 모델이 지정된 경우 이 문은 마이닝 모델만 처리합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>인수  
 *모델*  
 모델 식별자입니다.  
  
 *구조*  
 구조 식별자입니다.  
  
 *매핑된 모델 열*  
 열 식별자 및 중첩 식별자의 쉼표로 구분된 목록입니다.  
  
 *원본 데이터 쿼리*  
 공급자가 정의한 형식의 원본 쿼리입니다.  
  
## <a name="remarks"></a>주의  
 지정 하지 않으면 **마이닝 모델** 또는 **마이닝 구조**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 이름 뒤에 개체 유형을 검색 하 고 올바른 개체를 처리 합니다. 서버에 이름이 서로 동일한 마이닝 구조 및 마이닝 모델이 있는 경우에는 오류가 반환됩니다.  
  
 두 번째 구문 형식 INSERT INTO를 사용 하 여*\<개체 >*합니다. COLUMN_VALUES, 데이터 모델을 학습 하지 않고 모델 열에 직접 삽입할 수 있습니다. 이렇게 하면 간결하게 정렬된 방식으로 모델에 열 데이터가 제공되므로 계층 구조나 정렬된 열이 포함된 데이터 집합으로 작업할 때 유용합니다.  
  
 사용 하는 경우 **INSERT INTO** 마이닝 모델 또는 마이닝 구조 및 오프 범위 밖으로는 \<매핑된 모델 열 > 및 \<원본 데이터 쿼리와 > 인수는 문 처럼 동작 **ProcessDefault**, 이미 존재 하는 바인딩을 사용 하 여 합니다. 바인딩이 없는 경우에는 오류가 반환됩니다. 에 대 한 자세한 내용은 **ProcessDefault**, 참조 [처리 옵션 및 설정 &#40; Analysis Services &#41; ](../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md). 다음 예에서는 구문을 보여 줍니다.  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 지정 하는 경우 **마이닝 모델** 매핑된 열과 원본 데이터 쿼리, 모델 및 관련된 구조 처리를 제공 합니다.  
  
 다음 표에서는 개체의 상태에 따라 여러 가지 형식의 문을 실행한 결과를 설명합니다.  
  
|인수를 제거합니다.|개체의 상태|결과|  
|---------------|----------------------|------------|  
|INSERT INTO MINING MODEL*\<모델 >*|마이닝 구조가 처리됩니다.|마이닝 모델이 처리됩니다.|  
||마이닝 구조가 처리되지 않습니다.|마이닝 모델 및 마이닝 구조가 처리됩니다.|  
||마이닝 구조에 추가 마이닝 모델이 포함되어 있습니다.|프로세스가 실패합니다. 마이닝 구조 및 연결된 마이닝 모델을 다시 처리해야 합니다.|  
|INSERT INTO MINING STRUCTURE*\<구조 >*|마이닝 구조가 처리되거나 처리되지 않습니다.|마이닝 구조 및 연결된 마이닝 모델이 처리됩니다.|  
|INSERT INTO MINING MODEL*\<모델 >* 원본 쿼리 포함<br /><br /> 로 구분하거나 여러<br /><br /> INSERT INTO MINING STRUCTURE*\<구조 >* 원본 쿼리 포함|마이닝 구조 또는 모델에 이미 내용이 포함되어 있습니다.|프로세스가 실패합니다. 사용 하 여이 작업을 수행 하기 전에 개체를 지워야 [delete&#40; DMX &#41;](../dmx/delete-dmx.md)합니다.|  
  
## <a name="mapped-model-columns"></a>매핑된 모델 열  
 사용 하 여는 \<매핑된 모델 열 > 요소를 마이닝 모델의 열에 데이터 원본의 열을 매핑할 수 있습니다. \<매핑된 모델 열 > 요소 형식은 다음과 같습니다.  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 사용 하 여 **SKIP**을 원본 쿼리에 있어야 하지만 마이닝 모델에 존재 하지 않는 특정 열을 제외할 수 있습니다. SKIP은 입력 행 집합에 포함된 열을 제어하지 못하는 경우 유용합니다. 고유의 OPENQUERY를 작성 중인 경우에는 SKIP을 사용하는 대신 SELECT 열 목록에서 열을 생략하는 것이 좋습니다.  
  
 또한 SKIP은 입력 행 집합의 열이 조인을 수행하는 데 필요하지만 열이 마이닝 구조에서 사용되지 않는 경우 유용합니다. 이에 대한 일반적인 예는 마이닝 구조 및 중첩 테이블이 포함된 마이닝 모델입니다. 이 구조의 입력 행 집합에는 SHAPE 절을 사용하여 계층적 행 집합을 만드는 데 사용하는 외래 키 열이 있지만 해당 외래 키 열은 모델에서 거의 사용되지 않습니다.  
  
 SKIP에 대한 구문을 사용하려면 입력 행 집합에서 해당하는 마이닝 구조 열이 없는 개별 열의 위치에 SKIP을 삽입해야 합니다. 예를 들어 아래 중첩 테이블 예에서는 OrderNumber가 RELATE 절에서 조인을 지정하는 데 사용될 수 있도록 APPEND 절에서 OrderNumber를 선택해야 합니다. 그러나 마이닝 구조의 중첩 테이블에 OrderNumber 데이터를 삽입하기를 원치 않습니다. 따라서 이 예에서는 INSERT INTO 인수에 OrderNumber를 사용하는 대신 SKIP 키워드를 사용합니다.  
  
## <a name="source-data-query"></a>원본 데이터 쿼리  
 \<원본 데이터 쿼리와 > 요소는 다음과 같은 데이터 원본 유형을 포함할 수 있습니다.  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **셰이프**  
  
-   행 집합을 반환하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 쿼리  
  
 데이터 원본 유형에 대 한 자세한 내용은 참조 [&#60; 원본 데이터 쿼리와 &#62;](../dmx/source-data-query.md)합니다.  
  
## <a name="basic-example"></a>기본 예  
 다음 예제에서는 **OPENQUERY** 의 대상된 메일 데이터를 기반으로 Naive Bayes 모델을 학습 하는 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 데이터베이스입니다.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>중첩 테이블의 예  
 다음 예제에서는 **셰이프** 중첩된 테이블을 포함 하는 연결 마이닝 모델을 학습 합니다. 첫 번째 줄을 포함 하는 참고 **SKIP** 대신 OrderNumber에서 필요한는 **SHAPE_APPEND** 문이 하지만 않습니다 마이닝 모델에 사용 합니다.  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
