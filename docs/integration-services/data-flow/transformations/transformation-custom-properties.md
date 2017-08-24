---
title: "변환 사용자 지정 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Slowly Changing Dimension transformation
- Import Column transformation [Integration Services]
- Sort transformation
- Unpivot transformation
- Merge Join transformation
- Data Mining Query transformation
- Fuzzy Grouping transformation
- Data Conversion transformation
- Fuzzy Lookup transformation
- Term Extraction transformation
- Row Count transformation custom properties [Integration Services]
- transformations [Integration Services], properties
- Pivot transformation
- Lookup transformation
- Percentage Sampling transformation
- Export Column transformation [Integration Services]
- Row Sampling transformation
- Conditional Split transformation custom properties [Integration Services]
- custom properties [Integration Services]
- Audit transformation
- Term Lookup transformation
- Script Component transformation custom properties [Integration Services]
- Derived Column transformation
- OLE DB Command transformation
- Copy Column transformation custom properties [Integration Services]
- Character Map transformation custom properties [Integration Services]
ms.assetid: 56f5df6a-56f6-43df-bca9-08476a3bd931
caps.latest.revision: 72
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 62ff6e04e7f26e6ca1af9760ebb17c5f41d37f0d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="transformation-custom-properties"></a>변환 사용자 지정 속성
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 개체 모델에 있는 대부분의 데이터 흐름 개체에 공통된 속성 이외에 많은 데이터 흐름 개체에는 해당 개체와 관련된 사용자 지정 속성이 있습니다. 이러한 사용자 지정 속성은 런타임에만 사용할 수 있으며 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 관리 프로그래밍 참조 설명서에서 설명하지 않습니다.  
  
 이 항목에서는 다양한 데이터 흐름 변환의 사용자 지정 속성을 나열하고 설명합니다. 대부분의 데이터 흐름 개체에 공통되는 속성에 대한 자세한 내용은 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)을 참조하십시오.  
  
 변환의 일부 속성은 속성 식을 사용하여 설정할 수 있습니다. 자세한 내용은 [식을 사용하여 설정할 수 있는 데이터 흐름 속성](http://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)을 참조하세요.  
  
## <a name="transformations-with-custom-properties"></a>사용자 지정 속성이 있는 변환  
  
||||  
|-|-|-|  
|[집계](#aggregate)|[열 내보내기](#extract)|[행 개수](#rowcount)|  
|[감사](#audit)|[유사 항목 그룹화](#fgroup)|[행 샘플링](#rowsamp)|  
|[캐시 변환](#cachetransform)|[유사 항목 조회](#flookup)|[스크립트 구성 요소](#script)|  
|[문자표 변환](#charmap)|[열 가져오기](#insert)|[느린 변경 차원](#scd)|  
|[조건부 분할](#condsplit)|[조회](#lookup)|[정렬](#sort)|  
|[열 복사](#copymap)|[병합 조인](#mjoin)|[용어 추출](#textract)|  
|[데이터 변환](#dataconv)|[OLE DB 명령](#oledbcmd)|[용어 조회](#tlookup)|  
|[데이터 마이닝 쿼리](#dmquery)|[비율 샘플링](#percent)|[피벗 해제](#unpivot)|  
|[파생 열](#derived)|[피벗](#pivot)||  
  
### <a name="transformations-without-custom-properties"></a>사용자 지정 속성이 없는 변환  
 [Merge Transformation](../../../integration-services/data-flow/transformations/merge-transformation.md), [Multicast Transformation](../../../integration-services/data-flow/transformations/multicast-transformation.md)및 [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md)변환은 구성 요소, 입력 또는 출력 수준의 사용자 지정 속성을 포함하지 않습니다. 이러한 변환은 모든 데이터 흐름 구성 요소에 공통된 속성만 사용합니다.  
  
##  <a name="aggregate"></a> 집계 변환 사용자 지정 속성  
 집계 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 집계 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|AutoExtendFactor|정수|집계 중에 메모리를 확장할 수 있는 비율을 지정하는 1에서 100 사이의 값입니다. 이 속성의 기본값은 **25**입니다.|  
|CountDistinctKeys|정수|집계에서 쓸 수 있는 정확한 고유 카운트 수를 지정하는 값입니다. CountDistinctScale 값이 지정되어 있으면 CountDistinctKeys의 값이 우선 순위를 갖습니다.|  
|CountDistinctScale|Integer(열거형)|집계에서 셀 수 있는 열의 대략적인 고유 값 수를 설명하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **Low** (1) - 최대 50만 개의 키 값을 나타냅니다.<br /><br /> **Medium** (2) - 최대 500만 개의 키 값을 나타냅니다.<br /><br /> **High** (3) - 2,500만 개 이상의 키 값을 나타냅니다.<br /><br /> **Unspecified** (0) - CountDistinctScale 값이 사용되지 않음을 나타냅니다. **Unspecified** (0) 옵션을 사용하면 대량 데이터 집합의 성능에 영향을 줄 수 있습니다.|  
|키|정수|집계에서 쓰는 정확한 Group By 키 수를 지정하는 값입니다. KeyScalevalue가 지정되어 있으면 Keys의 값이 우선 순위를 갖습니다.|  
|KeyScale|Integer(열거형)|집계에서 쓸 수 있는 대략적인 Group By 키 값 수를 설명하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **Low** (1) - 최대 50만 개의 키 값을 나타냅니다.<br /><br /> **Medium** (2) - 최대 500만 개의 키 값을 나타냅니다.<br /><br /> **High** (3) - 2,500만 개 이상의 키 값을 나타냅니다.<br /><br /> **Unspecified** (0) - KeyScale 값이 사용되지 않음을 나타냅니다.|  
  
 다음 표에서는 집계 변환 출력의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|키|정수|집계에서 쓸 수 있는 정확한 Group By 키 수를 지정하는 값입니다. KeyScale 값이 지정되어 있으면 Keys의 값이 우선 순위를 갖습니다.|  
|KeyScale|Integer(열거형)|집계에서 쓸 수 있는 대략적인 Group By 키 값 수를 설명하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **Low** (1) - 최대 50만 개의 키 값을 나타냅니다.<br /><br /> **Medium** (2) - 최대 500만 개의 키 값을 나타냅니다.<br /><br /> **High** (3) - 2,500만 개 이상의 키 값을 나타냅니다.<br /><br /> **Unspecified** (0) - KeyScale 값이 사용되지 않음을 나타냅니다.|  
  
 다음 표에서는 집계 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|AggregationColumnId|정수|GROUP BY 또는 집계 함수에 참여하는 열의 **LineageID** 입니다.|  
|AggregationComparisonFlags|정수|집계 변환에서 열의 문자열 데이터를 비교하는 방법을 지정하는 값입니다. 자세한 내용은 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)을 참조하세요.|  
|AggregationType|Integer(열거형)|열에서 수행할 집계 연산을 지정하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **Group by** (0)<br /><br /> **Count** (1)<br /><br /> **Count all** (2)<br /><br /> **Countdistinct** (3)<br /><br /> **Sum** (4)<br /><br /> **Average** (5)<br /><br /> **Maximum** (7)<br /><br /> **Minimum** (6)|  
|CountDistinctKeys|정수|집계 유형이 **Count distinct**인 경우 집계에서 쓸 수 있는 정확한 키 수를 지정하는 값입니다. CountDistinctScale 값이 지정되어 있으면 CountDistinctKeys의 값이 우선 순위를 갖습니다.|  
|CountDistinctScale|Integer(열거형)|집계 유형이 **Count distinct**인 경우 집계에서 쓸 수 있는 대략적인 키 값 수를 설명하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **Low** (1) - 최대 50만 개의 키 값을 나타냅니다.<br /><br /> **Medium** (2) - 최대 500만 개의 키 값을 나타냅니다.<br /><br /> **High** (3) - 2,500만 개 이상의 키 값을 나타냅니다.<br /><br /> **Unspecified** (0) - CountDistinctScale 값이 사용되지 않음을 나타냅니다.|  
|IsBig|Boolean|열에 40억을 초과하는 값 또는 배정밀도 부동 소수점 값보다 전체 자릿수가 큰 값이 포함되어 있는지 여부를 나타내는 값입니다. 값은 0 또는 1일 수 있습니다. 0은 IsBig이 **False** 이며 열에 큰 값이나 정확한 값이 포함되어 있지 않음을 나타냅니다. 이 속성의 기본값은 1입니다.|  
  
 집계 변환의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Aggregate Transformation](../../../integration-services/data-flow/transformations/aggregate-transformation.md)을 참조하세요.  
  
##  <a name="audit"></a> 감사 변환 사용자 지정 속성  
 감사 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
 다음 표에서는 감사 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|LineageItemSelected|Integer(열거형)|출력에 대해 선택된 감사 항목입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **실행 인스턴스 GUID** (0)<br /><br /> **실행 시작 시간** (4)<br /><br /> **컴퓨터 이름** (5)<br /><br /> **패키지 ID** (1)<br /><br /> **패키지 이름** (2)<br /><br /> **태스크 ID** (8)<br /><br /> **태스크 이름** (7)<br /><br /> **사용자 이름** (6)<br /><br /> **버전 ID** (3)|  
  
 감사 변환의 입력, 입력 열 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Audit Transformation](../../../integration-services/data-flow/transformations/audit-transformation.md)을 참조하세요.  
  
##  <a name="cachetransform"></a> 캐시 변환 사용자 지정 속성  
 캐시 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 캐시 변환의 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|Connectionmanager|문자열|연결 관리자의 이름을 지정합니다.|  
|ValidateExternalMetadata|Boolean|디자인 타임에 외부 데이터 원본을 사용하여 캐시 변환의 유효성을 검사하는지 여부를 나타냅니다. 속성이 **False**로 설정된 경우 런타임에 외부 데이터 원본에 대한 유효성 검사가 수행됩니다.<br /><br /> 기본값은 **True**입니다.|  
|AvailableInputColumns|문자열|사용 가능한 입력 열 목록입니다.|  
|InputColumns|문자열|선택된 입력 열 목록입니다.|  
|CacheColumnName|문자열|선택된 입력 열에 매핑된 열의 이름을 지정합니다.<br /><br /> CacheColumnName 속성의 열 이름은 **캐시 연결 관리자 편집기** 의 **열**페이지에 나열된 해당 열 이름과 일치해야 합니다.<br /><br /> 자세한 내용은 [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md)를 참조하세요.|  
  
##  <a name="charmap"></a> 문자표 변환 사용자 지정 속성  
 문자표 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
 다음 표에서는 문자표 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|정수|출력 열의 원본인 입력 열의 **LineageID** 를 지정하는 값입니다.|  
|MapFlags|Integer(열거형)|열에서 문자표 변환이 수행하는 문자열 연산을 지정하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **바이트 반전** (2)<br /><br /> **전자** (6)<br /><br /> **반자** (5)<br /><br /> **히라가나** (3)<br /><br /> **가타카나** (4)<br /><br /> **대/소문자 구분 기능** (7)<br /><br /> **소문자** (0)<br /><br /> **중국어(간체)** (8)<br /><br /> **중국어(번체)**(9)<br /><br /> **대문자** (1)|  
  
 문자표 변환의 입력, 입력 열 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Character Map Transformation](../../../integration-services/data-flow/transformations/character-map-transformation.md)을 참조하세요.  
  
##  <a name="condsplit"></a> 조건부 분할 변환 사용자 지정 속성  
 조건부 분할 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
 다음 표에서는 조건부 분할 변환 출력의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|EvaluationOrder|정수|조건부 분할 변환이 평가하는 조건 목록에서 출력과 연결된 조건의 위치를 지정하는 값입니다. 조건은 가장 낮은 값에서 가장 높은 값의 순서로 평가됩니다.|  
|식|문자열|조건부 분할 변환이 평가하는 조건을 나타내는 식입니다. 열은 계보 식별자로 나타납니다.|  
|FriendlyExpression|문자열|조건부 분할 변환이 평가하는 조건을 나타내는 식입니다. 열은 해당 이름으로 나타납니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
|IsDefaultOut|Boolean|출력이 기본 출력인지 여부를 나타내는 값입니다.|  
  
 조건부 분할 변환의 입력, 입력 열 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)을 참조하세요.  
  
##  <a name="copymap"></a> 열 복사 변환 사용자 지정 속성  
 열 복사 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
 다음 표에서는 열 복사 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|copyColumnId|정수|출력 열을 복사해 온 입력 열의 **LineageID** 입니다.|  
  
 열 복사 변환의 입력, 입력 열 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Copy Column Transformation](../../../integration-services/data-flow/transformations/copy-column-transformation.md)을 참조하세요.  
  
##  <a name="dataconv"></a> 데이터 변환 사용자 지정 속성  
 데이터 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
 다음 표에서는 데이터 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|FastParse|Boolean|열이 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 에서 제공하는 더 빠르지만 로캘을 구분하지 않는 빠른 구문 분석 루틴을 사용하는지, 아니면 로캘을 구분하는 표준 구문 분석 루틴을 사용하는지를 나타내는 값입니다. 이 속성의 기본값은 **False**입니다. 자세한 내용은 [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 및 [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)를 참조하세요. 을 참조하십시오.<br /><br /> 참고: 이 속성은 **데이터 변환 편집기**에서는 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수는 있습니다.|  
|SourceInputColumnLineageId|정수|출력 열의 원본인 입력 열의 **LineageID** 입니다.|  
  
 데이터 변환의 입력, 입력 열 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)을 참조하세요.  
  
##  <a name="dmquery"></a> 데이터 마이닝 쿼리 변환 사용자 지정 속성  
 데이터 마이닝 쿼리 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 데이터 마이닝 쿼리 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|ASConnectionId|문자열|연결 개체의 고유 식별자입니다.|  
|ASConnectionString|문자열|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 프로젝트 또는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 연결 문자열입니다.|  
|CatalogName|문자열|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터베이스의 이름입니다.|  
|ModelName|문자열|데이터 마이닝 모델의 이름입니다.|  
|ModelStructureName|문자열|마이닝 구조의 이름입니다.|  
|ObjectRef|문자열|변환에서 사용하는 데이터 마이닝 구조를 식별하는 XML 태그입니다.|  
|QueryText|문자열|변환에서 사용하는 예측 쿼리 문입니다.|  
  
 데이터 마이닝 쿼리 변환의 입력, 입력 열, 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Data Mining Query Transformation](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)을 참조하세요.  
  
##  <a name="derived"></a> 파생 열 변환 사용자 지정 속성  
 파생 열 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
 다음 표에서는 파생 열 변환 입력 열 및 출력 열의 사용자 지정 속성을 설명합니다. 파생 열을 새 열로 추가하는 경우 이러한 사용자 지정 속성이 새 출력 열에 적용됩니다. 기존 입력 열의 내용을 파생 결과로 바꾸는 경우에는 이러한 사용자 지정 속성이 기존 입력 열에 적용됩니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|식|문자열|조건부 분할 변환이 평가하는 조건을 나타내는 식입니다. 열은 해당 열의 **LineageID** 속성으로 나타납니다.|  
|FriendlyExpression|문자열|조건부 분할 변환이 평가하는 조건을 나타내는 식입니다. 열은 해당 이름으로 나타납니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
  
 파생 열 변환의 입력 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Derived Column Transformation](../../../integration-services/data-flow/transformations/derived-column-transformation.md)을 참조하세요.  
  
##  <a name="extract"></a> 열 내보내기 변환 사용자 지정 속성  
 열 내보내기 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
 다음 표에서는 열 내보내기 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|AllowAppend|Boolean|변환에서 기존 파일에 데이터를 추가하는지 여부를 지정하는 값입니다. 이 속성의 기본값은 **False**입니다.|  
|ForceTruncate|Boolean|변환에서 데이터를 쓰기 전에 기존 파일을 자르는지 여부를 지정하는 값입니다. 이 속성의 기본값은 **False**입니다.|  
|FileDataColumnID|정수|변환에서 파일에 삽입하는 데이터가 포함된 열을 식별하는 값입니다. 추출 열에서 이 속성의 값은 **0**입니다. 파일 경로 열에서 이 속성에는 추출 열의 **LineageID** 가 포함됩니다.|  
|WriteBOM|Boolean|파일에 BOM(바이트 순서 표시)을 쓸지 여부를 지정하는 값입니다.|  
  
 열 내보내기 변환의 입력, 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Export Column Transformation](../../../integration-services/data-flow/transformations/export-column-transformation.md)을 참조하세요.  
  
##  <a name="insert"></a> 열 가져오기 변환 사용자 지정 속성  
 열 가져오기 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
 다음 표에서는 열 가져오기 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|ExpectBOM|Boolean|열 가져오기 변환에 BOM(바이트 순서 표시)이 필요한지 여부를 지정하는 값입니다. BOM은 데이터가 DT_NTEXT 데이터 형식인 경우에만 필요합니다.|  
|FileDataColumnID|정수|변환에서 데이터 흐름에 삽입하는 데이터가 포함된 열을 식별하는 값입니다. 삽입할 데이터 열에서 이 속성의 값은 0입니다. 원본 파일 경로가 포함된 열에서 이 속성에는 삽입할 데이터 열의 **LineageID** 가 포함됩니다.|  
  
 열 가져오기 변환의 입력, 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Import Column Transformation](../../../integration-services/data-flow/transformations/import-column-transformation.md)을 참조하세요.  
  
##  <a name="fgroup"></a> 유사 항목 그룹화 변환 사용자 지정 속성  
 유사 항목 그룹화 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 유사 항목 그룹화 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|Delimiters|문자열|변환에서 사용하는 토큰 구분 기호입니다. 기본 구분 기호는 문자는 포함: 공백 (), 쉼표 (,), 마침표 (.), 세미콜론 (;), 콜론 (:), 하이픈 (-), 곧은 따옴표 ("), 단일 곧은 따옴표 (') 두 번 앰퍼샌드 (&), 슬래시 기호 (/), 백슬래시 (\\), at 기호 (@), 느낌표 (!), 괄호 ((), 닫는 괄호 ())를 열어 물음표 (?) 미만 (\<), 보다 큼 (>), 여는 대괄호 (), 닫는 대괄호 (]), 여는 중괄호 ({}), 닫는 중괄호 (}), 파이프 (&#124;), 숫자 기호 (#), 별표 (*), 캐럿 (^) 및 백분율 (%).|  
|Exhaustive|Boolean|각 입력 레코드를 다른 모든 입력 레코드와 비교할지 여부를 지정하는 값입니다. 값 **True** 는 대개 디버깅용으로 사용됩니다. 이 속성의 기본값은 **False**입니다.<br /><br /> 참고: 이 속성은 **유사 항목 그룹화 변환 편집기**에서는 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수는 있습니다.|  
|MaxMemoryUsage|정수|변환에서 사용할 최대 메모리 양입니다. 이 속성의 기본값은 동적 메모리 사용을 가능하게 하는 **0**입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.<br /><br /> 참고: 이 속성은 **유사 항목 그룹화 변환 편집기**에서는 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수는 있습니다.|  
|MinSimilarity|Double|중복을 식별하기 위해 변환에서 사용하는 유사성 임계값으로, 0에서 1 사이의 값으로 나타납니다.  이 속성의 기본값은 0.8입니다.|  
  
 다음 표에서는 유사 항목 그룹화 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|ExactFuzzy|Integer(열거형)|변환에서 유사 일치를 수행하는지, 아니면 정확히 일치를 수행하는지를 지정하는 값입니다. 유효한 값은 **정확** 및 **유사**입니다. 이 속성의 기본값은 **유사**입니다.|  
|FuzzyComparisonFlags|Integer(열거형)|변환에서 열의 문자열 데이터를 비교하는 방법을 지정하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **FullySensitive**<br /><br /> **IgnoreCase**<br /><br /> **IgnoreKanaType**<br /><br /> **IgnoreNonSpace**<br /><br /> **IgnoreSymbols**<br /><br /> **IgnoreWidth**<br /><br /> <br /><br /> 자세한 내용은 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)을 참조하세요.|  
|LeadingTrailingNumeralsSignificant|Integer(열거형)|숫자의 의미를 지정하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **NumeralsNotSpecial** (0) - 숫자에 의미가 없는 경우 사용합니다.<br /><br /> **LeadingNumeralsSignificant** (1) - 선행 숫자에 의미가 있는 경우 사용합니다.<br /><br /> **TrailingNumeralsSignificant** (2) - 후행 숫자에 의미가 있는 경우 사용합니다.<br /><br /> **LeadingAndTrailingNumeralsSignificant** (3) - 선행 및 후행 숫자 모두에 의미가 있는 경우 사용합니다.|  
|MinSimilarity|Double|열의 조인에 사용되는 유사성 임계값으로, 0에서 1 사이의 값으로 지정됩니다. 임계값보다 큰 행만 일치하는 것으로 간주됩니다.|  
|ToBeCleaned|Boolean|열이 중복을 식별하는 데 사용되는지, 즉 이 열이 그룹화하는 열인지 여부를 지정하는 값입니다. 이 속성의 기본값은 **False**입니다.|  
  
 다음 표에서는 유사 항목 그룹화 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|ColumnType|Integer(열거형)|출력 열의 유형을 식별하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **Undefined** (0)<br /><br /> **KeyIn** (1)<br /><br /> **KeyOut** (2)<br /><br /> **Similarity** (3)<br /><br /> **ColumnSimilarity** (4)<br /><br /> **PassThru** (5)<br /><br /> **Canonical**(6)|  
|InputID|정수|해당 입력 열의 **LineageID** 입니다.|  
  
 유사 항목 그룹화 변환의 입력 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)을 참조하세요.  
  
##  <a name="flookup"></a> 유사 항목 조회 변환 사용자 지정 속성  
 유사 항목 조회 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 유사 항목 조회 변환의 사용자 지정 속성을 설명합니다. **ReferenceMetadataXML** 을 제외한 모든 속성이 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|CopyReferenceTable|Boolean|유사 항목 조회 인덱스 생성 및 후속 조회를 위해 참조 테이블의 복사본을 만들지 여부를 지정합니다. 이 속성의 기본값은 **True**입니다.|  
|Delimiters|문자열|변환에서 열 값을 토큰화하는 데 사용하는 구분 기호입니다. 다음 문자를 포함 하는 기본 구분 기호는: 공백 (), 쉼표 (,), 마침표 (.) 세미콜론 (;), 콜론 (:) 하이픈 (-), 곧은 따옴표 ("), 단일 곧은 따옴표 (')를 두 번 앰퍼샌드 (&), 슬래시 기호 (/), 백슬래시 (\\), at 기호 (@), 느낌표 (!), 물음표 (?), 닫는 괄호 ()), 여는 괄호 (() 보다 작은 (\<), 보다 큼 (>), 여는 대괄호 (), 닫는 대괄호 (]), 여는 중괄호 ({}), 닫는 중괄호 (}), 파이프 (&#124;). 숫자 기호(#), 별표(*), 캐럿(^) 및 백분율(%) 문자가 포함됩니다.|  
|DropExistingMatchIndex|Boolean|MatchIndexOptions가 ReuseExistingIndex로 설정되지 않은 경우 MatchIndexName에 지정된 일치 인덱스가 삭제되는지 여부를 지정하는 값입니다. 이 속성의 기본값은 **True**입니다.|  
|Exhaustive|Boolean|각 입력 레코드를 다른 모든 입력 레코드와 비교할지 여부를 지정하는 값입니다. 값 **True** 는 대개 디버깅용으로 사용됩니다. 이 속성의 기본값은 **False**입니다.<br /><br /> 참고: 이 속성은 **유사 항목 조회 변환 편집기**에서는 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수는 있습니다.|  
|MatchIndexName|문자열|일치 인덱스의 이름입니다. 일치 인덱스는 변환에서 만들어 사용 인덱스를 저장하는 테이블입니다. 일치 인덱스가 다시 사용되는 경우 MatchIndexName에서 다시 사용할 인덱스를 지정합니다. MatchIndexName은 유효한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 식별자 이름이어야 합니다. 예를 들어 이름에 공백이 포함된 경우 이름을 대괄호로 묶어야 합니다.|  
|MatchIndexOptions|Integer(열거형)|변환에서 일치 인덱스를 관리하는 방법을 지정하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **ReuseExistingIndex** (0)<br /><br /> **GenerateNewIndex** (1)<br /><br /> **GenerateAndPersistNewIndex** (2)<br /><br /> **GenerateAndMaintainNewIndex** (3)|  
|MaxMemoryUsage|정수|조회 테이블의 최대 캐시 크기입니다. 이 속성의 기본값은 캐시 크기에 제한이 없음을 의미하는 **0**입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.<br /><br /> 참고: 이 속성은 **유사 항목 조회 변환 편집기**에서는 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수는 있습니다.|  
|MaxOutputMatchesPerInput|정수|변환에서 각 입력 행에 대해 반환할 수 있는 최대 일치 항목 수입니다. 이 속성의 기본값은 **1**입니다.<br /><br /> 참고: 100보다 큰 값은 **고급 편집기**를 사용해야 지정할 수 있습니다.|  
|MinSimilarity|정수|변환이 구성 요소 수준에서 사용하는 유사성 임계값으로, 0에서 1 사이의 값으로 지정됩니다. 임계값보다 큰 행만 일치하는 것으로 간주됩니다.|  
|ReferenceMetadataXML|문자열|[!INCLUDE[ssInternalOnly](../../../includes/ssinternalonly-md.md)]|  
|ReferenceTableName|문자열|조회 테이블의 이름입니다. 이 이름은 유효한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 식별자 이름이어야 합니다. 예를 들어 이름에 공백이 포함된 경우 이름을 대괄호로 묶어야 합니다.|  
|WarmCaches|Boolean|True인 경우 실행이 시작되기 전에 조회에서 인덱스와 참조 테이블을 메모리에 부분적으로 로드합니다. 이로 인해 성능이 향상될 수 있습니다.|  
  
 다음 표에서는 유사 항목 조회 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|FuzzyComparisonFlags|정수|변환에서 열의 문자열 데이터를 비교하는 방법을 지정하는 값입니다. 자세한 내용은 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)을 참조하세요.|  
|FuzzyComparisonFlagsEx|Integer(열거형)|변환에서 사용하는 확장 비교 플래그를 지정하는 값입니다. 이 값에는 **MapExpandLigatures, MapFoldCZone**, **MapFoldDigits**, **MapPrecomposed**및 **NoMapping**이 포함될 수 있습니다. **NoMapping** 은 다른 플래그와 함께 사용할 수 없습니다.|  
|JoinToReferenceColumn|문자열|열이 조인된 참조 테이블의 열 이름을 지정하는 값입니다.|  
|JoinType|정수|변환에서 유사 일치를 수행하는지, 아니면 정확히 일치를 수행하는지를 지정하는 값입니다. 이 속성의 기본값은 **유사**입니다. 정확히 조인 유형의 정수 값은 **1** 이며 유사 항목 조인 유형의 값은 **2**입니다.|  
|MinSimilarity|Double|변환이 열 수준에서 사용하는 유사성 임계값으로, 0에서 1 사이의 값으로 지정됩니다. 임계값보다 큰 행만 일치하는 것으로 간주됩니다.|  
  
 다음 표에서는 유사 항목 조회 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
> [!NOTE]  
>  해당 입력 열의 통과 값이 포함된 출력 열의 경우 CopyFromReferenceColumn은 비어 있고 SourceInputColumnLineageID에는 해당 입력 열의 **LineageID** 가 포함됩니다. 조회 결과가 포함된 출력 열의 경우 CopyFromReferenceColumn에는 조회 열의 이름이 포함되며 SourceInputColumnLineageID는 비어 있습니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|ColumnType|Integer(열거형)|변환에서 출력에 추가하는 열에 대한 출력 열의 유형을 식별하는 값입니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **Undefined** (0)<br /><br /> **Similarity** (1)<br /><br /> **Confidence** (2)<br /><br /> **ColumnSimilarity** (3)|  
|CopyFromReferenceColumn|문자열|출력 열의 값을 제공하는 참조 테이블의 열 이름을 지정하는 값입니다.|  
|SourceInputColumnLineageId|정수|이 출력 열에 값을 제공하는 입력 열을 식별하는 값입니다.|  
  
 유사 항목 조회 변환의 입력 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)을 참조하세요.  
  
##  <a name="lookup"></a> 조회 변환 사용자 지정 속성  
 조회 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 조회 변환의 사용자 지정 속성을 설명합니다. **ReferenceMetadataXML** 을 제외한 모든 속성이 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|CacheType|Integer(열거형)|조회 테이블의 캐시 유형입니다. 값으로는 **전체** (0), **부분** (1) 및 **없음** (2)이 있습니다. 이 속성의 기본값은 **전체**입니다.|  
|DefaultCodePage|정수|데이터 원본에서 코드 페이지 정보를 사용할 수 없을 경우 사용할 기본 코드 페이지입니다.|  
|MaxMemoryUsage|정수|조회 테이블의 최대 캐시 크기입니다. 이 속성의 기본값은 캐시 크기에 제한이 없음을 의미하는 **25**입니다.|  
|MaxMemoryUsage64|정수|64비트 컴퓨터에서 조회 테이블의 최대 캐시 크기입니다.|  
|NoMatchBehavior|Integer(열거형)|참조 데이터 집합에서 일치 항목이 없는 열을 오류로 처리할지 여부를 지정하는 값입니다.<br /><br /> 속성이 **일치하는 항목이 없는 행을 오류로 처리합니다.** (0)로 설정된 경우 일치하는 항목이 없는 행이 오류로 처리됩니다. **조회 변환 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 이러한 유형의 오류가 발생할 때 수행할 작업을 지정할 수 있습니다. 자세한 내용은 [조회 변환 편집기&#40;오류 출력 페이지&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)를 참조하세요.<br /><br /> 속성이 **일치하는 항목이 없는 행을 불일치 항목 출력으로 보냅니다.**(1)로 설정된 경우 행이 오류로 처리되지 않습니다.<br /><br /> 기본값은 **일치하는 항목이 없는 행을 오류로 처리합니다.** (0)입니다.|  
|ParameterMap|문자열|**SqlCommand** 문에 사용된 매개 변수에 매핑되는 계보 ID를 세미콜론으로 구분한 목록입니다.|  
|ReferenceMetadataXML|문자열|변환에서 해당 출력에 복사하는 조회 테이블의 열에 대한 메타데이터입니다.|  
|SqlCommand|문자열|조회 테이블을 채우는 SELECT 문입니다.|  
|SqlCommandParam|문자열|조회 테이블을 채우는 매개 변수가 있는 SQL 문입니다.|  
  
 다음 표에서는 조회 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|CopyFromReferenceColumn|문자열|열을 복사해 올 참조 테이블의 열 이름입니다.|  
|JoinToReferenceColumns|문자열|원본 열이 조인되는 참조 테이블의 열 이름입니다.|  
  
 다음 표에서는 조회 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|CopyFromReferenceColumn|문자열|열을 복사해 올 참조 테이블의 열 이름입니다.|  
  
 조회 변환의 입력 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)을(를) 참조하세요.  
  
##  <a name="mjoin"></a> 병합 조인 변환 사용자 지정 속성  
 병합 조인 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 병합 조인 변환의 사용자 지정 속성을 설명합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|JoinType|Integer(열거형)|조인이 내부 조인(2), 왼쪽 우선 외부 조인(1), 완전 조인(0) 중 어느 것인지 여부를 지정합니다.|  
|MaxBuffersPerInput|정수|병합 조인 변환에서 과도한 메모리를 사용할 위험을 줄이기 위해 Microsoft에서 필요한 변경을 수행했기 때문에 더 이상 **MaxBuffersPerInput** 속성 값을 구성할 필요가 없습니다. 과도한 메모리가 사용되는 문제는 여러 병합 조인 입력에서 균일하지 않은 속도로 데이터를 생성하는 경우에 발생합니다.|  
|NumKeyColumns|정수|조인에 사용되는 열 수입니다.|  
|TreatNullsAsEqual|Boolean|변환에서 Null 값을 같은 값으로 처리하는지 여부를 지정하는 값입니다. 이 속성의 기본값은 **True**입니다. 속성 값이 **False**인 경우 변환에서는 Null 값을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서와 같이 처리합니다.|  
  
 다음 표에서는 병합 조인 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|InputColumnID|정수|데이터를 이 출력 열로 복사해 올 입력 열의 **LineageID** 입니다.|  
  
 병합 조인 변환의 입력, 입력 열 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Merge Join Transformation](../../../integration-services/data-flow/transformations/merge-join-transformation.md)을 참조하세요.  
  
##  <a name="oledbcmd"></a> OLE DB 명령 변환 사용자 지정 속성  
 OLE DB 명령 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 OLE DB 명령 변환의 사용자 지정 속성을 설명합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|CommandTimeOut|정수|제한 시간이 초과될 때까지 SQL 명령을 실행할 수 있는 최대 시간(초)입니다. 값 **0** 은 제한 시간이 없음을 의미합니다. 이 속성의 기본값은 **0**입니다.|  
|DefaultCodePage|정수|데이터 원본에서 코드 페이지 정보를 사용할 수 없을 경우 사용할 코드 페이지입니다.|  
|SqlCommand|문자열|데이터 흐름의 각 행에 대해 변환에서 실행하는 Transact-SQL 문입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
  
 다음 표에서는 OLE DB 명령 변환 외부 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|DBParamInfoFlag|Integer(비트 마스크)|매개 변수 특징을 설명하는 플래그 집합입니다. 자세한 내용은 MSDN Library의 OLE DB 설명서에서 DBPARAMFLAGSENUM을 참조하십시오.|  
  
 OLE DB 명령 변환의 입력, 입력 열, 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [OLE DB Command Transformation](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)을 참조하세요.  
  
##  <a name="percent"></a> 비율 샘플링 변환 사용자 지정 속성  
 비율 샘플링 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 비율 샘플링 변환의 사용자 지정 속성을 설명합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|SamplingSeed|정수|난수 생성기에서 사용하는 초기값입니다. 이 속성의 기본값은 변환에서 틱 수를 사용함을 나타내는 **0**입니다.|  
|SamplingValue|정수|원본의 비율로 나타내는 샘플의 크기입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
  
 다음 표에서는 비율 샘플링 변환 출력의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|선택|Boolean|샘플링된 행을 전송할 출력을 지정합니다. 선택된 출력에서는 Selected가 **True**로 설정되고, 선택되지 않은 출력에서는 **False**로 설정됩니다.|  
  
 비율 샘플링 변환의 입력, 입력 열 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)을 참조하세요.  
  
##  <a name="pivot"></a> 피벗 변환 사용자 지정 속성  
 다음 표에서는 피벗 변환을 위한 사용자 지정 구성 요소 속성을 설명합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|**PassThroughUnmatchedPivotKeyts**|Boolean|패키지를 실행할 때 피벗 키 열에서 인식되지 않은 값이 포함된 행을 무시하고 모든 피벗 키 값을 로그 메시지로 출력하도록 피벗 변환을 구성하려면 **True** 로 설정합니다.|  
  
 다음 표에서는 피벗 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|PivotUsage|Integer(열거형)|데이터 집합이 피벗될 때의 열 역할을 지정하는 값입니다.<br /><br /> **0**:<br />                      열이 피벗되지 않고 열 값만 변환 출력으로 전달됩니다.<br /><br /> **1**:<br />                      열이 하나 이상의 행을 한 집합의 일부로 식별하는 집합 키의 일부입니다. 동일 집합 키의 모든 입력 행이 하나의 출력 행으로 조합됩니다.<br /><br /> **2**:<br />                      열이 피벗 열입니다. 각 열 값으로부터 적어도 하나 이상의 열이 생성됩니다.<br /><br /> **3**:<br />                      이 열의 값이 피벗 결과로 생성된 열에 배치됩니다.|  
  
 다음 표에서는 피벗 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|PivotKeyValue|문자열|해당 PivotUsage 속성의 값에 따라 피벗 키로 표시되는 열에서 가능한 값 중 하나입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
|SourceColumn|정수|피벗된 값이 포함된 입력 열의 **LineageID** 또는 -1입니다. 값 -1은 해당 열이 피벗 작업에 사용되지 않음을 나타냅니다.|  
  
 자세한 내용은 [Pivot Transformation](../../../integration-services/data-flow/transformations/pivot-transformation.md)을 참조하세요.  
  
##  <a name="rowcount"></a> 행 개수 변환 사용자 지정 속성  
 행 개수 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 행 개수 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|VariableName|문자열|행 개수를 보유하는 변수의 이름입니다.|  
  
 행 개수 변환의 입력, 입력 열, 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Row Count Transformation](../../../integration-services/data-flow/transformations/row-count-transformation.md)을 참조하세요.  
  
##  <a name="rowsamp"></a> 행 샘플링 변환 사용자 지정 속성  
 행 샘플링 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 행 샘플링 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|SamplingSeed|정수|난수 생성기에서 사용하는 초기값입니다. 이 속성의 기본값은 변환에서 틱 수를 사용함을 나타내는 **0**입니다.|  
|SamplingValue|정수|샘플의 행 수입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
  
 다음 표에서는 행 샘플링 변환 출력의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|선택|Boolean|샘플링된 행을 전송할 출력을 지정합니다. 선택된 출력에서는 Selected가 **True**로 설정되고, 선택되지 않은 출력에서는 **False**로 설정됩니다.|  
  
 다음 표에서는 행 샘플링 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|정수|출력 열의 원본인 입력 열의 **LineageID** 를 지정하는 값입니다.|  
  
 행 샘플링 변환의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)을(를) 참조하세요.  
  
##  <a name="script"></a> 스크립트 구성 요소 사용자 지정 속성  
 스크립트 구성 요소에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다. 스크립트 구성 요소가 원본, 변환, 대상 중 어느 것으로 사용되는지 여부에 관계없이 같은 사용자 지정 속성을 사용할 수 있습니다.  
  
 다음 표에서는 스크립트 구성 요소의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|ReadOnlyVariables|문자열|읽기 전용 액세스 권한으로 스크립트 구성 요소에 대해 사용할 수 있는 쉼표로 구분된 변수 목록입니다.|  
|ReadWriteVariables|문자열|읽기/쓰기 액세스 권한으로 스크립트 구성 요소에 대해 사용할 수 있는 쉼표로 구분된 변수 목록입니다.|  
  
 스크립트 구성 요소의 입력, 입력 열, 출력 및 출력 열에는 스크립트 개발자가 해당 항목의 사용자 지정 속성을 만들지 않는 한 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Script Component](../../../integration-services/data-flow/transformations/script-component.md)를 참조하세요.  
  
##  <a name="scd"></a> 느린 변경 차원 변환 사용자 지정 속성  
 느린 변경 차원 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 느린 변경 차원 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|CurrentRowWhere|문자열|비즈니스 키가 같은 행 중 현재 행을 선택하는 SELECT 문의 WHERE 절입니다.|  
|EnableInferredMember|Boolean|유추 멤버 업데이트를 검색할지 여부를 지정하는 값입니다. 이 속성의 기본값은 **True**입니다.|  
|FailOnFixedAttributeChange|Boolean|고정 특성이 있는 행 열에 변경 내용이 포함되어 있거나 차원 테이블의 조회가 실패하는 경우 변환이 실패하는지 여부를 지정하는 값입니다. 들어오는 행에 새 레코드가 포함될 경우 이 값을 **True** 로 설정하면 조회가 실패한 후 변환이 계속됩니다. 이는 변환에서 오류를 사용하여 새 레코드를 식별하기 때문입니다. 이 속성의 기본값은 **False**입니다.|  
|FailOnLookupFailure|Boolean|기존 레코드의 조회가 실패할 때 변환이 실패하는지 여부를 지정하는 값입니다. 이 속성의 기본값은 **False**입니다.|  
|IncomingRowChangeType|정수|들어오는 모든 행이 새 행인지, 아니면 변환에서 변경 유형을 검색해야 하는지를 지정하는 값입니다.|  
|InferredMemberIndicator|문자열|유추 멤버의 열 이름입니다.|  
|SqlCommand|문자열|스키마 행 집합을 만드는 데 사용되는 SQL 문입니다.|  
|UpdateChangingAttributeHistory|Boolean|특성 업데이트 내용을 변경하기 위해 기록 특성 업데이트 내용을 변환 출력으로 전송할지 여부를 나타내는 값입니다.|  
  
 다음 표에서는 느린 변경 차원 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|ColumnType|Integer(열거형)|열의 업데이트 유형입니다. 값으로는 **변경 특성** (2), **고정 특성** (4), **기록 특성** (3), **키** (1) 및 **기타** (0)가 있습니다.|  
  
 느린 변경 차원 변환의 입력, 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)을 참조하세요.  
  
##  <a name="sort"></a> 정렬 변환 사용자 지정 속성  
 정렬 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 정렬 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|EliminateDuplicates|Boolean|변환이 변환 출력에서 중복 행을 제거하는지 여부를 지정합니다. 이 속성의 기본값은 **False**입니다.|  
|MaximumThreads|정수|변환에서 정렬에 사용할 수 있는 최대 스레드 수를 포함합니다. 값 **0** 은 스레드 수 제한이 없음을 의미합니다. 이 속성의 기본값은 **0**입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.|  
  
 다음 표에서는 정렬 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|NewComparisonFlags|Integer(비트 마스크)|변환에서 열의 문자열 데이터를 비교하는 방법을 지정하는 값입니다. 자세한 내용은 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)을 참조하세요.|  
|NewSortKeyPosition|정수|열의 정렬 순서를 지정하는 값입니다. 값 0은 이 열에서 데이터가 정렬되지 않음을 나타냅니다.|  
  
 다음 표에서는 정렬 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|SortColumnID|정수|정렬 열의 **LineageID** 입니다.|  
  
 정렬 변환의 입력 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Sort Transformation](../../../integration-services/data-flow/transformations/sort-transformation.md)을 참조하세요.  
  
##  <a name="textract"></a> 용어 추출 변환 사용자 지정 속성  
 용어 추출 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 용어 추출 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|--------------|-----------------|  
|FrequencyThreshold|정수|용어가 추출되기 전에 발생해야 하는 횟수를 나타내는 숫자 값입니다. 이 속성의 기본값은 **2**입니다.|  
|IsCaseSensitive|Boolean|명사 및 명사구를 추출할 때 대/소문자 구분을 사용할지 여부를 지정하는 값입니다. 이 속성의 기본값은 **False**입니다.|  
|MaxLengthOfTerm|정수|용어의 최대 길이를 나타내는 숫자 값입니다. 이 속성은 구에만 적용됩니다. 이 속성의 기본값은 **12**입니다.|  
|NeedRefenceData|Boolean|변환에서 참조 테이블에 저장된 제외 용어 목록을 사용할지 여부를 지정하는 값입니다. 이 속성의 기본값은 **False**입니다.|  
|OutTermColumn|문자열|제외 용어가 포함된 열의 이름입니다.|  
|OutTermTable|문자열|제외 용어가 있는 열이 포함된 테이블의 이름입니다.|  
|ScoreType|정수|용어와 연결할 점수 유형을 지정하는 값입니다. 유효한 값으로는 빈도를 나타내는 0과 TFIDF 점수를 나타내는 1이 있습니다. TFIDF 점수는 TF(용어 빈도)와 IDF(역 문서 빈도)의 곱으로, 용어 T의 TFIDF = (T의 빈도) \* log((입력의 행 수)/(T를 포함하는 행 수))와 같이 정의됩니다. 이 속성의 기본값은 **0**입니다.|  
|WordOrPhrase|정수|용어 유형을 지정하는 값입니다. 유효한 값으로는 단어만 나타내는 0, 명사구만 나타내는 1 및 단어와 명사구를 모두 나타내는 2가 있습니다. 이 속성의 기본값은 **0**입니다.|  
  
 용어 추출 변환의 입력, 입력 열, 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)을 참조하세요.  
  
##  <a name="tlookup"></a> 용어 조회 변환 사용자 지정 속성  
 용어 조회 변환에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 용어 조회 변환의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|IsCaseSensitive|Boolean|입력 열 텍스트와 조회 용어를 비교할 때 대/소문자 구분 비교를 적용할지 여부를 지정하는 값입니다. 이 속성의 기본값은 **False**입니다.|  
|RefTermColumn|문자열|조회 용어가 포함된 열의 이름입니다.|  
|RefTermTable|문자열|조회 용어가 있는 열이 포함된 테이블의 이름입니다.|  
  
 다음 표에서는 용어 조회 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|InputColumnType|정수|열 사용을 지정하는 값입니다. 유효한 값으로는 통과 열의 경우 0, 조회 열의 경우 1 및 통과 열이면서 조회 열인 열의 경우 2가 있습니다.|  
  
 다음 표에서는 용어 조회 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|CustomLineageID|정수|해당 열의 **LineageID** 이 0 또는 2인 경우 해당 입력 열의 **InputColumnType** 입니다.|  
  
 용어 조회 변환의 입력 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Term Lookup Transformation](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)을 참조하세요.  
  
##  <a name="unpivot"></a> 피벗 해제 변환 사용자 지정 속성  
 피벗 해제 변환에는 구성 요소 수준의 모든 데이터 흐름 구성 요소에 공통된 속성만 있습니다.  
  
> [!NOTE]  
>  이 섹션에서는 [피벗 해제 변환](../../../integration-services/data-flow/transformations/unpivot-transformation.md) 에 설명된 피벗 해제 시나리오를 사용하여 여기에서 설명하는 옵션의 사용 방법을 보여 줍니다.  
  
 다음 표에서는 피벗 해제 변환 입력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|Description|  
|--------------|---------------|-----------------|  
|DestinationColumn|정수|입력 열이 매핑되는 출력 열의 **LineageID** 입니다. 값 -1은 입력 열이 출력 열에 매핑되지 않음을 나타냅니다.|  
|PivotKeyValue|문자열|변환 출력 열에 복사되는 값입니다.<br /><br /> 이 속성의 값은 속성 식을 사용하여 지정할 수 있습니다.<br /><br /> [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)에 설명된 피벗 해제 시나리오에서 Pivot Value는 Ham, Coke, Milk, Beer 및 Chips와 같은 텍스트 값입니다. 이러한 값은 **피벗 키 값 열 이름** 옵션으로 지정한 새 Product 열에 텍스트 값으로 나타납니다.|  
  
 다음 표에서는 피벗 해제 변환 출력 열의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|PivotKey|Boolean|입력 열의 **PivotKeyValue** 속성에 있는 값을 이 출력 열에 쓸지 여부를 나타냅니다.<br /><br /> [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)에 설명된 피벗 해제 시나리오에서 Pivot Value 열 이름은 **Product** 이며 Ham, Coke, Milk, Beer 및 Chips 열이 피벗 해제되는 새 **Product** 열을 지정합니다.|  
  
 피벗 해제 변환의 입력 및 출력에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Unpivot Transformation](../../../integration-services/data-flow/transformations/unpivot-transformation.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 변환](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [공용 속성](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)   
 [경로 속성](http://msdn.microsoft.com/library/89b1e347-9579-4f6b-af74-c6519ea08eea)   
 [식을 사용 하 여 설정할 수 있는 데이터 흐름 속성](http://msdn.microsoft.com/library/cd0e171a-08be-45d6-81dc-ed94f37698b8)  
  
  
