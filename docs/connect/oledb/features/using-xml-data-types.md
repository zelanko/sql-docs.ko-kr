---
title: XML 데이터 형식을 사용 하 여 | Microsoft Docs
description: SQL Server에 대 한 OLE DB 드라이버와 XML 데이터 형식 사용
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d6ec0009a986e2abd56ac00c1e01826f3ed001f7
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612178"
---
# <a name="using-xml-data-types"></a>XML 데이터 형식 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 도입 된 **xml** 에 조각의 없고 XML 문서를 저장 하는 데 사용할 수 있는 데이터 형식을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스입니다. **xml** 데이터의 기본 제공 데이터 형식이 며 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 같은 몇 가지 다른 기본 제공 유형과 비슷합니다는 **int** 및 **varchar**합니다. 다른 기본 제공 형식과 함께 사용할 수 있는 **xml** 데이터 테이블을 만들 때 열 유형으로; 변수 유형, 매개 변수 형식 또는 함수 반환 유형; 또는 CAST 및 CONVERT 함수를 입력 합니다.  
  
## <a name="programming-considerations"></a>프로그래밍 고려 사항  
 XML은 원하는 경우 문서의 인코딩을 지정하는 XML 헤더를 포함할 수 있다는 점에서 자체 설명적 데이터 형식이라고 할 수 있습니다. 예를 들면 다음과 같습니다.  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 XML 표준은 XML 프로세서가 문서의 처음 몇 바이트를 검사하여 문서에 사용된 인코딩을 검색하는 방법을 설명합니다. 응용 프로그램에서 지정한 인코딩이 문서에 지정된 인코딩과 충돌하는 경우가 있을 수 있습니다. 바인딩된 매개 변수로 전달된 문서의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 XML을 이진 데이터로 처리하므로 변환이 수행되지 않으며 XML 파서는 문서 내에 지정된 인코딩을 아무런 문제없이 사용할 수 있습니다. 그러나 WSTR로 바인딩된 XML 데이터의 경우 문서가 유니코드로 인코딩되도록 응용 프로그램에서 관련 작업을 수행해야 합니다. 이 시나리오는 문서를 DOM에 로드 하 고 유니코드로 인코딩 변경 다음 문서를 직렬화 해야 할 수도 있습니다. 이 단계는 수행 하지, 데이터 변환이 발생할 수 있습니다, 결과 xml이 잘못 되었거나 손상 되었습니다.  
  
 XML이 리터럴로 지정된 경우에도 충돌이 발생할 가능성이 있습니다. 예를 들어 다음은 잘못된 XML 지정입니다.  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 
 DBTYPE_XML은 새 데이터 형식을 OLE DB 드라이버에서 SQL Server에 대 한 XML에 특정 합니다. DBTYPE_BYTES, DBTYPE_WSTR, DBTYPE_BSTR, DBTYPE_XML, DBTYPE_STR, DBTYPE_VARIANT, DBTYPE_IUNKNOWN 등 기존의 OLE DB 형식을 통해서도 XML 데이터에 액세스할 수 있습니다. OLE DB 드라이버는 다음 형식으로 SQL Server 행 집합의 열에서 XML 형식의 열에 저장 된 데이터를 검색할 수 있습니다.  
  
-   텍스트 문자열  
  
-   **ISequentialStream**  
  
> [!NOTE]  
>  OLE DB Driver for SQL Server SAX 판독기에 포함 되지 않습니다 되지만 **ISequentialStream** MSXML에서 SAX 및 DOM 개체로 쉽게 전달할 수 있습니다.  
  
 **ISequentialStream** 큰 XML 문서의 검색에 사용 해야 합니다. 다른 큰 값 유형에 사용되는 방법이 XML에도 적용됩니다. 자세한 내용은 참조 [큰 값 형식을 사용 하 여](../../oledb/features/using-large-value-types.md)합니다.  
  
 행 집합의 XML을 검색할 수도 있습니다를 형식의 열에 저장 된 데이터를 삽입 또는 같은 일반 인터페이스를 통해 응용 프로그램에 의해 업데이트 **irow:: Getcolumns**, **irowchange:: Setcolumns**, 및 **icommand:: Execute**합니다. 마찬가지로 검색의 경우 응용 프로그램 전달 텍스트 문자열 또는 **ISequentialStream** OLE DB driver for SQL Server.  
  
> [!NOTE]  
>  문자열 형태로 표시를 통해 XML 데이터를 보낼 수는 **ISequentialStream** 인터페이스를 가져와야 합니다 **ISequentialStream** DBTYPE_IUNKNOWN을 지정 하 고 설정으로 해당 *pObject* 인수 바인딩에 null입니다.  
  
 소비자 버퍼가 너무 작아 검색된 XML 데이터가 잘린 경우 길이가 알 수 없는 길이를 나타내는 0xffffffff로 반환될 수 있습니다. 이 동작은 실제 데이터 전에 길이 정보를 보내지 않고 클라이언트로 스트리밍되는 데이터 형식으로 구현와 일치 합니다. 경우에 따라 실제 길이가 반환 될 수 있습니다 때 공급자와 같은 전체 값을 버퍼링가 **irowset:: Getdata** 데이터 변환이 수행 되 고 있습니다.  
  
 SQL Server로 전송된 XML 데이터는 서버에서 이진 데이터로 처리됩니다. 이 동작 어떠한 변환도 일어나지 않으며 XML 파서는 XML 인코딩을 자동으로 검색을 허용 합니다. 이를 통해 보다 광범위한 XML 문서(예: UTF-8로 인코딩된 문서)를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 입력으로 사용할 수 있습니다.  
  
 입력 XML이 DBTYPE_WSTR로 바인딩된 경우 응용 프로그램에서는 XML이 이미 유니코드로 인코딩되었는지 확인하여 원치 않는 데이터 변환으로 인해 데이터가 손상되는 것을 방지해야 합니다.  
  
### <a name="data-bindings-and-coercions"></a>데이터 바인딩 및 강제 변환  
 다음 표에서 바인딩 및 강제 변환 형식을 나열 된 데이터를 사용 하 여 때 발생 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **xml** 데이터 형식입니다.  
  
|데이터 형식|SQL Server의<br /><br /> **XML**|SQL Server의<br /><br /> **비-XML**|SQL Server의<br /><br /> **XML**|SQL Server의<br /><br /> **비-XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|통과<sup>6,7</sup>|오류<sup>1</sup>|정상<sup>11, 6</sup>|오류<sup>8</sup>|  
|DBTYPE_BYTES|통과<sup>6,7</sup>|해당 없음<sup>2</sup>|정상 <sup>11, 6</sup>|해당 없음 <sup>2</sup>|  
|DBTYPE_WSTR|통과<sup>6, 10</sup>|해당 없음 <sup>2</sup>|정상<sup>4, 6, 12</sup>|해당 없음 <sup>2</sup>|  
|DBTYPE_BSTR|통과<sup>6, 10</sup>|해당 없음 <sup>2</sup>|정상 <sup>3</sup>|해당 없음 <sup>2</sup>|  
|DBTYPE_STR|정상<sup>6, 9, 10</sup>|해당 없음 <sup>2</sup>|정상<sup>5, 6, 12</sup>|해당 없음 <sup>2</sup>|  
|DBTYPE_IUNKNOWN|통한 바이트 스트림 **ISequentialStream**<sup>7</sup>|해당 없음 <sup>2</sup>|통한 바이트 스트림 **ISequentialStream**<sup>11</sup>|해당 없음 <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &AMP;#124; VT_ARRAY)|통과<sup>6,7</sup>|해당 없음 <sup>2</sup>|해당 사항 없음|해당 없음 <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|통과<sup>6, 10</sup>|해당 없음 <sup>2</sup>|정상<sup>3</sup>|해당 없음 <sup>2</sup>|  
  
 <sup>1</sup>서버 이외의 유형이 DBTYPE_XML가 지정 된 **icommandwithparameters:: Setparameterinfo** 고 접근자 유형이 DBTYPE_XML 이면 문이 실행 될 때 오류가 발생 (DB_E_ERRORSOCCURRED는 매개 변수 상태는 DBSTATUS_E_BADACCESSOR); 그렇지 않은 경우 데이터를 서버에 전송 되 하지만 서버 매개 변수의 데이터 형식으로 XML에서 암시적 변환이 중임을 나타내는 오류를 반환 합니다.  
  
 <sup>2</sup>이 문서의 범위를 초과 합니다.  
  
 <sup>3</sup>형식이 u t F-16이 고 (BOM) 순서 표시가 없으면 인코딩 사양 및 null 종결 없습니다.  
  
 <sup>4</sup>형식이 u t F-16, BOM, 없고 인코딩 사양, null 종료 합니다.  
  
 <sup>5</sup>형식은 null 종결자와 함께 클라이언트 코드 페이지로 인코딩된 멀티 바이트 문자입니다. 변환 서버에서 제공된 하는 유니코드 않을 데이터 손상, 하므로이 바인딩은 권장 되지 않습니다.  
  
 <sup>6</sup>by_ref가 사용 될 수 있습니다.  
  
 <sup>7</sup>utf-16 데이터는 BOM으로 시작 해야 합니다. 그렇지 않으면 서버에서 인코딩을 올바르게 인식할 수 없습니다.  
  
 <sup>8</sup>접근자 생성 시간 또는 인출 시간에 유효성 검사에서 발생할 수 있습니다. 오류는 DB_E_ERRORSOCCURRED이고 바인딩 상태는 DBBINDSTATUS_UNSUPPORTEDCONVERSION으로 설정됩니다.  
  
 <sup>9</sup>데이터가 서버로 전송 되기 전에 클라이언트 코드 페이지를 사용 하 여 유니코드로 변환 됩니다. 문서 인코딩이 클라이언트 코드 페이지가 일치 하지 않으면 하므로이 바인딩은 것이 좋습니다 데이터 손상이 발생할 수 있습니다.  
  
 <sup>10</sup>서버로 전송 되는 데이터에 항상 BOM이 추가 됩니다. 이미 데이터는 BOM으로 시작 된 경우 버퍼의 시작에 두 개의 Bom 게 됩니다. 서버에서는 첫 번째 BOM을 통해 인코딩을 UTF-16으로 인식한 다음 이 BOM을 삭제합니다. 두 번째 BOM은 너비가 0인 줄 바꿈하지 않는 공백 문자로 해석됩니다.  
  
 <sup>11</sup>형식이 u t F-16, 인코딩 사양, 서버에서 받은 데이터에 BOM 추가 됩니다. 서버에서 빈 문자열을 반환하더라도 BOM이 응용 프로그램에 반환됩니다. 버퍼 길이가 홀수 바이트이면 데이터가 올바르게 잘립니다. 전체 값이 청크로 반환되면 연결해서 올바른 값으로 다시 구성할 수 있습니다.  
  
 <sup>12</sup>버퍼 길이 두 개 미만의 문자-즉, null 종료-공간이 충분 하지 않으면 오버플로 오류가 보고 됩니다.  
  
> [!NOTE]  
>  NULL XML 값에 대해서는 데이터가 반환되지 않습니다.  
  
 XML 표준을 따르려면 UTF-16로 인코딩된 XML이 BOM(바이트 순서 표시), 즉 UTF-16 문자 코드 0xFEFF로 시작해야 합니다. WSTR 및 BSTR 바인딩을 사용 하는 작업을 하는 경우 OLE DB Driver for SQL Server 필요 하거나 인코딩이 바인딩에서 암시적으로 BOM을 추가 하지 않습니다. BYTES, XML 또는 IUNKNOWN 바인딩을 사용하는 경우 BOM을 추가하는 목적은 다른 XML 프로세서 및 저장소 시스템을 간편하게 다룰 수 있도록 하는 데 있습니다. BOM과 함께 사용할 수 해야이 경우 u t F-16으로 인코딩된 XML에 및 대부분의 XML 프로세서 (예: SQL Server) 값의 처음 몇 바이트를 검사 하 여 인코딩을 추론 이후 응용 프로그램에서는 실제 인코딩을 확인할 하지 필요 합니다. 바이트, XML, SQL Server 용 OLE DB 드라이버에서 수신 하는 XML 데이터 또는 IUNKNOWN 바인딩을 항상 BOM이 있는 및 포함 된 인코딩 선언이 없는 u t F-16으로 인코딩됩니다.  
  
 OLE DB 핵심 서비스에서 제공 하는 데이터 변환 (**IDataConvert**)은 DBTYPE_XML에 적용 되지 않습니다.  
  
 데이터가 서버로 전송되면 유효성 검사가 수행됩니다. 클라이언트 쪽 유효성 검사 및 인코딩 변경 내용이 응용 프로그램에서 처리 해야 합니다. XML 데이터를 직접 처리 하지 하지만 처리 대신 DOM 이나 SAX 판독기를 사용 해야 하는 것이 좋습니다.  
  
 DBTYPE_NULL 및 DBTYPE_EMPTY는 입력 매개 변수에 대해서는 바인딩할 수 있지만 출력 매개 변수나 결과에 대해서는 바인딩할 수 없습니다. 입력 매개 변수에 대해 바인딩할 경우 상태를 DBSTATUS_S_ISNULL 또는 DBSTATUS_S_DEFAULT로 설정해야 합니다.  
  
 DBTYPE_XML은 DBTYPE_EMPTY와 DBTYPE_NULL로 변환할 수 있습니다. DBTYPE_EMPTY는 DBTYPE_XML로 변환할 수 있지만 DBTYPE_NULL은 DBTYPE_XML로 변환할 수 없습니다. 이는 DBTYPE_WSTR와 일치합니다.  
  
 DBTYPE_IUNKNOWN (같이 앞의 표에), 지원 되는 바인딩 이지만 DBTYPE_XML과 DBTYPE_IUNKNOWN 간에 변환이 없습니다. DBTYPE_IUNKNOWN을 DBTYPE_BYREF와는 사용할 수 없습니다.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>OLE DB 행 집합의 추가 내용 및 변경 내용  
 OLE DB Driver for SQL Server 새 값을 추가 하거나 많은 핵심 OLE DB 스키마 행 집합을 변경 합니다.  
  
#### <a name="the-columns-and-procedureparameters-schema-rowsets"></a>COLUMNS 및 PROCEDURE_PARAMETERS 스키마 행 집합  
 COLUMNS 및 PROCEDURE_PARAMETERS 스키마 행 집합에 대 한 추가 열을 다음과 같습니다.  
  
|열 이름|형식|Description|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 스키마 컬렉션이 정의된 카탈로그의 이름입니다. 비-XML 열 이나 형식화 되지 않은 XML 열에 대해 NULL입니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 스키마 컬렉션이 정의된 스키마의 이름입니다. 비-XML 열 이나 형식화 되지 않은 XML 열에 대해 NULL입니다.|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|XML 스키마 컬렉션의 이름입니다. 비-XML 열 이나 형식화 되지 않은 XML 열에 대해 NULL입니다.|  
  
#### <a name="the-providertypes-schema-rowset"></a>PROVIDER_TYPES 스키마 행 집합  
 PROVIDER_TYPES 스키마 행 집합에서는 COLUMN_SIZE 값이 0에 대 한는 **xml** 데이터 형식이 고 DATA_TYPE이 DBTYPE_XML입니다.  
  
#### <a name="the-ssxmlschema-schema-rowset"></a>SS_XMLSCHEMA 스키마 행 집합  
 새로운 스키마 행 집합인 SS_XMLSCHEMA는 클라이언트가 XML 스키마 정보를 검색할 수 있도록 도입되었습니다. SS_XMLSCHEMA 행 집합에는 다음과 같은 열을 포함 되어 있습니다.  
  
|열 이름|형식|Description|  
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
 OLE DB Driver for SQL Server 새 값을 추가 하거나 많은 핵심 OLE DB 속성 집합 변경 합니다.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>DBPROPSET_SQLSERVERPARAMETER 속성 집합  
 지원 하기 위해는 **xml** OLE DB를 통해 데이터 형식 OLE DB Driver for SQL Server는 다음 값을 포함 된 새로운 DBPROPSET_SQLSERVERPARAMETER 속성 집합을 구현 합니다.  
  
|속성|형식|Description|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 스키마 컬렉션이 정의된 카탈로그(데이터베이스)의 이름입니다. 일부 SQL 세 부분으로 된 이름 식별자입니다.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|스키마 컬렉션 내 XML 스키마의 이름입니다. SQL의 세 부분으로 구성된 이름 식별자의 일부입니다.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|카탈로그 내 XML 스키마 컬렉션의 이름입니다. SQL의 세 부분으로 구성된 이름 식별자의 일부입니다.|  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>DBPROPSET_SQLSERVERCOLUMN 속성 집합  
 테이블 생성을 지원 하기 위해는 **ITableDefinition** 인터페이스, OLE DB Driver SQL Server는 DBPROPSET_SQLSERVERCOLUMN 속성 집합에 3 개의 새 열을 추가 합니다.  
  
|속성|형식|Description|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|형식화된 XML 열에 대해서는 이 속성이 XML 스키마가 저장된 카탈로그의 이름을 지정하는 문자열입니다. 다른 열 유형에 대해서는 이 속성이 빈 문자열을 반환합니다.|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|형식화된 XML 열에 대해서는 이 속성이 이 열을 정의하는 XML 스키마의 이름을 지정하는 문자열입니다.|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|형식화된 XML 열에 대해서는 이 속성이 값을 정의하는 XML 스키마 컬렉션의 이름을 지정하는 문자열입니다.|  
  
 SSPROP_PARAM 값과 마찬가지로 이러한 속성은 모두 옵션이며 기본적으로 비어 있습니다. SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME 및 SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME은 SSPROP_COL_XML_SCHEMACOLLECTIONNAME이 지정된 경우에만 지정할 수 있습니다. XML을 서버에 전달할 때 이러한 값이 포함되어 있으면 현재 데이터베이스에 대해 이들 속성의 존재 여부(유효성)가 확인되고 인스턴스 데이터가 스키마에 대해 검사됩니다. 어떤 경우든 이러한 속성은 모두 비어 있거나 모두 채워져 있어야 올바른 상태입니다.  
  
### <a name="ole-db-interface-additions-and-changes"></a>OLE DB 인터페이스의 추가 내용 및 변경 내용  
 OLE DB Driver for SQL Server 새 값을 추가 하거나 많은 핵심 OLE DB 인터페이스를 변경 합니다.  
  
#### <a name="the-isscommandwithparameters-interface"></a>ISSCommandWithParameters 인터페이스  
 지원 하기 위해는 **xml** OLE DB를 통해 데이터 형식을 OLE DB Driver for SQL Server의 추가 포함 하 여 변경 내용 많은 구현는 [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md) 인터페이스입니다. 이 새 인터페이스는 핵심 OLE DB 인터페이스에서 상속 **ICommandWithParameters**합니다. 상속 되며, 세 가지 방법 외에도 **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, 및 **SetParameterInfo**; **ISSCommandWithParameters** 제공는 [GetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) 및 [SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) 서버 특정 처리에 사용 되는 메서드 데이터 형식입니다.  
  
> [!NOTE]  
>  **ISSCommandWithParameters** 인터페이스도에서 활용 하는 새로운 SSPARAMPROPS 구조입니다.  
  
#### <a name="the-icolumnsrowset-interface"></a>IColumnsRowset 인터페이스  
 OLE DB Driver for SQL Server에는 다음 항목을 추가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-특정 열에서 반환 된 행 집합에는 **icolumnrowset::** 메서드. 이러한 열에는 XML 스키마 컬렉션의 세 부분으로 구성된 이름이 포함됩니다. 비XML 열이나 형식화되지 않은 XML 열에 대해서는 이 세 열 모두 기본값인 NULL을 사용합니다.  
  
|열 이름|형식|Description|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|XML 스키마 컬렉션이 속한 카탈로그입니다.<br /><br /> 그렇지 않으면 NULL입니다.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|XML 스키마 컬렉션이 속한 스키마입니다. 그렇지 않으면 NULL입니다.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|형식화된 XML 열에 대해서는 XML 스키마 컬렉션의 이름이고, 그렇지 않으면 NULL입니다.|  
  
#### <a name="the-irowset-interface"></a>IRowset 인터페이스  
 XML 열에는 XML 인스턴스를 통해 검색 된 **irowset:: Getdata** 메서드. 클라이언트에서 지정한 바인딩에 따라 XML 인스턴스가 DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML, DBTYPE_STR, DBTYPE_BYTES로 검색되거나 DBTYPE_IUNKNOWN을 통해 인터페이스로 검색될 수 있습니다. 소비자가 DBTYPE_BSTR, DBTYPE_WSTR 또는 DBTYPE_VARIANT를 지정하면 공급자는 XML 인스턴스를 사용자가 요청한 형식으로 변환한 후 해당 바인딩에 지정된 위치에 가져다 놓습니다.  
  
 소비자가 DBTYPE_IUNKNOWN을 지정 하는 경우 설정의 *pObject* 인수를 NULL 또는 설정은 *pObject* 인수를 IID_ISequentialStream, 공급자가 반환는 **ISequentialStream** 소비자 열에서 XML 데이터를 스트리밍할 수 있도록 인터페이스를 소비자입니다. **ISequentialStream** XML 데이터를 유니코드 문자 스트림으로 반환 합니다.  
  
 DBTYPE_IUNKNOWN에 바인딩된 XML 값을 반환할 때 공급자는 `sizeof (IUnknown *)`의 크기 값을 보고합니다. 이 동작은 해킹 바인딩되는 경우 열 DBTYPE_IUnknown 또는 DBTYPE_IDISPATCH, 및 DBTYPE_IUNKNOWN/isequentialstream 정확한 열 크기를 알 수 없는 경우와 일치 합니다.  
  
#### <a name="the-irowsetchange-interface"></a>IRowsetChange 인터페이스  
 소비자는 두 가지 방법으로 열의 XML 인스턴스를 업데이트할 수 있습니다. 저장소 개체를 통해 첫 번째 식은 **ISequentialStream** 공급자가 생성 합니다. 소비자는 호출할 수는 **isequentialstream:: Write** 메서드를 직접 공급자에 의해 반환 된 XML 인스턴스를 업데이트 합니다.  
  
 다른 하나는 **irowsetchange:: Setdata** 또는 **irowsetchange:: Insertrow** 메서드. 이 방법을 사용할 경우 소비자 버퍼의 XML 인스턴스를 DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML 또는 DBTYPE_IUNKNOWN 유형의 바인딩에 지정할 수 있습니다.  
  
 DBTYPE_BSTR, DBTYPE_WSTR 또는 DBTYPE_VARIANT를 지정 하는 경우 공급자는 소비자 버퍼에 적절 한 열에 있는 XML 인스턴스를 저장 합니다.  
  
 소비자 만들어야 DBTYPE_IUNKNOWN/ISequentialStream을 지정 소비자 저장소 개체를 지정 하지 않는 경우는 **ISequentialStream** 사전에 개체 하 고, 개체에서 XML 문서를 바인딩하고, 그런 다음는 개체를 통해 공급자는 **irowsetchange:: Setdata** 메서드. 소비자는 저장소를 만들 수도 개체, pObject 인수를 IID_ISequentialStream으로 설정 하 고, 만들는 **ISequentialStream** 개체를 전달 합니다는 **ISequentialStream** 개체는 **irowsetchange:: Setdata** 메서드. 두 경우 모두 공급자를 통해 XML 개체를 검색할 수는 **ISequentialStream** 개체를 적절 한 열에 삽입 합니다.  
  
#### <a name="the-irowsetupdate-interface"></a>IRowsetUpdate 인터페이스  
 **IRowsetUpdate** 인터페이스 지연 된 업데이트에 대 한 기능을 제공 합니다. 행 집합을 사용할 수 있는 데이터 사용할 수 없어 다른 트랜잭션에서 소비자 호출할 때까지 **irowsetupdate:: Update** 메서드.  
  
#### <a name="the-irowsetfind-interface"></a>IRowsetFind 인터페이스  
 **irowsetfind:: Findnextrow** 메서드는 사용 하지는 **xml** 데이터 형식입니다. 때 **irowsetfind:: Findnextrow** 호출 되 고 *hAccessor* 인수에 DBTYPE_XML 열 지정도 DB_E_BADBINDINFO가 반환 됩니다. 이는 검색하는 열의 유형에 관계없이 발생합니다. 다른 바인딩 형식에 대해서는 **FindNextRow** 검색할 열 경우 db_e_badcompareop 실패는 **xml** 데이터 형식입니다.  
 
  
## <a name="see-also"></a>관련 항목  
 [OLE DB Driver for SQL Server 기능](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
