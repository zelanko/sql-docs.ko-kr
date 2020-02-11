---
title: DMX (데이터 마이닝 확장) 참조 | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c47514f551ec07a8c8837533cb38c0e6283645cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892879"
---
# <a name="data-mining-extensions-dmx-reference"></a>DMX(Data Mining Extensions) 참조
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  DMX (데이터 마이닝 확장)는에서 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]데이터 마이닝 모델을 만들고 작업 하는 데 사용할 수 있는 언어입니다. DMX를 사용하여 새 데이터 마이닝 모델의 구조를 만들고 이 모델을 학습하고 이 모델을 검색, 관리 및 예측할 수 있습니다. DMX는 DDL(데이터 정의 언어) 문, DML(데이터 조작 언어) 문, 함수 및 연산자로 구성됩니다.  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Microsoft OLE DB for Data Mining 사양  
 의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 마이닝 기능은 데이터 마이닝 사양의 [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB를 준수 하도록 빌드됩니다.  
  
 데이터 [!INCLUDE[msCoName](../includes/msconame-md.md)] 마이닝 사양의 OLE DB은 다음을 정의 합니다.  
  
-   데이터 마이닝 모델을 정의하는 정보를 유지하기 위한 구조  
  
-   데이터 마이닝 모델을 만들고 사용하기 위한 언어  
  
 이 사양에서는 데이터 마이닝의 기초를 데이터 마이닝 모델 가상 개체로 정의합니다. 데이터 마이닝 모델 개체에는 특정 마이닝 모델에 대해 알려진 모든 내용이 포함됩니다. 데이터 마이닝 모델 개체는 모델을 설명하는 열, 데이터 형식 및 메타 정보가 포함된 SQL 테이블과 같은 구조로 구성됩니다. 이 구조에서는 SQL의 확장 기능인 DMX 언어를 사용하여 모델을 만들고 사용할 수 있습니다.  
  
 **자세한 내용:** [마이닝 구조 &#40;Analysis Services 데이터 마이닝&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining)  
  
##  <a name="BKMK_DMXStatements"></a>DMX 문  
 DMX 문을 사용하여 데이터 마이닝 모델을 작성, 처리, 삭제, 복사, 검색 및 예측할 수 있습니다. DMX에는 두 가지 유형의 문인 데이터 정의 문과 데이터 조작 문이 있습니다. 이 두 가지 유형의 문을 사용하여 다양한 태스크를 수행할 수 있습니다.  
  
 다음 섹션에서는 DMX 문을 사용하는 방법에 대해 설명합니다.  
  
-   [데이터 정의 문](#BKMK_DDL)  
  
-   [데이터 조작 문](#BKMK_DML)  
  
-   [쿼리 기본 사항](#BKMK_Queries)  
  
###  <a name="BKMK_DDL"></a>데이터 정의 문  
 DMX의 데이터 정의 문을 사용하여 새 마이닝 구조 및 모델을 만들거나 정의하고 마이닝 모델과 마이닝 구조를 가져오거나 내보내고 데이터베이스의 기존 모델을 삭제할 수 있습니다. DMX의 데이터 정의 문은 DDL(데이터 정의 언어)의 일부입니다.  
  
 DMX의 데이터 정의 문을 사용하여 다음과 같은 태스크를 수행할 수 있습니다.  
  
-   [CREATE 마이닝](../dmx/create-mining-structure-dmx.md) structure 문을 사용 하 여 마이닝 구조를 만들고 [ALTER 마이닝 structure](../dmx/alter-mining-structure-dmx.md) 문을 사용 하 여 마이닝 구조에 마이닝 모델을 추가 합니다.  
  
-   [CREATE 마이닝 model](../dmx/create-mining-model-dmx.md) 문을 사용 하 여 빈 데이터 마이닝 모델 개체를 작성 하 여 마이닝 모델 및 연결 된 마이닝 구조를 동시에 만듭니다.  
  
-   [Export](../dmx/export-dmx.md) 문을 사용 하 여 마이닝 모델 및 연결 된 마이닝 구조를 파일로 내보냅니다. [Import](../dmx/import-dmx.md) 문을 사용 하 여 EXPORT 문으로 만든 파일에서 마이닝 모델 및 연결 된 마이닝 구조를 가져옵니다.  
  
-   [SELECT into](../dmx/select-into-dmx.md) 문을 사용 하 여 기존 마이닝 모델의 구조를 새 모델로 복사 하 고 동일한 데이터로 학습 합니다.  
  
-   [DROP 마이닝 model](../dmx/drop-mining-model-dmx.md) 문을 사용 하 여 데이터베이스에서 마이닝 모델을 완전히 제거 합니다. [DROP 마이닝 structure](../dmx/drop-mining-structure-dmx.md) 문을 사용 하 여 데이터베이스에서 마이닝 구조 및 연결 된 모든 마이닝 모델을 완전히 제거 합니다.  
  
 DMX 문을 사용 하 여 수행할 수 있는 데이터 마이닝 태스크에 대 한 자세한 내용은 [데이터 마이닝 확장 &#40;dmx&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)를 참조 하세요.  
  
 [DMX 문으로 이동](#BKMK_DMXStatements)  
  
###  <a name="BKMK_DML"></a>데이터 조작 문  
 DMX의 데이터 조작 문을 사용하여 기존 마이닝 모델로 작업하고 모델을 검색하고 모델에 대한 예측을 만들 수 있습니다. DMX의 데이터 조작 문은 DML(데이터 조작 언어)의 일부입니다.  
  
 DMX의 데이터 조작 문을 사용하여 다음과 같은 태스크를 수행할 수 있습니다.  
  
-   [INSERT INTO](../dmx/insert-into-dmx.md) 문을 사용 하 여 마이닝 모델을 학습 합니다. 마이닝 모델의 학습을 수행하면 실제 원본 데이터가 데이터 마이닝 모델 개체에 삽입되지 않는 대신에 알고리즘에서 만드는 마이닝 모델을 설명하는 추상화가 수행됩니다. INSERT INTO 문의 원본 쿼리는 [ \<원본 데이터 쿼리>](../dmx/source-data-query.md)에 설명 되어 있습니다.  
  
-   SELECT 문을 확장 하 여 원본 데이터의 통계와 같이 모델 학습 중에 계산 되 고 데이터 마이닝 모델에 저장 되는 정보를 검색 합니다. SELECT 문의 기능을 확장 하기 위해 포함할 수 있는 절은 다음과 같습니다.  
  
    -   [&#60;모델 &#62; &#40;DMX&#41;에서 고유를 선택 합니다.](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [&#60;모델&#62;에서 선택 합니다. 콘텐츠 &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
    -   [&#60;모델&#62;에서 선택 합니다. 사례 &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [&#60;모델&#62;에서 선택 합니다. DMX&#41;SAMPLE_CASES &#40;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [&#60;모델&#62;에서 선택 합니다. DMX&#41;DIMENSION_CONTENT &#40;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   SELECT 문의 [예측 조인](../dmx/select-from-model-prediction-join-dmx.md) 절을 사용 하 여 기존 마이닝 모델을 기반으로 예측을 만듭니다. 예측 조인 문의 원본 쿼리는 [ \<원본 데이터 쿼리>](../dmx/source-data-query.md)에 설명 되어 있습니다.  
  
-   [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) 문을 사용 하 여 모델 또는 구조에서 학습 된 모든 데이터를 제거 합니다.  
  
 DMX 문을 사용 하 여 수행할 수 있는 데이터 마이닝 태스크에 대 한 자세한 내용은 [데이터 마이닝 확장 &#40;dmx&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)를 참조 하세요.  
  
 [DMX 문으로 이동](#BKMK_DMXStatements)  
  
###  <a name="BKMK_Queries"></a>DMX 쿼리 기본 사항  
 SELECT 문은 대부분의 DMX 쿼리에 대 한 기본입니다. 이 문과 함께 다양한 절을 사용하여 마이닝 모델을 검색하거나 복사하거나 예측할 수 있습니다. 예측 쿼리는 SELECT의 형태를 사용 하 여 기존 마이닝 모델을 기반으로 예측을 만듭니다. 함수를 통해 데이터 마이닝 모델의 내재된 기능을 확장하여 마이닝 모델을 다양하게 검색 및 쿼리할 수 있습니다.  
  
 DMX 함수를 사용하여 모델 학습 중에 발견한 정보를 가져오고 새 정보를 계산할 수 있습니다. 기본 데이터 또는 예측 정확성을 설명하는 통계를 반환하거나 예측에 대한 상세한 설명을 반환하는 등의 여러 가지 용도로 함수를 사용할 수 있습니다.  
  
 **자세한**내용은 Dmx [Select 문 이해](../dmx/understanding-the-dmx-select-statement.md), [일반 예측 함수 &#40;Dmx&#41;](../dmx/general-prediction-functions-dmx.md), [dmx 예측 쿼리의 구조 및 사용](../dmx/structure-and-usage-of-dmx-prediction-queries.md), [데이터 마이닝 확장 &#40;dmx&#41; 함수 참조를 참조](../dmx/data-mining-extensions-dmx-function-reference.md) **하세요.**    
  
 [DMX 문으로 이동](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 함수 참조](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 연산자 참조](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 규칙](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 구문 요소](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;일반 예측 함수 &#40;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 예측 쿼리의 구조 및 사용법](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX Select 문 이해](../dmx/understanding-the-dmx-select-statement.md)  
  
  
