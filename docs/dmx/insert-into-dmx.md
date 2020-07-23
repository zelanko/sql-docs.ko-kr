---
title: INSERT INTO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eedff3b14960fae68ad4e3a9ac54a0034c1a9300
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969782"
---
# <a name="insert-into-dmx"></a>INSERT INTO(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  지정한 데이터 마이닝 개체를 처리합니다. 마이닝 모델 및 마이닝 구조를 처리 하는 방법에 대 한 자세한 내용은 [데이터 마이닝&#41;&#40;처리 요구 사항 및 고려 사항 ](https://docs.microsoft.com/analysis-services/data-mining/processing-requirements-and-considerations-data-mining)을 참조 하세요.  
  
 마이닝 구조가 지정된 경우 이 문은 마이닝 구조 및 연결된 모든 마이닝 모델을 처리합니다. 마이닝 모델이 지정된 경우 이 문은 마이닝 모델만 처리합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>인수  
 *model*  
 모델 식별자입니다.  
  
 *구조체나*  
 구조 식별자입니다.  
  
 *매핑된 모델 열*  
 열 식별자 및 중첩 식별자의 쉼표로 구분된 목록입니다.  
  
 *원본 데이터 쿼리*  
 공급자가 정의한 형식의 원본 쿼리입니다.  
  
## <a name="remarks"></a>설명  
 **마이닝 모델** 또는 **마이닝 구조**를 지정 하지 않으면에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이름을 기준으로 개체 유형을 검색 하 고 올바른 개체를 처리 합니다. 서버에 이름이 서로 동일한 마이닝 구조 및 마이닝 모델이 있는 경우에는 오류가 반환됩니다.  
  
 두 번째 구문 형식을 사용 하 여를에 삽입 *\<object>* 합니다. COLUMN_VALUES 모델을 학습 하지 않고 모델 열에 직접 데이터를 삽입할 수 있습니다. 이렇게 하면 간결하게 정렬된 방식으로 모델에 열 데이터가 제공되므로 계층 구조나 정렬된 열이 포함된 데이터 세트으로 작업할 때 유용합니다.  
  
 마이닝 모델 또는 마이닝 구조와 함께 **INSERT INTO** 를 사용 하 고 \<mapped model columns> 및 \<source data query> 인수를 벗어나면 문이 이미 존재 하는 바인딩을 사용 하 여 **processdefault**와 같이 동작 합니다. 바인딩이 없는 경우에는 오류가 반환됩니다. **Processdefault**에 대 한 자세한 내용은 [처리 옵션 및 설정 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services)를 참조 하세요. 다음 예에서는 구문을 보여 줍니다.  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 **마이닝 모델** 을 지정 하 고 매핑된 열과 원본 데이터 쿼리를 제공 하면 모델 및 연결 된 구조가 처리 됩니다.  
  
 다음 표에서는 개체의 상태에 따라 여러 가지 형식의 문을 실행한 결과를 설명합니다.  
  
|인수를 제거합니다.|개체의 상태|결과|  
|---------------|----------------------|------------|  
|마이닝 모델에 삽입*\<model>*|마이닝 구조가 처리됩니다.|마이닝 모델이 처리됩니다.|  
||마이닝 구조가 처리되지 않습니다.|마이닝 모델 및 마이닝 구조가 처리됩니다.|  
||마이닝 구조에 추가 마이닝 모델이 포함되어 있습니다.|프로세스가 실패합니다. 마이닝 구조 및 연결된 마이닝 모델을 다시 처리해야 합니다.|  
|마이닝 구조에 삽입*\<structure>*|마이닝 구조가 처리되거나 처리되지 않습니다.|마이닝 구조 및 연결된 마이닝 모델이 처리됩니다.|  
|*\<model>* 원본 쿼리를 포함 하는 마이닝 모델에 삽입<br /><br /> 또는<br /><br /> *\<structure>* 원본 쿼리를 포함 하는 마이닝 구조에 삽입|마이닝 구조 또는 모델에 이미 내용이 포함되어 있습니다.|프로세스가 실패합니다. [삭제 &#40;DMX&#41;](../dmx/delete-dmx.md)를 사용 하 여이 작업을 수행 하기 전에 개체를 지워야 합니다.|  
  
## <a name="mapped-model-columns"></a>매핑된 모델 열  
 요소를 사용 하 여 \<mapped model columns> 데이터 원본의 열을 마이닝 모델의 열에 매핑할 수 있습니다. \<mapped model columns>요소의 형식은 다음과 같습니다.  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 **SKIP**을 사용 하면 원본 쿼리에 반드시 있어야 하지만 마이닝 모델에는 없는 특정 열을 제외할 수 있습니다. SKIP은 입력 행 집합에 포함된 열을 제어하지 못하는 경우 유용합니다. 고유의 OPENQUERY를 작성 중인 경우에는 SKIP을 사용하는 대신 SELECT 열 목록에서 열을 생략하는 것이 좋습니다.  
  
 또한 SKIP은 입력 행 집합의 열이 조인을 수행하는 데 필요하지만 열이 마이닝 구조에서 사용되지 않는 경우 유용합니다. 이에 대한 일반적인 예는 마이닝 구조 및 중첩 테이블이 포함된 마이닝 모델입니다. 이 구조의 입력 행 집합에는 SHAPE 절을 사용하여 계층적 행 집합을 만드는 데 사용하는 외래 키 열이 있지만 해당 외래 키 열은 모델에서 거의 사용되지 않습니다.  
  
 SKIP에 대한 구문을 사용하려면 입력 행 집합에서 해당하는 마이닝 구조 열이 없는 개별 열의 위치에 SKIP을 삽입해야 합니다. 예를 들어 아래 중첩 테이블 예에서는 OrderNumber가 RELATE 절에서 조인을 지정하는 데 사용될 수 있도록 APPEND 절에서 OrderNumber를 선택해야 합니다. 그러나 마이닝 구조의 중첩 테이블에 OrderNumber 데이터를 삽입하기를 원치 않습니다. 따라서 이 예에서는 INSERT INTO 인수에 OrderNumber를 사용하는 대신 SKIP 키워드를 사용합니다.  
  
## <a name="source-data-query"></a>원본 데이터 쿼리  
 요소에는 \<source data query> 다음 데이터 원본 유형이 포함 될 수 있습니다.  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **형태**  
  
-   행 집합을 반환하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 쿼리  
  
 데이터 원본 유형에 대 한 자세한 내용은 [&#60;원본 데이터 쿼리&#62;](../dmx/source-data-query.md)를 참조 하세요.  
  
## <a name="basic-example"></a>기본 예  
 다음 예에서는 **OPENQUERY** 를 사용 하 여 데이터베이스의 타겟 메일링 데이터를 기반으로 Naive Bayes 모델을 학습 합니다 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] .  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>중첩 테이블의 예  
 다음 예에서는 **셰이프** 를 사용 하 여 중첩 테이블을 포함 하는 연결 마이닝 모델을 학습 합니다. 펀치 선은 **SHAPE_APPEND** 문에 필요 하지만 마이닝 모델에는 사용 되지 않는 **SKIP** 대신 ordernumber를 포함 합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
