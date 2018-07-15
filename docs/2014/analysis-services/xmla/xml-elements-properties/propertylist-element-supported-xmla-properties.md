---
title: 지원 되는 XMLA 속성 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- properties [XML for Analysis]
- XML for Analysis, properties
- XMLA, properties
ms.assetid: 5745f7b4-6b96-44d5-b77c-f2831a898e5e
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04e2b96df0cc549acadd50d80356a62bf327b7c3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243963"
---
# <a name="supported-xmla-properties-xmla"></a>지원되는 XMLA 속성(XMLA)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 다음 표에 나열 된 속성을 지원 합니다. 이러한 나열 된 속성을 사용 합니다 [속성](properties-element-xmla.md) 의 요소를 [검색](../xml-elements-methods-discover.md) 및 [Execute](../xml-elements-methods-execute.md) 메서드.  
  
|속성|요소|  
|----------|-------------|  
|AxisFormat|*사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 내에서 사용 되는 형식을 결정 하는 [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) 다차원 데이터 집합의 축을 설명 하기 위해 결과 집합입니다. 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*ClusterFormat*|합니다 `MDDataSet` 하나 이상의 축 이루어집니다 [CrossProduct](crossproduct-element-xmla.md) 요소입니다.|  
|*CustomFormat*|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 사용 하는 *TupleFormat* 이 설정에 대 한 형식입니다.|  
|*TupleFormat*|(기본값) 합니다 `MDDataSet` 하나 이상 포함 되어 있는 축 [튜플](tuple-element-xmla.md) 요소입니다.|  
  
 이 속성은 `Execute` 메서드와 함께 사용할 수 있습니다.  
  
|속성|요소|  
|----------|-------------|  
|BeginRange|*사용법*<br /> 쓰기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> `CellOrdinal` 특성 값에 해당하는 정수 값(0부터 시작)을 포함합니다. (합니다 `CellOrdinal` 특성이 포함 되어는 [셀](cell-element-mddataset-xmla.md) 요소에는 [CellData](celldata-element-xmla.md) 부분 `MDDataSet`.)<br /><br /> 클라이언트 응용 프로그램은 `EndRange` 속성과 함께 이 속성을 사용하여 명령에 의해 반환되는 OLAP 데이터 집합을 셀의 특정 범위로 제한할 수 있습니다. -1을 지정하면 `EndRange` 속성에 지정된 셀까지 모든 셀이 반환됩니다.<br /><br /> 이 속성의 기본값은-1입니다.<br /><br /> 이 속성은 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|Catalog|*사용법*<br /> 읽기/쓰기 `String` 속성(옵션)<br /><br /> *Description*<br /> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스로 세션을 설정하여 XMLA 명령을 보내는 경우 이 속성은 OLE DB 속성인 DBPROP_INIT_CATALOG와 같습니다.<br /><br /> 세션 중 이 속성을 설정하여 세션에 대한 현재 데이터베이스를 변경하는 경우 이 속성은 OLE DB 속성인 DBPROP_CURRENTCATALOG와 같습니다.<br /><br /> 이 속성의 기본값은 빈 문자열입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|CatalogLocation|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_CATALOGLOCATION과 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_CL_START와 같은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|ClientProcessID|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 현재 세션에 대한 프로세스 스레드의 ID(식별자)를 포함합니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|CommitTimeout|*사용법*<br /> 쓰기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 롤백하기 전에 현재 실행 중인 XMLA 명령의 커밋 단계에서 대기하는 시간(초)을 결정합니다. 커밋 단계와 같은 XMLA 명령에 해당 [문](../xml-elements-commands/statement-element-xmla.md) 하거나 [프로세스](../xml-elements-commands/process-element-xmla.md)합니다.<br /><br /> 영(0) 값은 인스턴스가 무기한 대기함을 나타냅니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|콘텐츠|*사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> `Discover` 및 `Execute` 메서드에서 반환되는 데이터 형식을 결정합니다. 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|명령의 구조가 확인은 되지만 실행되지 않도록 합니다.|  
|*스키마*|요청된 명령과 관련된 XML 스키마를 반환합니다. XML 스키마는 열 및 기타 정보를 나타냅니다.|  
|*데이터*|요청된 데이터만 반환합니다.|  
|*SchemaData*|(기본값) 스키마 정보 및 데이터를 반환합니다.|  
  
 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.  
  
|속성|요소|  
|----------|-------------|  
|Cube|*사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 명령에 대한 컨텍스트를 설정하는 큐브의 이름을 포함합니다. 명령 자체에 큐브 이름이 같은 FROM 절에는 MDX (Multidimensional Expressions) 내에서 포함 하는 경우 [선택](/sql/mdx/mdx-data-manipulation-select) 문은이 속성의 설정은 무시 됩니다.<br /><br /> 이 속성의 기본값은 빈 문자열입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DataSourceInfo|*사용법*<br /> 읽기/쓰기 `String` 속성(필수)<br /><br /> *Description*<br /> 데이터 원본에 연결하는 데 필요한 인스턴스 이름과 같은 정보를 포함합니다.<br /><br /> 클라이언트 응용 프로그램은 인스턴스로 보낼 `DataSourceInfo` 속성의 내용을 구성하지 않아야 합니다. 대신 클라이언트 응용 프로그램이 사용 하 여 공급자가 지 원하는 데이터 원본을 찾아야 합니다 `Discover` 검색 하는 메서드를 [DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md) 행 집합입니다. 그런 다음 클라이언트 응용 프로그램은 DISCOVER_DATASOURCES 행 집합에서 클라이언트가 검색한 `DataSourceInfo` 속성에 대해 같은 값을 다시 보냅니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropCatalogTerm|*사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_CATALOGTERM과 같습니다.<br /><br /> 이 속성의 기본값은 "데이터베이스"입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropCatalogUsage|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_CATALOGUSAGE와 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropColumnDefinition|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_COLUMNDEFINITION과 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropConcatNullBehavior|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_CONCATNULLBEHAVIOR와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_CB_NULL과 같은 1입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropDataSourceReadOnly|*사용법*<br /> 읽기 전용 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_DATASOURCEREADONLY와 같습니다.<br /><br /> 이 속성의 기본값은 FALSE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropGroupBy|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_GROUPBY와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_GB_EQUALS_SELECT와 같은 2입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropHeterogeneousTables|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_HETEROGENEOUSTABLES와 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropIdentifierCase|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_IDENTIFIERCASE와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_IC_MIXED와 같은 8입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropInitMode|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_INIT_MODE와 같습니다.<br /><br /> 이 속성에 대해 유일하게 지원되는 값은 DB_MODE_READWRITE 및 DB_MODE_READ입니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMaxIndexSize|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_MAXINDEXSIZE와 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMaxOpenChapters|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_MAXOPENCHAPTERS와 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMaxRowSize|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_MAXROWSIZE와 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMaxRowSizeIncludeBlob|*사용법*<br /> 읽기 전용 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_MAXROWSIZEINCLUDESBLOB와 같습니다.<br /><br /> 이 속성의 기본값은 TRUE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMaxTablesInSelect|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_MAXTABLESINSELECT와 같습니다.<br /><br /> 이 속성의 기본값은 1입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdAutoexists|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> Autoexist의 동작을 결정합니다. 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*0*|기본값, 1과 동일합니다.|  
|*1.*|쿼리 축 및 명명된 집합에 대해 중첩된 AUTOEXIST를 적용합니다. WHERE 절 및 하위 SELECT를 포함합니다.|  
|*2*|쿼리 축에 대해 중첩된 Autoexist를 적용하고 Autoexist에서 명명된 집합을 제외합니다. WHERE 절 및 하위 SELECT를 포함합니다.|  
|*3*|WHERE 절의 명명된 집합에 대해 Autoexist를 적용하지 않습니다. WHERE 절의 쿼리 축에 대해 중첩되지 않은 Autoexist를 적용합니다. 하위 SELECT의 쿼리 축 및 하위 SELECT의 명명된 집합에 대해 중첩된 Autoexist를 적용합니다.|  
  
 이 속성의 기본값은 0 또는 빈 값입니다. 세션을 만들 때만 설정할 수 있는 세션 속성입니다.  
  
|속성|요소|  
|----------|-------------|  
|DbpropMsmdCacheMode|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdCachePolicy|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdCacheRatio|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdCacheRatio2|*사용법*<br /> 읽기/쓰기 `Double` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdCompareCaseNotSensitiveStringFlags|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 대/소문자 구분 문자열 비교 및 정렬 순서 기능을 결정합니다. 이 속성은 일본어의 가타카나와 힌디어처럼 대문자와 소문자를 지원하지 않는 문자 집합에서 비교가 수행되는 방식을 제어합니다. 이 속성의 값은 프로세스 스레드의 첫 번째 연결에서 설정되며 해당 프로세스 스레드의 모든 후속 연결에 영향을 줍니다.<br /><br /> 다음 표를 사용하여 사용할 플래그를 결정합니다.|  
  
|속성|값|Description|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0x00000001*|대/소문자가 무시됩니다.|  
|해당 사항 없음|*0x00000002*|이진 비교입니다. 문자는 특정 알파벳의 순서가 아닌 문자 집합의 기본 값을 기반으로 비교됩니다.|  
|NORM_IGNORENONSPACE|*0x00000010*|비공백 문자가 무시됩니다.|  
|NORM_IGNORESYMBOLS|*0x00000100*|기호가 무시됩니다.|  
|NORM_IGNOREKANATYPE|*0x00001000*|히라가나 문자와 가타카나 문자가 구별되지 않습니다. 비교 시 해당 히라가나 문자와 가타카나 문자는 같은 것으로 간주됩니다.|  
|NORM_IGNOREWIDTH|*0x00010000*|동일한 문자의 싱글바이트 버전과 더블바이트 버전이 구별되지 않습니다.|  
|SORT_STRINGSORT|*0x00100000*|문장 부호가 기호와 동일하게 처리됩니다.|  
  
 OLE DB에서의 문자열 비교 방법을 보려면 MSDN Library의 Platform SDK 섹션에서 "CompareString"을 검색하십시오.  
  
 이 속성의 기본값은 없습니다.  
  
 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.  
  
|속성|요소|  
|----------|-------------|  
|DbpropMsmdCompareCaseSensitiveStringFlags|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 대/소문자를 구분하지 않는 문자열 비교 및 정렬 순서 기능을 결정합니다. 이 속성은 일본어의 가타카나와 힌디어처럼 대문자와 소문자를 지원하지 않는 문자 집합에서 비교가 수행되는 방식을 제어합니다. 이 속성의 값은 프로세스 스레드의 첫 번째 연결에서 설정되며 해당 프로세스 스레드의 모든 후속 연결에 영향을 줍니다.<br /><br /> 다음 표를 사용하여 사용할 플래그를 결정합니다.|  
  
|속성|값|Description|  
|----------|-----------|-----------------|  
|NORM_IGNORECASE|*0x00000001*|대/소문자가 무시됩니다.|  
|해당 사항 없음|*0x00000002*|이진 비교입니다. 문자는 특정 알파벳의 순서가 아닌 문자 집합의 기본 값을 기반으로 비교됩니다.|  
|NORM_IGNORENONSPACE|*0x00000010*|비공백 문자가 무시됩니다.|  
|NORM_IGNORESYMBOLS|*0x00000100*|기호가 무시됩니다.|  
|NORM_IGNOREKANATYPE|*0x00001000*|히라가나 문자와 가타카나 문자가 구별되지 않습니다. 비교 시 해당 히라가나 문자와 가타카나 문자는 같은 것으로 간주됩니다.|  
|NORM_IGNOREWIDTH|*0x00010000*|동일한 문자의 싱글바이트 버전과 더블바이트 버전이 구별되지 않습니다.|  
|SORT_STRINGSORT|*0x00100000*|문장 부호가 기호와 동일하게 처리됩니다.|  
  
 OLE DB에서의 문자열 비교 방법을 보려면 MSDN Library의 Platform SDK 섹션에서 "CompareString"을 검색하십시오.  
  
 이 속성의 기본값은 없습니다.  
  
 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.  
  
|속성|요소|  
|----------|-------------|  
|DbpropMsmdDebugMode|*사용법*<br /> 읽기/쓰기 `String` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdDynamicDebugLimit|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdFlattened2|*사용법*<br /> 읽기/쓰기 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 부모-자식 계층이 축 0에서 요청되지 않는 한 평면화된 결과의 단일 테이블 열에 부모-자식 계층의 모든 멤버를 출력합니다. 출력 열에 대한 수준 템플릿은 사용되지 않습니다.<br /><br /> 이 속성의 기본값은 FALSE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdMDXCompatibility|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 비정형 또는 불균형 계층의 자리 표시자 멤버가 처리되는 방법을 결정합니다. 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*0*|이전 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 버전과의 호환성을 위해 이 값은 1과 같습니다.|  
|*1.*|롤플레잉 차원의 계층이 차원 이름과 계층 이름을 포함하는 캡션을 받습니다. 캡션의 형식은 다음과 같습니다.<br /><br /> [Dimension].[Hierarchy]<br /><br /> 자리 표시자 멤버가 표시됩니다.|  
|*2*|롤플레잉 차원의 계층이 차원 이름과 계층 이름을 포함하는 캡션을 받습니다. 캡션의 형식은 다음과 같습니다.<br /><br /> [Dimension].[Hierarchy]<br /><br /> 자리 표시자 멤버가 표시되지 않습니다.|  
|*3*|(기본값) 자리 표시자 멤버가 표시되지 않습니다.|  
  
 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.  
  
|속성|요소|  
|----------|-------------|  
|DbpropMsmdMDXUniqueNameStyle|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 차원의 멤버에 대해 고유한 이름을 생성하는 알고리즘을 결정합니다. 이 속성은 다음 표에 나열된 값일 수 있습니다.<br /><br /> 이 속성의 기본값은 6입니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*0*|이전 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 버전과의 호환성을 위해 이 값은 2와 같습니다.|  
|*1.*|다음과 같은 키 경로 알고리즘을 사용합니다.<br /><br /> [dim].&[key1].&[key2]|  
|*2*|다음과 같은 이름 경로 알고리즘을 사용합니다.<br /><br /> [dim].[name1].&[name2]|  
|*3*|시간이 경과해도 안정적인 보장된 고유한 이름을 사용합니다.|  
  
 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.  
  
|속성|요소|  
|----------|-------------|  
|DbpropMsmdSQLCompatibility|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMsmdSubQueries|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 하위 쿼리의 동작을 결정하는 비트 마스크입니다. 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*0*|기본값이며 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 이전 버전과 호환됩니다.<br /><br /> 계산 멤버 또는 계산 집합은 하위 SELECT 또는 하위 큐브에서 허용되지 않습니다.|  
|*1.*|계산 멤버 또는 계산 집합은 하위 SELECT 또는 하위 큐브에서 허용됩니다. 계산 멤버의 상위 항목은 하위 SELECT 또는 하위 큐브의 공간에 포함되지 않습니다.|  
|*2*|계산 멤버 또는 계산 집합은 하위 SELECT 또는 하위 큐브에서 허용됩니다. 계산 멤버의 상위 항목은 하위 SELECT 또는 하위 큐브의 공간에 포함됩니다.|  
  
 이 속성의 기본값은 0 또는 빈 값입니다.  
  
 세션을 만들 때만 설정할 수 있는 세션 속성입니다.  
  
 참조 [하위 Select 및 하위 큐브의 계산 멤버](../../multidimensional-models/mdx/calculated-members-in-subselects-and-subcubes.md) 계산된 멤버 또는 하위 select 및 하위 큐브의 계산된 집합의 동작에 대 한 자세한 설명은 대 한 합니다.  
  
|속성|요소|  
|----------|-------------|  
|DbpropMsmdUseFormulaCache|*사용법*<br /> 읽기/쓰기 `String` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropMultiTableUpdate|*사용법*<br /> 읽기 전용 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_MULTITABLEUPDATE와 같습니다.<br /><br /> 이 속성의 기본값은 FALSE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropNullCollation|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_NULLCOLLATION과 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_NC_LOW와 같은 4입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropOrderByColumnsInSelect|*사용법*<br /> 읽기 전용 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_ORDERBYCOLUMNSINSELECT와 같습니다.<br /><br /> 이 속성의 기본값은 FALSE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropOutputParameterAvailable|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_OUTPUTPARAMETERAVAILABILITY와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_OA_NOTSUPPORTED와 같은 1입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropPersistentIdType|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_PERSISTENTIDTYPE과 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_PT_NAME과 같은 4입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropPrepareAbortBehavior|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_PREPAREABORTBEHAVIOR와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_CB_DELETE와 같은 1입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropPrepareCommitBehavior|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_PREPARECOMMITBEHAVIOR와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_CB_DELETE와 같은 1입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropProcedureTerm|*사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_PROCEDURETERM과 같습니다.<br /><br /> 이 속성의 기본값은 "계산 멤버"입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropQuotedIdentifierCase|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_QUOTEDIDENTIFIERCASE와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_IC_MIXED와 같은 8입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropSchemaUsage|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_SCHEMAUSAGE와 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropSqlSupport|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_SQLSUPPORT와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_SQL_SUBMINIMUM과 같은 512입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropSubqueries|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_SUBQUERIES와 같습니다.<br /><br /> **참고!** DMX(Data Mining Extensions)는 하위 쿼리를 지원하지만 이 속성은 SQL의 하위 쿼리 지원을 참조합니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropSupportedTxnDdl|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_SUPPORTEDTXNDDL과 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_TC_NONE과 같은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropSupportedTxnIsoLevels|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_SUPPORTEDTXNISOLEVELS와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_TI_READCOMMITTED와 같은 4096입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropSupportedTxnIsoRetain|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_SUPPORTEDTXNISORETAIN과 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_TR_ABORT_NO, DBPROPVAL_TR_COMMIT_NO 및 DBPROPVAL_TR_NONE의 조합과 같은 292입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|DbpropTableTerm|*사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_TABLETERM과 같습니다.<br /><br /> 이 속성의 기본값은 "큐브"입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|Dialect|*사용법*<br /> 읽기/쓰기 `String` 속성(옵션)<br /><br /> *Description*<br /> 다음과 같은 경우 사용되는 언어를 설정합니다.<br /><br /> -언어 공급자가 첫 번째를 사용 하는 시간 공급자가 쿼리를 실행 하려고 합니다.<br />-쿼리 실패의 결과로 반환 되는 실행 오류에 사용 되는 언어입니다.<br /><br /> 대부분의 쿼리에 다른 언어가 아닌 하나의 특정 언어가 사용되는 경우 `Dialect` 속성을 사용할 수 있습니다.<br /><br /> 쿼리 구문은 DMX 및 SQL과 같은 언어와 유사할 수 있습니다. 구문이 유사할 수 있으므로 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 쿼리 구문에서 언어를 유추하지 못할 수 있습니다. 쿼리가 한 언어로 실행되지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스는 다른 언어로 쿼리를 다시 실행하려고 할 수 있습니다.<br /><br /> `Dialect` 속성을 설정하면 공급자가 쿼리를 다른 언어로 다시 실행하려고 하는 경우에도 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 우선 순위가 높은 언어로 쿼리 실행 오류를 반환합니다. 예를 들어 `Dialect` 속성이 MDGUID_DM으로 설정된 경우 공급자는 먼저 쿼리를 데이터 마이닝 쿼리로 실행하려고 하지만 이 쿼리는 실패합니다. 그러면 공급자는 쿼리를 SQL 쿼리로 다시 전송합니다. 그러나 이 SQL 쿼리도 실패합니다. `Dialect` 속성의 값이 MDGUID_DM이므로 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 SQL 오류 메시지가 아닌 데이터 마이닝 오류 메시지를 반환합니다.<br /><br /> `Dialect` 속성을 설정하지 않으면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]는 마지막으로 사용된 언어로 쿼리 실행 오류를 반환합니다. 예를 들어 `Dialect` 속성이 설정되지 않은 경우 데이터 마이닝 쿼리가 실패합니다. 그러면 공급자가 쿼리를 SQL로 다시 전송합니다. SQL 쿼리도 실패합니다. `Dialect` 속성이 설정되지 않았으므로 공급자는 데이터 마이닝 메시지 대신 SQL 오류 메시지를 반환합니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.<br /><br /> 이 속성에 사용 가능한 언어는 다음 표에 나열되어 있습니다.|  
  
|속성|값|Description|  
|----------|-----------|-----------------|  
|DBGUID_SQL|*C8B522D7-5CF3-11CE-ADE5-00AA0044773D*|SQL 파서에 우선 순위가 있습니다.|  
|MDGUID_DM|*62C58FED-CCA5-44F1-83B6-7B45682B3904*|DMX 파서에 우선 순위가 있습니다.|  
|MDGUID_MDX|*A07CCCD0-8148-11D0-87BB-00C04FC33942*|MDX 파서에 우선 순위가 있습니다.|  
  
|속성|요소|  
|----------|-------------|  
|Disable Prefetch Facts|*사용법*<br /> 읽기/쓰기 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> True로 설정하면 엔진에서 더 이상 세션의 길이에 대한 값을 사전 인출하지 않습니다.<br /><br /> 이 속성의 기본값은 `False`합니다.|  
|EffectiveRoles|*사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|EffectiveUserName|*사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 연결할 때 사용자 이름을 재정의하는 데 사용할 계정의 이름을 지정합니다. 속성의 값이 정규화 되지 않으므로, 하는 MDX [UserName](/sql/mdx/username-mdx) 이 속성을 사용 하는 경우 함수는 리터럴 값을 반환 합니다. 이 속성은 서버 관리자만 사용할 수 있습니다.<br /><br /> 이 속성은 다음 SID 유형을 지원: 사용자, 그룹, 별칭, WellKnownGroup, 컴퓨터.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|EndRange|*사용법*<br /> 쓰기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> `CellOrdinal` 특성 값에 해당하는 정수 값(0부터 시작)을 지정합니다. `CellOrdinal` 특성은 `Cell`의 `CellData` 섹션에 있는 `MDDataSet` 요소의 일부입니다.<br /><br /> 클라이언트 응용 프로그램은 `BeginRange` 속성과 함께 이 속성을 사용하여 명령에 의해 반환되는 OLAP 데이터 집합을 셀의 특정 범위로 제한할 수 있습니다. -1을 지정하면 `BeginRange` 속성에 지정된 셀에서 모든 셀이 반환됩니다.<br /><br /> 이 속성의 기본값은-1입니다.<br /><br /> 이 속성은 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|ExecutionMode|*사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 *Execute*합니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|ForceCommitTimeout|*사용법*<br /> 쓰기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이전에 실행된 명령을 강제로 롤백하기 전에 현재 실행 중인 XMLA 명령의 커밋 단계에서 대기하는 시간(초)을 결정합니다. 커밋 단계는 `Statement` 또는 `Process`와 같은 XMLA 명령에 해당합니다.<br /><br /> 영(0) 값은 인스턴스가 무기한 대기함을 나타냅니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|형식|*사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> `Discover` 및 `Execute` 메서드에서 반환되는 결과 집합의 유형을 결정합니다. 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
 이 속성의 기본값은 *네이티브*합니다.  
  
 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|*테이블 형식*|결과 사용 하 여 집합을 반환 합니다 [행 집합](../xml-data-types/rowset-data-type-xmla.md) 데이터 형식입니다.|  
|*다차원*|사용 하 여 행 집합을 반환 합니다 [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) 데이터 형식입니다.|  
|*네이티브*|형식이 명시적으로 지정되지 않습니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 명령에 적합한 형식을 반환합니다. 실제 결과 유형은 결과의 네임스페이스로 식별됩니다.|  
  
|속성|요소|  
|----------|-------------|  
|ImpactAnalysis|*사용법*<br /> 쓰기 전용 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|LocaleIdentifier|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> `Discover` 또는 `Execute` 메서드에 사용되는 LCID(로캘 ID)를 읽거나 설정합니다. 언어 식별자의 전체 16진수 목록을 보려면 MSDN Library에서 "언어 식별자"를 검색하십시오.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MaximumRows|*사용법*<br /> 쓰기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropAggregateCellUpdate|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_AGGREGATECELL_UPDATE와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_AU_SUPPORTED와 같은 4입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropAxes|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_AXES와 같습니다.<br /><br /> 이 속성의 기본값은 2147483647입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropDrillFunctions|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 서버에서 드릴 함수의 지원 수준을 결정합니다. 유효한 비트 마스크를 작성하기 위해 다음 값이 사용됩니다.<br /><br /> MDPROPVAL_MDF_BASIC (0x01)<br /><br /> MDPROPVAL_MDF_ASYMMETRIC (0x02)<br /><br /> MDPROPVAL_MDF_CALC_MEMBERS (0x04)<br /><br /> 기본값은 다음과 같습니다.<br /><br /> SQL Server 2008의 경우 3<br /><br /> SQL Server 2008 R2 및 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]의 경우 7<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropFlatteningSupport|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_FLATTENING_SUPPORT와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_FS_FULL_SUPPORT와 같은 1입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxCaseSupport|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_CASESUPPORT와 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxDescFlags|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_DESCFLAGS와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_MD_BEFORE, MDPROPVAL_MD_AFTER 및 MDPROPVAL_MD_SELF와 같은 7입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxFormulas|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_FORMULAS와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_MF_WITH_CALCMEMBERS, MDPROPVAL_MF_WITH_NAMEDSETS, MDPROPVAL_MF_CREATE_CALCMEMBERS, MDPROPVAL_MF_CREATE_NAMEDSETS, MDPROPVAL_MF_SCOPE_SESSION 및 MDPROPVAL_MF_SCOPE_GLOBAL의 조합과 같은 63입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxJoinCubes|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_JOINCUBES와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_MJC_SINGLECUBE와 같은 1입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxMemberFunctions|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_MEMBER_FUNCTIONS와 같습니다.<br /><br /> 이 속성의 기본값은 사용 가능한 모든 OLE DB 값의 조합과 같은 15입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxNamedSets|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 다음 표에 나열된 값의 비트 마스크입니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*0x01*|MDPROPVAL_MNS_BASIC|  
|*0x02*|MDPROPVAL_MNS_DYNAMIC|  
|*0x04*|MDPROPVAL_MNS_DISPLAYFOLDER|  
|*0x08*|MDPROPVAL_MNS_CAPTION|  
  
 이 속성의 기본값은 값 15입니다.  
  
|속성|요소|  
|----------|-------------|  
|MdpropMdxNonMeasureExpressions|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_NONMEASURE_EXPRESSIONS와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_NME_ALLDIMENSIONS와 같은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxNumericFunctions|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_NUMERIC_FUNCTIONS와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_MNF_MEDIAN, MDPROPVAL_MNF_VAR, MDPROPVAL_MNF_STDDEV, MDPROPVAL_MNF_RANK, MDPROPVAL_MNF_AGGREGATE, MDPROPVAL_MNF_COVARIANCE, MDPROPVAL_MNF_CORRELATION, MDPROPVAL_MNF_LINREGSLOPE, MDPROPVAL_MNF_LINREGVARIANCE, MDPROPVAL_MNF_LINREG2 및 MDPROPVAL_MNF_LINREGPOINT의 조합과 같은 2047입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxObjQualification|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_OBJQUALIFICATION과 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_MOQ_DIM_HIER, MDPROPVAL_MOQ_DIMHIER_LEVEL, MDPROPVAL_MOQ_DIMHIER_MEMBER, MDPROPVAL_MOQ_LEVEL_MEMBER 및 MDPROPVAL_MOQ_MEMBER_MEMBER의 조합과 같은 496입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxOuterReference|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_OUTERREFERENCE와 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxQueryByProperty|*사용법*<br /> 읽기 전용 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_QUERYBYPROPERTY와 같습니다.<br /><br /> 이 속성의 기본값은 TRUE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxRangeRowset|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_RANGEROWSET과 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_RR_UPDATE와 같은 4입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxSetFunctions|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_SET_FUNCTIONS와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_MSF_TOPPERCENT, MDPROPVAL_MSF_BOTTOMPERCENT, MDPROPVAL_MSF_TOPSUM, MDPROPVAL_MSF_BOTTOMSUM, MDPROPVAL_MSF_PERIODSTODATE, MDPROPVAL_MSF_LASTPERIODS, MDPROPVAL_MSF_YTD, MDPROPVAL_MSF_QTD, MDPROPVAL_MSF_MTD, MDPROPVAL_MSF_WTD, MDPROPVAL_MSF_DRILLDOWNMEMBER, MDPROPVAL_MSF_DRILLDOWNLEVEL, MDPROPVAL_MSF_DRILLDOWNMEMBERTOP, MDPROPVAL_MSF_DRILLDOWNMEMBERBOTTOM, MDPROPVAL_MSF_DRILLDOWNLEVEL, MDPROPVAL_MSF_DRILLDOWNLEVELTOP, MDPROPVAL_MSF_DRILLDOWNLEVELBOTTOM, MDPROPVAL_MSF_DRILLUPMEMBER, MDPROPVAL_MSF_DRILLUPLEVEL 및 MDPROPVAL_MSF_TOGGLEDRILLSTATE의 조합과 같은 524287입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxSlicer|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_SLICER와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_MS_SINGLETUPLE과 같은 2입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxStringCompop|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_MDX_STRING_COMPOP과 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_MSC_LESSTHAN, MDPROPVAL_MSC_GREATERTHAN, MDPROPVAL_MSC_LESSTHANEQUAL 및 MDPROPVAL_MSC_GREATERTHANEQUAL의 조합과 같은 15입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdpropMdxSubQueries|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> SQL Server 2014에서 이 속성의 기본값은 값 63입니다.<br /><br /> SQL Server 2008 R2 및 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 이 속성의 기본값은 31입니다.<br /><br /> SQL Server 2008에서 이 속성의 기본값은 값 15입니다.<br /><br /> MDX의 하위 쿼리에 대한 지원 수준을 나타냅니다. 다음 표에 나열된 값의 비트 마스크입니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*0x01*|MDPROPVAL_MSQ_BASIC|  
|*0x02*|MDPROPVAL_MSQ_ARBITRARYSHAPE|  
|*0x04*|MDPROPVAL_MSQ_NONVISUAL|  
|*0x08*|MDPROPVAL_MSQ_CALCMEMBERS|  
  
|||  
|-|-|  
|*0x10*|MDPROPVAL_MSQ_CALCMEMBERS2|  
  
|속성|요소|  
|----------|-------------|  
|MdpropNamedLevels|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_NAMED_LEVELS와 같습니다.<br /><br /> 이 속성의 기본값은 MDPROPVAL_NL_NAMEDLEVELS 및 MDPROPVAL_NL_NUMBEREDLEVELS의 조합과 같은 3입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|MdxMissingMemberMode|*사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> MDX 문에서 누락된 멤버를 무시할 것인지 여부를 나타냅니다.<br /><br /> 이 속성은 OLE DB 속성인 DBPROP_MDX_MISSING_MEMBER_MODE와 같습니다.<br /><br /> 이 속성의 기본값은 *기본*입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.<br /><br /> 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*기본값*|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 의해 생성되는 값을 사용합니다.|  
|*오류*|오류를 발생시킵니다.|  
|*무시*|누락된 멤버를 항상 무시합니다.|  
  
|속성|요소|  
|----------|-------------|  
|MDXSupport|*사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> MDX 지원 수준을 설명하는 열거형을 지정합니다.<br /><br /> `Value` = *Core* 모든 MDX 옵션이 지원 됩니다.<br /><br /> 열거형에 포함 하는 유일한 값은 현재 *Core*합니다. 이후 릴리스에서 이 열거형에 대해 다른 값이 정의될 예정입니다.<br /><br /> 이 속성의 기본값은 *Core*합니다.<br /><br /> 이 속성은 `Discover` 메서드와 함께 사용할 수 있습니다.|  
|NonEmptyThreshold|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|암호|**이 속성은 더 이상 지원 합니다.**<br /><br /> *사용법*<br /> 쓰기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 이전 버전과의 호환성을 위해 이 속성은 `Execute` 또는 `Discover` 메서드와 함께 사용될 경우 오류를 생성하지 않고 무시됩니다.|  
|ProviderName|*사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_DBMSNAME과 같습니다.<br /><br /> 이 속성의 기본값은 "OLAP 서버"입니다.<br /><br /> 이 속성은 `Discover` 메서드와 함께 사용할 수 있습니다.|  
|ProviderType|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_DATASOURCE_TYPE과 같습니다.<br /><br /> 이 속성의 기본값은 6입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|ProviderVersion|*사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_DBMSVER와 같습니다.<br /><br /> 이 속성의 기본값은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 버전입니다.<br /><br /> 이 속성은 `Discover` 메서드와 함께 사용할 수 있습니다.|  
|ReadOnlySession|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|RealTimeOlap|*사용법*<br /> 읽기/쓰기 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> TRUE로 설정하면 테이블 알림을 수신하는 모든 파티션이 캐싱을 무시하고 실시간으로 쿼리됩니다. 이 속성은 OLE DB 속성인 DBPROP_MSMD_REAL_TIME_OLAP과 같습니다.<br /><br /> 이 속성의 기본값은 FALSE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|ReturnCellProperties|*사용법*<br /> 읽기/쓰기 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 이 속성의 기본값은 FALSE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|역할|*사용법*<br /> 읽기/쓰기 `String` 속성(옵션)<br /><br /> *Description*<br /> 클라이언트 응용 프로그램이 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 연결하는 데 사용하는 역할 이름의 쉼표로 구분된 문자열을 지정합니다. 이 속성을 통해 사용자는 현재 사용 중인 역할 이외의 역할을 사용하여 연결할 수 있습니다. 예를 들어 서버 관리자가 역할의 멤버로 큐브에 연결하여 해당 역할에 부여된 사용 권한을 테스트할 수 있습니다. 이 사용자는 이 속성을 사용하여 연결하도록 지정된 역할의 멤버여야 합니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.<br /><br /> **참고!** 역할 이름은 대/소문자를 구분합니다. **사용 하지 않는** 쉼표로 구분 된 역할 이름 사이 공백이 있습니다. 공백을 사용하면 쿼리에서 오류 및 예기치 않은 결과를 보안된 셀 집합으로 반환할 수 있습니다.|  
|SafetyOptions|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 클라이언트 응용 프로그램에서 안전하지 않은 라이브러리를 등록 및 로드할 수 있는지 여부를 결정합니다.<br /><br /> 이 속성의 값은 로컬 큐브에 PASSTHROUGH 키워드가 허용되는지 여부도 결정합니다. 다음과 같은 경우 오류가 발생합니다.<br /><br /> 인 경우 클라이언트 응용 프로그램이 PASSTHROUGH 키워드를 포함 하는 INSERT INTO 문을 사용 하 여 로컬 큐브를 만들려면 하려고 시도 합니다.<br />인 경우 클라이언트 응용 프로그램이 PASSTHROUGH 키워드를 사용 하는 INSERT INTO 문이 있는 로컬 큐브를 업데이트 하려고 시도 합니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.<br /><br /> 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|속성|값|Description|  
|----------|-----------|-----------------|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_DEFAULT|*0*|이 값은 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE로 처리됩니다.<br /><br /> 로컬 큐브에 대한 연결의 경우 이 값은 CREATECUBE 연결 문자열 속성의 사용 여부에 따라 달라집니다. CREATECUBE 연결 문자열 속성이 사용되면 이 값은 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL과 같습니다. 그렇지 않으면 이 값은 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE와 같습니다.|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL|*1.*|이 값은 초기화 및 스크립팅을 수행하기에 안전한지 확인하지 않고 모든 사용자 정의 함수 라이브러리를 활성화합니다. 로컬 큐브에 대한 연결의 경우 이 값은 저장 프로시저와 PASSTHROUGH 키워드(INSERT INTO 문)를 사용할 수 있도록 합니다.<br /><br /> **이 옵션은 좋지 않습니다**합니다.|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_SAFE|*2*|이 값은 특정 사용자 정의 함수 라이브러리의 모든 클래스가 초기화 및 스크립팅을 수행하기에 안전한지 확인되도록 합니다. 로컬 큐브에 대한 연결의 경우 이 값은 PermissionSet 속성이 안전으로 설정되지 않은 저장 프로시저와 PASSTHROUGH 키워드(INSERT INTO 문)를 사용하지 못하도록 합니다.<br /><br /> 이 값의 동작도 제거 합니다 [MDSCHEMA_ACTIONS](../../schema-rowsets/ole-db-olap/mdschema-actions-rowset.md) 명령 또는 HTML의 값은 ACTION_TYPE 열에 있거나 ACTION_TYPE 열에 url 값과 값 하지 않는 CONTENT 열에는 스키마 행 집합 "http://" 또는 "https://"로 시작 합니다.|  
|DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_NONE|*3*|이 값은 세션 중 사용자 정의 함수가 사용되지 않도록 합니다. 로컬 큐브에 대한 연결의 경우 이 값은 모든 저장 프로시저와 PASSTHROUGH 키워드(INSERT INTO 문)를 사용하지 못하도록 합니다.<br /><br /> 이 값은 MDSCHEMA_ACTIONS 스키마 행 집합의 모든 동작도 제거합니다.|  
  
|속성|요소|  
|----------|-------------|  
|SecuredCellValue|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 보안된 셀에 액세스하려고 할 때 반환할 `Value` 및 `Formatted Value` 셀 속성에 대한 오류 코드와 값을 지정합니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.<br /><br /> 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*0*|(기본값) 이전 버전과 호환성을이 값은 동일 *1*합니다. 이 기본값의 의미는 이후 버전에서 변경될 수 있습니다.|  
|*1.*|반환: HRESULT 반환 합니다<br /><br /> 셀의 `Value` 속성은 결과를 Variant 데이터 형식으로 포함합니다. 문자열 "#N/A"가 `Formatted Value` 속성에 반환됩니다.|  
|*2*|오류를 HRESULT의 값으로 반환합니다.|  
|*3*|`Value` 및 `Formatted Value` 속성 모두에 NULL을 반환합니다.|  
|*4*|`Value` 속성에 숫자 영(0)을 반환하고 `Formatted Value` 속성에 서식이 지정된 0을 반환합니다. 예를 들어 `Formatted Value` 속성이 "#.##"인 셀에 대해 `Format` 속성에는 0.00이 반환됩니다.|  
|*5*|`Value` 및 `Formatted Value` 속성 모두에 문자열 "#SEC"를 반환합니다.|  
  
|속성|요소|  
|----------|-------------|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|*사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 DBPROP_SERVERNAME과 같습니다.<br /><br /> 이 속성의 기본값은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 이름입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|ShowHiddenCubes|*사용법*<br /> 읽기/쓰기 `Boolean` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 FALSE입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|SQLQueryMode|*사용법*<br /> 읽기/쓰기 `String` 속성(옵션)<br /><br /> *Description*<br /> SQL 쿼리에 계산이 포함되는지 여부를 결정합니다.<br /><br /> 이 속성의 기본값은 *계산*합니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.<br /><br /> 이 속성은 다음 표에 나열된 값일 수 있습니다.|  
  
|값|Description|  
|-----------|-----------------|  
|*데이터*|계산이 포함되지 않습니다.|  
|*계산*|계산이 반환됩니다.|  
|*IncludeEmpty*|계산 및 빈 행이 반환됩니다.|  
  
|속성|요소|  
|----------|-------------|  
|SQLSupport|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성의 기본값은 512입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|SspropInitAppName|*사용법*<br /> 읽기/쓰기 `String` 속성(옵션)<br /><br /> *Description*<br /> 클라이언트 응용 프로그램의 이름을 포함합니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|SspropInitPacketsize|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 클라이언트 응용 프로그램의 ID를 포함합니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|SspropInitWsid|*사용법*<br /> 읽기/쓰기 `String` 속성(옵션)<br /><br /> *Description*<br /> 클라이언트 워크스테이션의 ID를 포함합니다.<br /><br /> 이 속성의 기본값은 없습니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|StateSupport|*사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> 상태 저장에 대한 지원 수준을 지정합니다.<br /><br /> *없음* = <br />                        상태 저장이 지원되지 않습니다.<br /><br /> *세션* = 상태 저장 세션 지원을 통해 제공 됩니다.<br /><br /> 상태 저장 및 세션 지원에 대 한 자세한 내용은 참조 하세요. [관리 연결 및 세션 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)합니다.<br /><br /> 이 속성의 기본값은 *세션*합니다.<br /><br /> 이 속성은 `Discover` 메서드와 함께 사용할 수 있습니다.|  
|Timeout|*사용법*<br /> 읽기/쓰기 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 오류를 반환하기 전에 요청이 성공할 때까지 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 대기해야 하는 최대 시간(초)을 지정합니다. 이 속성은 오류를 반환하기 전에 쓰기 저장(writeback) 테이블에 대한 업데이트가 성공할 때까지 인스턴스가 대기해야 하는 최대 시간도 결정합니다. 이 시간은 연결 문자열 속성인 Writeback Timeout과 같습니다.<br /><br /> 이 속성의 기본값은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|TransactionDDL|*사용법*<br /> 읽기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 나중에 사용하도록 예약되어 있습니다.<br /><br /> 이 속성의 기본값은 0입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|UserName|이 속성은 더 이상 지원되지 않습니다.<br /><br /> *사용법*<br /> 읽기 전용 `String` 속성(옵션)<br /><br /> *Description*<br /> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스가 명령과 연결하는 사용자 이름을 반환하는 문자열을 지정합니다. 이전 버전과의 호환성을 위해 이 속성은 `Execute` 또는 `Discover` 메서드와 함께 사용될 경우 오류를 생성하지 않고 무시됩니다. 이 속성은 OLE DB 속성인 DBPROP_USERNAME과 같습니다.<br /><br /> 이 속성의 기본값은 현재 세션 또는 연결을 연 사용자 이름입니다.<br /><br /> 이 속성은 `Execute` 메서드와 함께 사용할 수 있습니다.|  
|VisualMode|*사용법*<br /> 쓰기 전용 `Integer` 속성(옵션)<br /><br /> *Description*<br /> 이 속성은 OLE DB 속성인 MDPROP_VISUALMODE와 같습니다.<br /><br /> 이 속성의 기본값은 DBPROPVAL_VISUAL_MODE_DEFAULT와 같은 영(0)입니다.<br /><br /> 이 속성은 `Discover` 및 `Execute` 메서드와 함께 사용할 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [PropertyList 요소 &#40;XMLA&#41;](propertylist-element-xmla.md)  
  
  
