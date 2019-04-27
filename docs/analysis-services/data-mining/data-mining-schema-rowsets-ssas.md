---
title: 데이터 마이닝 스키마 행 집합 (SSAs) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 127111dcbcdef14d511c7e296743ba23a5ca1cdd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62670456"
---
# <a name="data-mining-schema-rowsets-ssas"></a>데이터 마이닝 스키마 행 집합(SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에는 기존 OLE DB 데이터 마이닝 스키마 행 집합 대부분이 DMX(Data Mining Extensions) 문을 사용하여 쿼리할 수 있는 시스템 테이블 집합으로 노출됩니다. 데이터 마이닝 스키마 행 집합을 대상으로 쿼리를 작성하면 사용할 수 있는 서비스를 식별하고, 모델과 구조의 상태에 대한 업데이트를 가져오고, 모델 콘텐츠나 매개 변수에 대한 정보를 찾을 수 있습니다. 데이터 마이닝 스키마 행 집합에 대한 설명은 [Data Mining Schema Rowsets](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets)을 참조하십시오.  
  
> [!NOTE]  
>  XMLA를 사용하여 데이터 마이닝 스키마 행 집합을 쿼리할 수도 있습니다. SQL Server Management Studio에서 이 작업을 수행하는 방법에 대한 자세한 내용은 [XMLA를 사용하여 데이터 마이닝 쿼리 만들기](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md)를 참조하세요.  
  
## <a name="list-of-data-mining-schema-rowsets"></a>데이터 마이닝 스키마 행 집합 목록  
 다음 표에서는 쿼리 및 모니터링하는 데 유용한 데이터 마이닝 스키마 행 집합의 목록을 보여 줍니다.  
  
|행 집합 이름|Description|  
|-----------------|-----------------|  
|DMSCHEMA_MINING_MODELS|현재 컨텍스트의 모든 마이닝 모델을 나열합니다.<br /><br /> 여기에는 만든 날짜, 모델을 만드는 데 사용된 매개 변수 및 학습 집합의 크기와 같은 정보가 포함됩니다.|  
|DMSCHEMA_MINING_COLUMNS|현재 컨텍스트의 마이닝 모델에 사용된 모든 열을 나열합니다.<br /><br /> 마이닝 구조 원본 열에 대한 매핑, 데이터 형식, 전체 자릿수, 열에 사용할 수 있는 예측 함수 등의 정보가 포함됩니다.|  
|DMSCHEMA_MINING_STRUCTURES|현재 컨텍스트의 모든 마이닝 구조를 나열합니다.<br /><br /> 구조가 채워졌는지 여부, 구조가 마지막으로 처리된 날짜, 구조에 대해 지정된 홀드아웃 데이터 집합 정의(있는 경우) 등의 정보가 포함됩니다.|  
|DMSCHEMA_MINING_STRUCTURE_COLUMNS|현재 컨텍스트의 마이닝 구조에 사용된 모든 열을 나열합니다.<br /><br /> 내용 유형과 데이터 형식, null 허용 여부, 열에 중첩 테이블 데이터가 포함되었는지 여부 등의 정보가 포함됩니다.|  
|DMSCHEMA_MINING_SERVICES|지정된 서버에서 사용할 수 있는 모든 마이닝 서비스나 알고리즘을 나열합니다.<br /><br /> 지원되는 모델링 플래그, 입력 유형, 지원되는 데이터 원본 유형 등의 정보가 포함됩니다.|  
|DMSCHEMA_MINING_SERVICE_PARAMETERS|현재 인스턴스에서 사용할 수 있는 마이닝 서비스의 모든 매개 변수를 나열합니다.<br /><br /> 각 매개 변수의 데이터 형식, 기본값, 상한 및 하한 등의 정보가 포함됩니다.|  
|DMSCHEMA_MODEL_CONTENT|모델이 처리된 경우 모델의 내용을 반환합니다.<br /><br /> 자세한 내용은 [마이닝 모델 콘텐츠&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)를 참조하세요.|  
|DBSCHEMA_CATALOGS|Analysis Services의 현재 인스턴스에 포함된 모든 데이터베이스(카탈로그)를 나열합니다.|  
|MDSCHEMA_INPUT_DATASOURCES|Analysis Services의 현재 인스턴스에 포함된 모든 데이터 원본을 나열합니다.|  
  
> [!NOTE]  
>  이 표의 목록에 포함된 행 집합은 일부에 불과하며 여기에는 문제 해결에 가장 도움이 될 수 있는 행 집합만 나열되었습니다.  
  
## <a name="examples"></a>예  
 다음 섹션에서는 데이터 마이닝 스키마 행 집합에 대한 몇 가지 쿼리 예를 제공합니다.  
  
### <a name="example-1-list-data-mining-services"></a>예 1: 데이터 마이닝 서비스 나열  
 다음 쿼리는 현재 서버에서 사용할 수 있는 마이닝 서비스, 즉 설정되어 있는 알고리즘의 목록을 반환합니다. 각 마이닝 서비스에 대해 제공되는 열에는 각 알고리즘에 사용될 수 있는 모델링 플래그와 내용 유형, 각 서비스의 GUID 및 각 서비스에 추가되었을 수 있는 예측 제한이 포함됩니다.  
  
```  
SELECT *  
FROM $system.DMSCHEMA_MINING_SERVICES  
```  
  
### <a name="example-2-list-mining-model-parameters"></a>예 2: 마이닝 모델 매개 변수 목록  
 다음 예는 특정 마이닝 모델을 만드는 데 사용된 매개 변수를 반환합니다.  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
### <a name="example-3-list-all-rowsets"></a>예제 3: 모든 행 집합 나열  
 다음 예에서는 현재 서버에서 사용할 수 있는 행 집합의 전체 목록을 반환합니다.  
  
```  
SELECT *   
FROM $system.DBSCHEMA_TABLES  
```  
  
  
