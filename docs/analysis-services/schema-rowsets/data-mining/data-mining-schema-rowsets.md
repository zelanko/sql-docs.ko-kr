---
title: 데이터 마이닝 스키마 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ee1f8d3288d884f7322fa578d8cd9b58919c335b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="data-mining-schema-rowsets"></a>Data Mining Schema Rowsets
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  실행 중인 서버 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 다음 데이터 마이닝 스키마 행 집합을 지원 합니다. 에 특정 XML/A 공급자가 특정 행 집합을 지원 하는지 여부를 확인 하려면 사용는 [DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md) 포함 된 행 집합의 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서는 데이터 마이닝 스키마 행 집합이 $SYSTEM 스키마에 Transact-SQL 언어로 된 테이블로 표시됩니다. 예를 들어 Analysis Services 인스턴스에 대한 다음 쿼리는 현재 인스턴스에서 사용할 수 있는 스키마 목록을 반환합니다.  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>섹션 내용  
  
|스키마 행 집합|Description|  
|-------------------|-----------------|  
|[DMSCHEMA_MINING_COLUMNS 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|서버에 배포된 모든 정의된 데이터 마이닝 구조의 개별 열에 대해 설명합니다.|  
|[DMSCHEMA_MINING_FUNCTIONS 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|서버에 설치된 각 데이터 마이닝 알고리즘에 사용할 수 있는 예측 함수 및 마이닝 함수에 대해 설명합니다.|  
|[DMSCHEMA_MINING_MODEL_CONTENT 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|클라이언트 응용 프로그램을 사용하여 학습된 데이터 마이닝 모델의 내용을 검색할 수 있습니다.|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|마이닝 모델 콘텐츠의 XML(PMML 2.1) 표현을 반환합니다.|  
|[DMSCHEMA_MINING_MODEL_XML 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|마이닝 모델의 XML(PMML 2.1) 구조를 반환합니다. 이 행 집합은 이전 버전과의 호환성을 위해 유지되는 DMSCHEMA_MINING_MODEL_PMML과 동일한 스키마입니다.|  
|[DMSCHEMA_MINING_MODELS 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|서버에 배포된 데이터 마이닝 모델을 열거합니다.|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|서버에 설치된 각 데이터 마이닝 알고리즘의 동작을 구성하는 데 사용할 수 있는 매개 변수 목록을 제공합니다.|  
|[DMSCHEMA_MINING_SERVICES 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|서버에서 사용할 수 있는 각 데이터 마이닝 알고리즘에 대한 설명을 제공합니다.|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|서버에 배포된 모든 마이닝 구조의 개별 열에 대해 설명합니다.|  
|[DMSCHEMA_MINING_STRUCTURES 행 집합](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|마이닝 구조에 대한 정보를 열거합니다.|  
  
 여기에 나열 된 모든 스키마 행 집합은 실행 중인 서버에서 지 원하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [데이터 마이닝 스키마 행 집합 &#40;SSAs&#41;](../../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
