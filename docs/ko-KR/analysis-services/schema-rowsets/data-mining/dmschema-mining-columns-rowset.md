---
title: DMSCHEMA_MINING_COLUMNS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DMSCHEMA_MINING_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9f43f69d2695c9b73b45e152273a679ad8b17fe2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dmschemaminingcolumns-rowset"></a>DMSCHEMA_MINING_COLUMNS 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 모든 데이터 마이닝 모델의 개별 열에 대해 설명합니다. 이 행 집합은 현재 카탈로그로 제한됩니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DMSCHEMA_MINING_COLUMNS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|카탈로그 이름입니다. 모델이 멤버인 데이터베이스 이름으로 채워집니다.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|정규화되지 않은 스키마 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**모델 이름**|**DBTYPE_WSTR**|마이닝 모델 이름입니다. 이 열은 열과 연결된 마이닝 모델 이름을 포함하며 비어 있을 수 없습니다.|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|열 이름입니다.|  
|**COLUMN_GUID**|**DBTYPE_GUID**|열 GUID입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**|열 속성 ID입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**|열의 서수 위치입니다. 열 번호는 1부터 시작됩니다. 열에 대한 안정적인 서수 값이 없는 경우 이 열에는 **NULL** 이 포함됩니다.|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**|열에 기본값이 있는지 여부를 나타내는 부울입니다.<br /><br /> 열에 기본값이 있으면**TRUE** 이고, 그렇지 않으면 **FALSE**입니다.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**|열의 기본값입니다.<br /><br /> 기본값이 **NULL** 값이면 **COLUMN_HASDEFAULT** 는 **TRUE**이고, 이 열은 **NULL**입니다.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**|열 특징을 설명하는 비트 마스크입니다. **DBCOLUMNFLAGS** 열거 형식은 비트 마스크의 비트를 지정합니다. 이 열은 비어 있을 수 없습니다.|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|null 값이 허용되는 열인지 여부를 나타내는 부울입니다.<br /><br /> null 값이 허용되는 열이 아니면**FALSE** 이고, null 값이 허용되는 열이면 **TRUE**입니다.|  
|**DATA_TYPE**|**DBTYPE_UI2**|열 데이터 형식 표시기입니다. 다음 목록에서는 반환되는 표시기 유형의 예를 보여 줍니다.<br /><br /> "**TABLE**"는 **DBTYPE_HCHAPTER**를 반환합니다.<br /><br /> "**TEXT**"는 **DBTYPE_WCHAR**를 반환합니다.<br /><br /> "**LONG**"는 **DBTYPE_I8**를 반환합니다.<br /><br /> "**DOUBLE**"는 **DBTYPE_R8**를 반환합니다.<br /><br /> "**DATE**"는 **DBTYPE_DATE**를 반환합니다.|  
|**TYPE_GUID**|**DBTYPE_GUID**|열 데이터 형식의 GUID입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **VT_NULL**합니다.|  
|**때**|**DBTYPE_UI4**|열 값의 최대 길이로서 문자, 이진 또는 비트 열의 경우 이 값은 다음 중 하나입니다.<br /><br /> 열 길이가 정의되어 있으면 열의 최대 길이(열 유형에 따라 각각 문자, 바이트 또는 비트)입니다. 예를 들어 SQL 테이블에 있는 **CHAR(5)** 열의 최대 길이는 5입니다.<br /><br /> 열 길이가 정의되어 있지 않으면 데이터 형식의 최대 길이(열 유형에 따라 각각 문자, 바이트 또는 비트)입니다.<br /><br /> 열과 데이터 형식의 최대 길이가 모두 정의되어 있지 않으면 0입니다.<br /><br /> 다른 모든 열 유형의 경우에는**NULL** 입니다.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**|열 유형이 문자 또는 이진이면 옥텟(바이트) 단위의 최대 열 길이입니다. 0 값은 열에 최대 길이가 없음을 나타냅니다. 다른 모든 열 유형의 경우 이 열은 **NULL** 입니다.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**|열의 데이터 형식이 **VARNUMERIC**이외의 숫자 데이터 형식이면 열의 최대 전체 자릿수입니다.<br /><br /> 열의 데이터 형식이 숫자가 아니거나**NULL** 이면 **VARNUMERIC**입니다.<br /><br /> 데이터 형식이 **DBTYPE_DECIMAL** 또는 **DBTYPE_NUMERIC** 인 열의 전체 자릿수는 열 정의에 따라 달라집니다.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**|열 유형 표시기가 **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**또는 **DBTYPE_VARNUMERIC**이면 소수점 이하 자릿수입니다. 그렇지 않으면 이 열은 **VT_NULL**입니다.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**|열 데이터 형식이 DateTime 또는 간격 유형이면 열의 date/time 전체 자릿수(초 소수 부분 자릿수)이고, 그렇지 않으면 **NULL**입니다.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**|문자 집합이 정의된 카탈로그 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**|문자 집합이 정의된 정규화되지 않은 스키마 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**|문자 집합 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**|데이터 정렬이 정의된 카탈로그 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**|데이터 정렬이 정의된 정규화되지 않은 스키마 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**데이터 정렬 이름**|**DBTYPE_WSTR**|데이터 정렬 이름입니다 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**|도메인이 정의된 카탈로그 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**|도메인이 정의된 정규화되지 않은 스키마 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**DOMAIN_NAME**|**DBTYPE_WSTR**|도메인 이름입니다. 이 열에서 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|열에 대 한 알기 쉬운 설명에서이 열을 지원 하지 않는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 항상 포함 **NULL**합니다.|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**|열의 통계 분포에 대한 설명입니다. 이 열은 다음 값 중 하나입니다.<br /><br /> "**보통**"<br /><br /> "**LOG_NORMAL**"<br /><br /> "**UNIFORM**"|  
|**CONTENT_TYPE**|**DBTYPE_WSTR**|열 내용에 대한 설명입니다. 이 열은 다음 값 중 하나입니다.<br /><br /> "**키**"<br /><br /> "**이산**"<br /><br /> "**CONTINUOUS**"<br /><br /> "**DISCRETIZED (**[인수]**)**"<br /><br /> "**ORDERED**"<br /><br /> "**KEY TIME**"<br /><br /> "**CYCLICAL**"<br /><br /> "**확률**"<br /><br /> "**분산**"<br /><br /> "**STDEV**"<br /><br /> "**지원**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"<br /><br /> **"KEY SEQUENCE**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**|쉼표로 구분된 플래그 목록입니다. 정의된 플래그는 다음과 같습니다.<br /><br /> "**MODEL_EXISTENCE_ONLY**"<br /><br /> "**회귀 변수**"<br /><br /> 알고리즘별 모델링 플래그가 이 열에 포함될 수도 있습니다.|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**|이 열이 키와 관련되어 있는지 여부를 나타내는 부울입니다.<br /><br /> 이 열이 키와 관련되어 있으면**TRUE** 입니다. 키가 단일 열이면 **RELATED_ATTRIBUTE** 필드에 열 이름이 포함될 수도 있습니다.|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**|현재 열이 관련되어 있거나 특수 속성을 갖는 대상 열의 이름입니다.|  
|**IS_INPUT**|**DBTYPE_BOOL**|열이 입력 열인지 여부를 나타내는 부울입니다.<br /><br /> 입력 열이면**VARIANT_TRUE** 입니다.|  
|**IS_PREDICTABLE**|**DBTYPE_BOOL**|예측 가능한 열인지 여부를 나타내는 부울입니다.<br /><br /> 예측 가능한 열이면**TRUE** 입니다.|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**|이 열이 포함되어 있는 **TABLE** 열의 이름입니다. 이 열이 다른 열에 포함되어 있지 않으면 **NULL** 입니다.|  
|**PREDICTION_SCALAR_FUNCTIONS**|**DBTYPE_WSTR**|열에서 수행할 수 있는 쉼표로 구분된 스칼라 함수 목록입니다.|  
|**PREDICTION_TABLE_FUNCTIONS**|**DBTYPE_WSTR**|열에 적용할 수 있는 쉼표로 구분된 함수 목록입니다. 함수는 테이블을 반환해야 합니다. 목록 형식은 다음과 같습니다.<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> 이 형식을 사용하면 클라이언트 응용 프로그램에서 각 함수의 서명(매개 변수 목록)을 확인할 수 있습니다.|  
|**IS_POPULATED**|**DBTYPE_BOOL**|열이 사용 가능한 값 집합을 알고 있는지 여부를 나타내는 부울입니다.<br /><br /> 열이 사용 가능한 값 집합을 알고 있으면**TRUE** 입니다.<br /><br /> 열이 채워져 있지 않으면 **FALSE** 입니다.|  
|**PREDICTION_SCORE**|**DBTYPE_R8**|열 예측에 대한 모델 점수로서, 모델의 정확도를 측정하는 데 사용됩니다.|  
|**SOURCE_COLUMN**|**DBTYPE_WSTR**|현재 마이닝 열에 대한 원본 마이닝 구조 열의 이름입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 **DMSCHEMA_MINING_COLUMNS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|(선택 사항)|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|(선택 사항)|  
|**모델 이름**|**DBTYPE_WSTR**|(선택 사항)|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 스키마 행 집합](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
