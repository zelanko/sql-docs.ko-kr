---
title: XML 데이터 형식 사용 | Microsoft Docs
description: OLE DB Driver for SQL Server에서 XML 데이터 형식 사용
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [OLE DB Driver for SQL Server], xml data type
- OLE DB Driver for SQL Server schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- MSOLEDBSQL, XML
- xml data type [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- OLE DB Driver for SQL Server OLE DB interfaces
- XML [SQL Server], OLE DB Driver for SQL Server
- COLUMNS rowset
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 8b6c129aa03fd887f0483f15bdb831e2d41b347f
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006806"
---
# <a name="using-xml-data-types"></a>XML 데이터 형식 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에는 XML 문서와 조각을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 저장할 수 있는 **xml** 데이터 형식이 도입되었습니다. **xml** 데이터 형식은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 기본 제공 데이터 형식이며 **int** 및 **varchar**와 같은 다른 기본 제공 형식과 비슷합니다. 다른 기본 제공 형식과 마찬가지로 **xml** 데이터 형식도 변수 유형, 매개 변수 유형, 함수 반환 유형 또는 테이블을 만드는 경우 열 유형으로 사용하거나 CAST 및 CONVERT 함수에 사용할 수 있습니다.  
  
## <a name="programming-considerations"></a>프로그래밍 고려 사항  
 XML은 원하는 경우 문서의 인코딩을 지정하는 XML 헤더를 포함할 수 있다는 점에서 자체 설명적 데이터 형식이라고 할 수 있습니다. 예를 들면 다음과 같습니다.  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 XML 표준은 XML 프로세서가 문서의 처음 몇 바이트를 검사하여 문서에 사용된 인코딩을 검색하는 방법을 설명합니다. 애플리케이션에서 지정한 인코딩이 문서에 지정된 인코딩과 충돌하는 경우가 있을 수 있습니다. 바인딩된 매개 변수로 전달된 문서의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 XML을 이진 데이터로 처리하므로 변환이 수행되지 않으며 XML 파서는 문서 내에 지정된 인코딩을 아무런 문제없이 사용할 수 있습니다. 그러나 WSTR로 바인딩된 XML 데이터의 경우 문서가 유니코드로 인코딩되도록 애플리케이션에서 관련 작업을 수행해야 합니다. 이 시나리오에서는 문서를 DOM으로 로드하고 인코딩을 유니코드로 변경한 다음, 문서를 직렬화해야 할 수 있습니다. 이 단계를 수행하지 않으면 데이터 변환이 일어날 수 있으며 그 결과 XML이 잘못되거나 손상될 수 있습니다.  
  
 XML이 리터럴로 지정된 경우에도 충돌이 발생할 가능성이 있습니다. 예를 들어 다음은 잘못된 XML 지정입니다.  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server용 OLE DB 드라이버 
 DBTYPE_XML은 OLE DB Driver for SQL Server에서 XML에 관련된 새로운 데이터 형식입니다. DBTYPE_BYTES, DBTYPE_WSTR, DBTYPE_BSTR, DBTYPE_XML, DBTYPE_STR, DBTYPE_VARIANT, DBTYPE_IUNKNOWN 등 기존의 OLE DB 형식을 통해서도 XML 데이터에 액세스할 수 있습니다. XML 형식 열에 저장된 데이터는 SQL Server용 OLE DB 드라이버 행 집합에 있는 다음 형식의 열에서 검색할 수 있습니다.  
  
-   텍스트 문자열  
  
-   **ISequentialStream**  
  
> [!NOTE]  
>  SQL Server용 OLE DB 드라이버에 SAX 판독기가 포함되어 있지는 않지만 MSXML에서 **ISequentialStream**을 SAX 및 DOM 개체로 쉽게 전달할 수 있습니다.  
  
 **ISequentialStream**은 큰 XML 문서의 검색에 사용합니다. 다른 큰 값 유형에 사용되는 방법이 XML에도 적용됩니다. 자세한 내용은 [큰 값 형식 사용](../../oledb/features/using-large-value-types.md)을 참조하세요.  
  
 행 집합의 XML 형식 열에 저장된 데이터는 **IRow::GetColumns**, **IRowChange::SetColumns** 및 **ICommand::Execute** 같은 일반 인터페이스를 통해 애플리케이션에 의해서도 검색, 삽입 또는 업데이트될 수 있습니다. 검색의 경우와 마찬가지로 애플리케이션에서 텍스트 문자열 또는 **ISequentialStream**을 SQL Server용 OLE DB 드라이버에 전달할 수 있습니다.  
  
> [!NOTE]  
>  문자열 형식의 XML 데이터를 **ISequentialStream** 인터페이스를 통해 보내려면 바인딩에서 DBTYPE_IUNKNOWN을 지정하고 해당 *pObject* 인수를 null로 설정하여 **ISequentialStream**을 가져와야 합니다.  
  
 소비자 버퍼가 너무 작아 검색된 XML 데이터가 잘린 경우 길이가 알 수 없는 길이를 나타내는 0xffffffff로 반환될 수 있습니다. 이 동작은 실제 데이터를 보내기 전에 길이 정보를 보내지 않고 클라이언트로 스트리밍되는 데이터 형식으로 구현하는 것과 같습니다. 일부 경우 공급자가 **IRowset::GetData**와 같은 전체 값을 버퍼링하고 데이터 변환이 수행되면 실제 길이가 반환될 수 있습니다.  
  
 SQL Server로 전송된 XML 데이터는 서버에서 이진 데이터로 처리됩니다. 이 동작은 어떠한 변환도 일어나지 않으며 XML 파서는 XML 인코딩을 자동 검색할 수 있습니다. 이를 통해 보다 광범위한 XML 문서(예: UTF-8로 인코딩된 문서)를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 입력으로 사용할 수 있습니다.  
  
 입력 XML이 DBTYPE_WSTR로 바인딩된 경우 애플리케이션에서는 XML이 이미 유니코드로 인코딩되었는지 확인하여 원치 않는 데이터 변환으로 인해 데이터가 손상되는 것을 방지해야 합니다.  
  
### <a name="data-bindings-and-coercions"></a>데이터 바인딩 및 강제 변환  
 다음 표에서는 표에 나열된 데이터 형식을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **xml** 데이터 형식과 함께 사용할 때 발생하는 바인딩 및 강제 변환에 대해 설명합니다.  
  
|데이터 형식|SQL Server의<br /><br /> **XML**|SQL Server의<br /><br /> **비XML**|SQL Server의<br /><br /> **XML**|SQL Server의<br /><br /> **비XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|통과<sup>6,7</sup>|오류<sup>1</sup>|확인<sup>11, 6</sup>|오류<sup>8</sup>|  
|DBTYPE_BYTES|통과<sup>6,7</sup>|해당 없음<sup>2</sup>|확인<sup>11, 6</sup>|해당 없음<sup>2</sup>|  
|DBTYPE_WSTR|통과<sup>6,10</sup>|해당 없음<sup>2</sup>|OK<sup>4, 6, 12</sup>|해당 없음<sup>2</sup>|  
|DBTYPE_BSTR|통과<sup>6,10</sup>|해당 없음<sup>2</sup>|확인<sup>3</sup>|해당 없음<sup>2</sup>|  
|DBTYPE_STR|확인<sup>6, 9, 10</sup>|해당 없음<sup>2</sup>|확인<sup>5, 6, 12</sup>|해당 없음<sup>2</sup>|  
|DBTYPE_IUNKNOWN|**ISequentialStream**을 통한 바이트 스트림<sup>7</sup>|해당 없음<sup>2</sup>|**ISequentialStream**을 통한 바이트 스트림<sup>11</sup>|해당 없음<sup>2</sup>|  
|DBTYPE_VARIANT(VT_UI1 &#124; VT_ARRAY)|통과<sup>6,7</sup>|해당 없음<sup>2</sup>|해당 없음|해당 없음<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|통과<sup>6,10</sup>|해당 없음<sup>2</sup>|확인<sup>3</sup>|해당 없음<sup>2</sup>|  
  
 <sup>1</sup>DBTYPE_XML 이외의 서버 유형이 **ICommandWithParameters::SetParameterInfo**에 지정되었고 접근자 유형이 DBTYPE_XML이면 문이 실행될 때 오류가 발생합니다(DB_E_ERRORSOCCURRED, 매개 변수 상태는 DBSTATUS_E_BADACCESSOR임). 그렇지 않은 경우에는 데이터가 서버로 전송되지만 XML에서 매개 변수 데이터 형식으로의 암시적 변환이 이루어지지 않았음을 나타내는 오류가 반환됩니다.  
  
 <sup>2</sup>이 문서에서는 다루지 않습니다.  
  
 <sup>3</sup>형식이 UTF-16이고 BOM(바이트 순서 표시), 인코딩 사양 및 null 종결을 포함하지 않습니다.  
  
 <sup>4</sup>형식이 UTF-16이고 BOM, 인코딩 사양을 포함하지 않지만 null 종결은 포함합니다.  
  
 <sup>5</sup>형식이 클라이언트 코드 페이지로 인코딩된 멀티바이트 문자이고 null 종결자를 포함합니다. 서버에서 제공하는 유니코드에서 변환되면 데이터가 손상될 수 있으므로 이 바인딩은 사용하지 않는 것이 좋습니다.  
  
 <sup>6</sup>BY_REF가 사용될 수 있습니다.  
  
 <sup>7</sup>UTF-16 데이터는 BOM으로 시작해야 합니다. 그렇지 않으면 서버에서 인코딩을 올바르게 인식할 수 없습니다.  
  
 <sup>8</sup>접근자 생성 시간 또는 인출 시간에 유효성 검사가 수행될 수 있습니다. 오류는 DB_E_ERRORSOCCURRED이고 바인딩 상태는 DBBINDSTATUS_UNSUPPORTEDCONVERSION으로 설정됩니다.  
  
 <sup>9</sup>데이터가 서버로 전송되기 전에 클라이언트 코드 페이지를 사용하여 유니코드로 변환됩니다. 문서 인코딩이 클라이언트 코드 페이지와 일치하지 않으면 데이터가 손상될 수 있으므로 이 바인딩은 사용하지 않는 것이 좋습니다.  
  
 <sup>10</sup>서버로 전송된 데이터에 항상 BOM이 추가됩니다. 데이터의 시작 부분에 이미 BOM이 있는 경우 버퍼 시작 부분에 두 개의 BOM이 오게 됩니다. 서버에서는 첫 번째 BOM을 통해 인코딩을 UTF-16으로 인식한 다음 이 BOM을 삭제합니다. 두 번째 BOM은 너비가 0인 줄 바꿈하지 않는 공백 문자로 해석됩니다.  
  
 <sup>11</sup>형식이 UTF-16이고 인코딩 사양을 포함하지 않으며 서버에서 받은 데이터에 BOM이 추가됩니다. 서버에서 빈 문자열을 반환하더라도 BOM이 애플리케이션에 반환됩니다. 버퍼 길이가 홀수 바이트이면 데이터가 올바르게 잘립니다. 전체 값이 청크로 반환되면 연결해서 올바른 값으로 다시 구성할 수 있습니다.  
  
 <sup>12</sup>버퍼 길이가 2자 미만이면, 즉 null 종결을 포함할 공간이 충분하지 않으면 오버플로 오류가 보고됩니다.  
  
> [!NOTE]  
>  NULL XML 값에 대해서는 데이터가 반환되지 않습니다.  
  
 XML 표준을 따르려면 UTF-16로 인코딩된 XML이 BOM(바이트 순서 표시), 즉 UTF-16 문자 코드 0xFEFF로 시작해야 합니다. WSTR 및 BSTR 바인딩을 사용하는 경우 인코딩이 바인딩에서 암시적으로 지정되므로 SQL Server용 OLE DB 드라이버가 BOM을 요구하거나 BOM을 추가하지 않습니다. BYTES, XML 또는 IUNKNOWN 바인딩을 사용하는 경우 BOM을 추가하는 목적은 다른 XML 프로세서 및 스토리지 시스템을 간편하게 다룰 수 있도록 하는 데 있습니다. 이 경우 UTF-16으로 인코딩된 XML에 BOM을 제공해야 합니다. SQL Server를 비롯한 대부분의 XML 프로세서는 값의 처음 몇 바이트를 검사하여 인코딩을 추론하기 때문에 애플리케이션에서는 실제 인코딩을 확인할 필요가 없습니다. BYTES, XML 또는 IUNKNOWN 바인딩을 사용하여 SQL Server용 OLE DB 드라이버에서 받은 XML 데이터는 항상 UTF-16으로 인코딩되고 BOM을 포함하며 인코딩 선언을 포함하지 않습니다.  
  
 OLE DB 핵심 서비스에서 제공하는 데이터 변환(**IDataConvert**)은 DBTYPE_XML에 적용되지 않습니다.  
  
 데이터가 서버로 전송되면 유효성 검사가 수행됩니다. 클라이언트 쪽 유효성 검사 및 인코딩 변경 내용은 애플리케이션에서 처리해야 합니다. XML 데이터를 직접 처리하지 말고 DOM 또는 SAX 판독기를 사용하여 처리하는 것이 좋습니다.  
  
 DBTYPE_NULL 및 DBTYPE_EMPTY는 입력 매개 변수에 대해서는 바인딩할 수 있지만 출력 매개 변수나 결과에 대해서는 바인딩할 수 없습니다. 입력 매개 변수에 대해 바인딩할 경우 상태를 DBSTATUS_S_ISNULL 또는 DBSTATUS_S_DEFAULT로 설정해야 합니다.  
  
 DBTYPE_XML은 DBTYPE_EMPTY와 DBTYPE_NULL로 변환할 수 있습니다. DBTYPE_EMPTY는 DBTYPE_XML로 변환할 수 있지만 DBTYPE_NULL은 DBTYPE_XML로 변환할 수 없습니다. 이는 DBTYPE_WSTR와 일치합니다.  
  
 앞의 표에서 볼 수 있듯이 DBTYPE_IUNKNOWN은 지원되는 바인딩이지만 DBTYPE_XML과 DBTYPE_IUNKNOWN 간에는 변환이 수행되지 않습니다. DBTYPE_IUNKNOWN을 DBTYPE_BYREF와는 사용할 수 없습니다.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 행 집합의 추가 내용 및 변경 내용  
 OLE DB Driver for SQL Server는 많은 핵심 OLE DB 스키마 행 집합에 새로운 값 또는 변경 내용을 추가합니다.  
  
#### <a name="the-columns-and-procedure_parameters-schema-rowsets"></a>COLUMNS 및 PROCEDURE_PARAMETERS 스키마 행 집합  
 COLUMNS 및 PROCEDURE_PARAMETERS 스키마 행 집합에 추가된 열은 다음과 같습니다.  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 스키마 컬렉션이 정의된 카탈로그의 이름입니다. 비XML 열 또는 형식화되지 않은 XML 열에 대해서는 NULL입니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 스키마 컬렉션이 정의된 스키마의 이름입니다. 비XML 열 또는 형식화되지 않은 XML 열에 대해서는 NULL입니다.|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML 스키마 컬렉션의 이름입니다. 비XML 열 또는 형식화되지 않은 XML 열에 대해서는 NULL입니다.|  
  
#### <a name="the-provider_types-schema-rowset"></a>PROVIDER_TYPES 스키마 행 집합  
 PROVIDER_TYPES 스키마 행 집합에서는 **xml** 데이터 형식에 대한 COLUMN_SIZE 값이 0이고 DATA_TYPE이 DBTYPE_XML입니다.  
  
#### <a name="the-ss_xmlschema-schema-rowset"></a>SS_XMLSCHEMA 스키마 행 집합  
 새로운 스키마 행 집합인 SS_XMLSCHEMA는 클라이언트가 XML 스키마 정보를 검색할 수 있도록 도입되었습니다. SS_XMLSCHEMA 행 집합에는 다음 열이 포함됩니다.  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 컬렉션이 속한 카탈로그입니다.|  
|SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 컬렉션이 속한 스키마입니다.|  
|SCHEMACOLLECTIONNAME|DBTYPE_WSTR|형식화된 XML 열에 대해서는 XML 스키마 컬렉션의 이름이고, 그렇지 않으면 NULL입니다.|  
|TARGETNAMESPACEURI|DBTYPE_WSTR|XML 스키마의 대상 네임스페이스입니다.|  
|SCHEMACONTENT|DBTYPE_WSTR|XML 스키마 콘텐츠입니다.|  
  
 각 XML 스키마는 카탈로그 이름, 스키마 이름, 스키마 컬렉션 이름 및 대상 네임스페이스 URI(Uniform Resource Identifier)로 범위가 결정됩니다. 또한 이름이 DBSCHEMA_XML_COLLECTIONS인 새 GUID도 정의되었습니다. SS_XMLSCHEMA 스키마 행 집합에 대한 제한 수 및 제한된 열은 다음과 같이 정의되어 있습니다.  
  
|GUID|제한 수|제한된 열|  
|----------|----------------------------|------------------------|  
|DBSCHEMA_XML_COLLECTIONS|4|SCHEMACOLLECTION_CATALOGNAME<br /><br /> SCHEMACOLLECTION_SCHEMANAME<br /><br /> SCHEMACOLLECTIONNAME<br /><br /> TARGETNAMESPACEURI|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>OLE DB 속성 집합의 추가 내용 및 변경 내용  
 OLE DB Driver for SQL Server는 여러 핵심 OLE DB 속성 집합에 새 값 또는 변경 사항을 추가합니다.  
  
#### <a name="the-dbpropset_sqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 속성 집합  
 OLE DB를 통해 **xml** 데이터 형식을 지원하기 위해 SQL Server용 OLE DB 드라이버는 다음 값이 포함된 새로운 DBPROPSET_SQLSERVERPARAMETER 속성 집합을 구현합니다.  
  
|속성|Type|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 스키마 컬렉션이 정의된 카탈로그(데이터베이스)의 이름입니다. SQL의 세 부분으로 구성된 이름 식별자의 일부입니다.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|스키마 컬렉션 내 XML 스키마의 이름입니다. SQL의 세 부분으로 구성된 이름 식별자의 일부입니다.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|카탈로그 내 XML 스키마 컬렉션의 이름입니다. SQL의 세 부분으로 구성된 이름 식별자의 일부입니다.|  
  
#### <a name="the-dbpropset_sqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 속성 집합  
 **ITableDefinition** 인터페이스를 통한 테이블 생성을 지원하기 위해 SQL Server용 OLE DB 드라이버는 DBPROPSET_SQLSERVERCOLUMN 속성 집합에 세 개의 새로운 열을 추가합니다.  
  
|속성|Type|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|형식화된 XML 열에 대해서는 이 속성이 XML 스키마가 저장된 카탈로그의 이름을 지정하는 문자열입니다. 다른 열 유형에 대해서는 이 속성이 빈 문자열을 반환합니다.|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|형식화된 XML 열에 대해서는 이 속성이 이 열을 정의하는 XML 스키마의 이름을 지정하는 문자열입니다.|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|형식화된 XML 열에 대해서는 이 속성이 값을 정의하는 XML 스키마 컬렉션의 이름을 지정하는 문자열입니다.|  
  
 SSPROP_PARAM 값과 마찬가지로 이러한 속성은 모두 옵션이며 기본적으로 비어 있습니다. SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME 및 SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME은 SSPROP_COL_XML_SCHEMACOLLECTIONNAME이 지정된 경우에만 지정할 수 있습니다. XML을 서버에 전달할 때 이러한 값이 포함되어 있으면 현재 데이터베이스에 대해 이들 속성의 존재 여부(유효성)가 확인되고 인스턴스 데이터가 스키마에 대해 검사됩니다. 어떤 경우든 이러한 속성은 모두 비어 있거나 모두 채워져 있어야 올바른 상태입니다.  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 인터페이스의 추가 내용 및 변경 내용  
 OLE DB Driver for SQL Server는 여러 핵심 OLE DB 인터페이스에 새 값 또는 변경 사항을 추가합니다.  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 인터페이스  
 OLE DB를 통해 **xml** 데이터 형식을 지원하기 위해 SQL Server용 OLE DB 드라이버는 [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) 인터페이스의 추가를 비롯하여 많은 변경을 구현합니다. 이 새 인터페이스는 핵심 OLE DB 인터페이스인 **ICommandWithParameters**에서 상속됩니다. **ICommandWithParameters**에서 상속되는 세 개의 메서드인 **GetParameterInfo**, **MapParameterNames** 및 **SetParameterInfo** 외에도 **ISSCommandWithParameters**는 서버별 데이터 형식을 처리하는 데 사용되는 [GetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) 및 [SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 메서드를 제공합니다.  
  
> [!NOTE]  
>  또한 **ISSCommandWithParameters** 인터페이스는 새로운 SSPARAMPROPS 구조를 사용합니다.  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 인터페이스  
 SQL Server용 OLE DB 드라이버는 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 열을 **IColumnRowset::GetColumnsRowset** 메서드에서 반환되는 행 집합에 추가합니다. 이러한 열에는 XML 스키마 컬렉션의 세 부분으로 구성된 이름이 포함됩니다. 비XML 열이나 형식화되지 않은 XML 열에 대해서는 이 세 열 모두 기본값인 NULL을 사용합니다.  
  
|열 이름|Type|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 스키마 컬렉션이 속한 카탈로그입니다.<br /><br /> 그렇지 않으면 NULL입니다.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 스키마 컬렉션이 속한 스키마입니다. 그렇지 않으면 NULL입니다.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|형식화된 XML 열에 대해서는 XML 스키마 컬렉션의 이름이고, 그렇지 않으면 NULL입니다.|  
  
#### <a name="the-irowset-interface"></a>IRowset 인터페이스  
 XML 열의 XML 인스턴스는 **IRowset::GetData** 메서드를 통해 검색됩니다. 클라이언트에서 지정한 바인딩에 따라 XML 인스턴스가 DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML, DBTYPE_STR, DBTYPE_BYTES로 검색되거나 DBTYPE_IUNKNOWN을 통해 인터페이스로 검색될 수 있습니다. 소비자가 DBTYPE_BSTR, DBTYPE_WSTR 또는 DBTYPE_VARIANT를 지정하면 공급자는 XML 인스턴스를 사용자가 요청한 형식으로 변환한 후 해당 바인딩에 지정된 위치에 가져다 놓습니다.  
  
 소비자가 DBTYPE_IUNKNOWN을 지정하고 *pObject* 인수를 NULL로 설정하거나 *pObject* 인수를 IID_ISequentialStream으로 설정하면 소비자가 열에서 XML 데이터를 스트리밍할 수 있도록 공급자가 **ISequentialStream** 인터페이스를 소비자에게 반환합니다. 그러면 **ISequentialStream**이 XML 데이터를 유니코드 문자 스트림으로 반환합니다.  
  
 DBTYPE_IUNKNOWN에 바인딩된 XML 값을 반환할 때 공급자는 `sizeof (IUnknown *)`의 크기 값을 보고합니다. 이 동작은 열이 DBTYPE_IUnknown 또는 DBTYPE_IDISPATCH로 바인딩되어 있는데 정확한 열 크기를 확인할 수 없는 경우 DBTYPE_IUNKNOWN/ISequentialStream이 취하는 방법과 같습니다.  
  
#### <a name="the-irowsetchange-interface"></a>IRowsetChange 인터페이스  
 소비자는 두 가지 방법으로 열의 XML 인스턴스를 업데이트할 수 있습니다. 하나는 공급자가 만든 스토리지 개체 **ISequentialStream**을 사용하는 것입니다. 소비자는 **ISequentialStream::Write** 메서드를 호출하여 공급자가 반환한 XML 인스턴스를 직접 업데이트할 수 있습니다.  
  
 다른 하나는 **IRowsetChange::SetData** 또는 **IRowsetChange::InsertRow** 메서드를 사용하는 것입니다. 이 방법을 사용할 경우 소비자 버퍼의 XML 인스턴스를 DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML 또는 DBTYPE_IUNKNOWN 유형의 바인딩에 지정할 수 있습니다.  
  
 DBTYPE_BSTR, DBTYPE_WSTR 또는 DBTYPE_VARIANT가 지정되는 경우 공급자가 소비자 버퍼의 XML 인스턴스를 적절한 열에 저장합니다.  
  
 DBTYPE_IUNKNOWN/ISequentialStream을 지정하면 소비자가 스토리지 개체를 지정하지 않은 경우에는 소비자가 미리 **ISequentialStream** 개체를 만들어 XML 문서를 개체에 바인딩한 다음, **IRowsetChange::SetData** 메서드를 통해 개체를 공급자에 전달해야 합니다. 소비자는 스토리지 개체를 만들고 pObject 인수를 IID_ISequentialStream으로 설정하고 **ISequentialStream** 개체를 만든 다음, 이 **ISequentialStream** 개체를 **IRowsetChange::SetData** 메서드에 전달할 수도 있습니다. 두 경우 모두 공급자는 **ISequentialStream** 개체를 통해 XML 개체를 검색하여 적절한 열에 삽입할 수 있습니다.  
  
#### <a name="the-irowsetupdate-interface"></a>IRowsetUpdate 인터페이스  
 **IRowsetUpdate** 인터페이스는 지연된 업데이트에 사용할 수 있는 기능을 제공합니다. 소비자가 **IRowsetUpdate::Update** 메서드를 호출할 때까지 행 집합에서 사용할 수 있는 데이터를 다른 트랜잭션에서 사용할 수 없습니다.  
  
#### <a name="the-irowsetfind-interface"></a>IRowsetFind 인터페이스  
 **IRowsetFind::FindNextRow** 메서드는 **xml** 데이터 형식에 사용할 수 없습니다. *hAccessor* 인수에 DBTYPE_XML 열이 지정되어 **IRowsetFind::FindNextRow**가 호출되면 DB_E_BADBINDINFO가 반환되며 이는 검색하는 열의 유형에 관계없이 발생합니다. 이외 다른 바인딩 유형의 경우 검색하는 열이 **xml** 데이터 형식이면 **FindNextRow**가 실패하며 DB_E_BADCOMPAREOP가 반환됩니다.  
 
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
