---
title: 큰 CLR 사용자 정의 형식 (OLE DB) | Microsoft Docs
description: 큰 CLR 사용자 정의 형식(OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab00a5bac7c55a7e627b7220a4b0af7948fa84f1
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="large-clr-user-defined-types-ole-db"></a>큰 CLR 사용자 정의 형식(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 OLE DB에서 OLE DB Driver 큰 공용 언어 런타임 (CLR) 사용자 정의 형식 (Udt)를 지원 하도록 SQL Server에 대 한 변경 내용을 설명 합니다.  
  
 SQL Server 용 OLE DB Driver의 큰 CLR Udt에 대 한 지원에 대 한 자세한 내용은 참조 [Large CLR User-Defined 형식](../../oledb/features/large-clr-user-defined-types.md)합니다. 샘플을 보려면 [사용 큰 CLR Udt &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-large-clr-udts-ole-db.md)합니다.  
  
## <a name="data-format"></a>데이터 형식  
 OLE DB Driver for SQL Server를 사용 하 여 ~을 큰 개체 (LOB) 형식에 대 한 무제한 크기인 값의 길이 나타내는 0입니다. ~0은 8,000바이트보다 큰 CLR UDT 크기도 나타냅니다.  
  
 다음 표에서는 매개 변수 및 행 집합의 데이터 형식 매핑을 보여 줍니다.  
  
|SQL Server 데이터 형식|OLE DB 데이터 형식|메모리 레이아웃|Value|  
|--------------------------|----------------------|-------------------|-----------|  
|CLR UDT|DBTYPE_UDT|BYTE[](byte array\)|132 (oledb.h)|  
  
 UDT 값은 바이트 배열로 나타납니다. 16진수 문자열로의 변환 및 그 반대의 변환이 지원됩니다. 리터럴 값은 접두사 "0x"를 사용하여 16진수 문자열로 나타납니다. 16진수 문자열은 밑수가 16인 이진 데이터의 텍스트 표현입니다. 예제는 서버 유형으로 변환 되기 **varbinary(10)** 를 DBTYPE_STR로 줄어들고 결과적 모든 문자 쌍이 단일 바이트를 나타내는 20 자의 16 진수 표현입니다.  
  
## <a name="parameter-properties"></a>매개 변수 속성  
 DBPROPSET_SQLSERVERPARAMETER 속성 집합은 OLE DB를 통해 UDT를 지원합니다. 자세한 내용은 참조 [사용자 형식](../../oledb/features/using-user-defined-types.md)합니다.  
  
## <a name="column-properties"></a>열 속성  
 DBPROPSET_SQLSERVERCOLUMN 속성 집합은 OLE DB를 통해 테이블 만들기를 지원합니다. 자세한 내용은 참조 [사용자 형식](../../oledb/features/using-user-defined-types.md)합니다.  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>ITableDefinition::CreateTable의 데이터 형식 매핑  
 다음 정보를 사용 하는 **DBCOLUMNDESC** itabledefinition:: Createtable UDT 열이 필요한 경우 사용 되는 구조:  
  
|OLE DB 데이터 형식 (*wType*)|*pwszTypeName*|SQL Server 데이터 형식|*rgPropertySets*|  
|----------------------------------|--------------------|--------------------------|----------------------|  
|DBTYPE_UDT|무시됨|UDT|DBPROPSET_SQLSERVERCOLUMN 속성 집합을 포함해야 합니다.|  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 정보를 통해 DBPARAMINFO 구조에 반환 **prgParamInfo** 는 다음과 같습니다.  
  
|매개 변수 유형|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|-------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (8,000바이트 이하 길이)|"DBTYPE_UDT"|*n*|정의되지 않음|정의되지 않음|clear|  
|DBTYPE_UDT<br /><br /> (8,000바이트를 초과하는 길이)|"DBTYPE_UDT"|~0|정의되지 않음|정의되지 않음|집합|  
  
## <a name="icommandwithparameterssetparameterinfo"></a>ICommandWithParameters::SetParameterInfo  
 DBPARAMBINDINFO 구조에 제공된 정보는 다음을 준수해야 합니다.  
  
|매개 변수 유형|*pwszDataSourceType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|--------------------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (8,000바이트 이하 길이)|DBTYPE_UDT|*n*|무시됨|무시됨|DBTYPE_IUNKNOWN을 사용하여 매개 변수가 전달되는 경우 설정해야 합니다.|  
|DBTYPE_UDT<br /><br /> (8,000바이트를 초과하는 길이)|DBTYPE_UDT|~0|무시됨|무시됨|무시됨|  
  
## <a name="isscommandwithparameters"></a>ISSCommandWithParameters  
 응용 프로그램 사용 **ISSCommandWithParameters** 을 가져오고 매개 변수 속성 섹션에 정의 된 매개 변수 속성을 설정 합니다.  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 반환되는 열은 다음과 같습니다.  
  
|열 유형|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE|DBCOLUMN_FLAGS_ISLONG|DBCOLUMNS_ISSEARCHABLE|DBCOLUMN_OCTETLENGTH|  
|-----------------|--------------------|--------------------------|-------------------------|---------------------|-----------------------------|-----------------------------|---------------------------|  
|DBTYPE_UDT<br /><br /> (8,000바이트 이하 길이)|DBTYPE_UDT|*n*|NULL|NULL|지우기|DB_ALL_EXCEPT_LIKE|n|  
|DBTYPE_UDT<br /><br /> (8,000바이트를 초과하는 길이)|DBTYPE_UDT|~0|NULL|NULL|Set|DB_ALL_EXCEPT_LIKE|0|  
  
 UDT에 대해 다음 열도 정의됩니다.  
  
|열 식별자|형식|Description|  
|-----------------------|----------|-----------------|  
|DBCOLUMN_UDT_CATALOGNAME|DBTYPE_WSTR|UDT 열의 경우 UDT가 정의된 카탈로그의 이름입니다.|  
|DBCOLUMN_UDT_SCHEMANAME|DBTYPE_WSTR|UDT 열의 경우 UDT가 정의된 스키마의 이름입니다.|  
|DBCOLUMN_UDT_NAME|DBTYPE_WSTR|UDT 열의 경우 UDT의 단일 부분 이름입니다.|  
|DBCOLUMN_ASSEMBLY_TYPENAME|DBTYPE_WSTR|UDT 열의 경우 UDT의 전체 유형 이름입니다. 어셈블리 유형의 정규화된 이름을 사용하면 Type.GetType 메서드를 사용하여 해당 유형의 개체를 인스턴스화할 수 있습니다.|  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 DBCOLUMNINFO 구조에 반환되는 정보는 다음과 같습니다.  
  
|매개 변수 유형|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBCOLUMNFLAGS_ISLONG|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------|  
|DBTYPE_UDT<br /><br /> (8,000바이트 이하 길이)|DBTYPE_UDT|*n*|~0|~0|지우기|  
|DBTYPE_UDT<br /><br /> (8,000바이트를 초과하는 길이)|DBTYPE_UDT|~0|~0|~0|Set|  
  
## <a name="columns-rowset-schema-rowsets"></a>COLUMNS 행 집합(스키마 행 집합)  
 UDT 유형에 대해 다음 열 값이 반환됩니다.  
  
|열 유형|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_ISLONG|CHARACTER_OCTET_LENGTH|  
|-----------------|----------------|-----------------------------------------|------------------------------|  
|DBTYPE_UDT<br /><br /> (8,000바이트 이하 길이)|DBTYPE_UDT|지우기|*n*|  
|DBTYPE_UDT<br /><br /> (8,000바이트를 초과하는 길이)|DBTYPE_UDT|Set|0|  
  
 UDT에 대해 다음 추가 열이 정의됩니다.  
  
|열 식별자|형식|Description|  
|-----------------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|UDT 열의 경우 UDT가 정의된 카탈로그의 이름입니다.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|UDT 열의 경우 UDT가 정의된 스키마의 이름입니다.|  
|SS_UDT_NAME|DBTYPE_WSTR|UDT 열의 경우 UDT의 단일 부분 이름입니다.|  
|SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|UDT 열의 경우 UDT의 전체 유형 이름입니다. 어셈블리 유형의 정규화된 이름을 사용하면 Type.GetType 메서드를 사용하여 해당 유형의 개체를 인스턴스화할 수 있습니다.|  
  
 PROCEDURE_PARAMETERS 행 집합과 관련해서 DATA_TYPE에는 COLUMNS 스키마 행 집합과 동일한 값이 포함되고 TYPE_NAME에는 UDT가 포함됩니다. 동일한 추가 열도 정의됩니다.  
  
 PROVIDER_TYPES 스키마 행 집합에는 사용자 정의 형식이 나타나지 않습니다.  
  
## <a name="bindings-and-conversions"></a>바인딩 및 변환  
  
|바인딩 데이터 형식|UDT에서 서버로|비 UDT에서 서버로|서버에서 UDT로|서버에서 비 UDT로|  
|----------------------|-------------------|------------------------|---------------------|--------------------------|  
|DBTYPE_UDT|지원 되는 (5)|오류 (1)|지원 되는 (5)|오류 (4)|  
|DBTYPE_BYTES|지원 되는 (5)|해당 사항 없음|지원 되는 (5)|해당 사항 없음|  
|DBTYPE_WSTR|지원됨 (2), (5)|해당 사항 없음|지원됨 (3), (5), (6)|해당 사항 없음|  
|DBTYPE_BSTR|지원됨 (2), (5)|해당 사항 없음|지원 되는 (3), (5)|해당 사항 없음|  
|DBTYPE_STR|지원됨 (2), (5)|해당 사항 없음|지원 되는 (3), (5)|해당 사항 없음|  
|DBTYPE_IUNKNOWN|지원 되는 (6)|해당 사항 없음|지원 되는 (6)|해당 사항 없음|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|지원됨 (5)|해당 사항 없음|지원 되는 (3), (5)|해당 사항 없음|  
|DBTYPE_VARIANT (VT_BSTR)|지원됨 (2), (5)|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
  
### <a name="key-to-symbols"></a>기호 설명  
  
|기호|의미|  
|------------|-------------|  
|1.|서버 이외의 유형이 DBTYPE_UDT로 지정 **icommandwithparameters:: Setparameterinfo** 접근자 유형이 DBTYPE_UDT 인 이며 문이 실행 될 때 오류가 발생 합니다.  오류는 DB_E_ERRORSOCCURRED이고 매개 변수 상태는 DBSTATUS_E_BADACCESSOR가 됩니다.<br /><br /> UDT가 아닌 서버 매개 변수에 대해 UDT 유형의 매개 변수를 지정하는 것은 오류입니다.|  
|2|데이터가 16진수 문자열에서 이진 데이터로 변환됩니다.|  
|3|데이터가 이진 데이터에서 16진수 문자열로 변환됩니다.|  
|4|유효성 검사 사용 시 발생할 수 **CreateAccessor** 또는 **GetNextRows**합니다. 오류는 DB_E_ERRORSOCCURRED이고 바인딩 상태는 DBBINDSTATUS_UNSUPPORTEDCONVERSION으로 설정됩니다.|  
|5|BY_REF가 사용될 수 있습니다.|  
|6|UDT 매개 변수를 DBBINDING의 DBTYPE_IUNKNOWN으로 바인딩할 수 있습니다. DBTYPE_IUNKNOWN으로 응용 프로그램 ISequentialStream 인터페이스를 사용 하 여 스트림으로 데이터를 처리 하려는 것을 나타냅니다. 소비자가 지정 하는 경우 *wType* DBTYPE_IUNKNOWN 유형으로 바인딩 및 해당 열 또는 출력 저장된 프로시저의 매개 변수는 UDT, OLE DB Driver for SQL Server는 ISequentialStream을 반환 합니다. 입력된 매개 변수에 대 한 OLE DB Driver for SQL Server에 대 한 쿼리 하는 ISequentialStream 인터페이스에 대 한 합니다.<br /><br /> 큰 UDT의 경우 DBTYPE_IUNKNOWN 바인딩을 사용하는 동안 UDT 데이터의 길이를 바인딩하지 않도록 선택할 수 있습니다. 하지만 작은 UDT의 경우에는 길이를 바인딩해야 합니다. 다음 중 하나 이상이 True이면 DBTYPE_UDT 매개 변수를 큰 UDT로 지정할 수 있습니다.<br />*ulParamParamSize* 은 ~ 0입니다.<br />DBPARAMBINDINFO 구조체에 DBPARAMFLAGS_ISLONG이 설정되어 있습니다.<br /><br /> 행 데이터의 경우 DBTYPE_IUNKNOWN 바인딩만 큰 UDT에 사용할 수 있습니다. 열 행 집합에서 icolumnsinfo:: Getcolumninfo 메서드를 사용 하 여 큰 UDT 유형이 있는지 확인 하거나 IColumnsInfo 인터페이스 개체의 명령 수 있습니다. 다음 중 하나 이상이 True이면 DBTYPE_UDT 열은 큰 UDT 열입니다.<br />에 DBCOLUMNFLAGS_ISLONG 플래그가 설정 되어 *dwFlags* DBCOLUMNINFO 구조의 멤버입니다. <br />*ulColumnSize* DBCOLUMNINFO의 구성원은 ~ 0입니다.|  
  
 DBTYPE_NULL 및 DBTYPE_EMPTY는 입력 매개 변수에 대해서는 바인딩할 수 있지만 출력 매개 변수나 결과에 대해서는 바인딩할 수 없습니다. 입력 매개 변수에 대해 바인딩할 경우 DBTYPE_NULL을 나타내는 DBSTATUS_S_ISNULL 또는 DBTYPE_EMPTY를 나타내는 DBSTATUS_S_DEFAULT로 상태를 설정해야 합니다. DBTYPE_BYREF는 DBTYPE_NULL 또는 DBTYPE_EMPTY에 사용할 수 없습니다.  
  
 DBTYPE_UDT를 DBTYPE_EMPTY 및 DBTYPE_NULL로 변환할 수도 있습니다. 하지만 DBTYPE_NULL 및 DBTYPE_EMPTY를 DBTYPE_UDT로 변환할 수는 없습니다. 이는 DBTYPE_BYTES와 일치합니다. **ISSCommandWithParameters** 프로세스 Udt 매개 변수로 사용 됩니다.  
  
 OLE DB 핵심 서비스에서 제공 하는 데이터 변환 (**IDataConvert**) DBTYPE_UDT에 적용 되지 않습니다.  
  
 다른 바인딩은 지원되지 않습니다.  
  
## <a name="comparability-for-irowsetfind"></a>IRowsetFind 비교  
 UDT 유형의 경우 다음과 같은 비교만 지원됩니다.  
  
-   EQ  
  
-   NE  
  
-   IGNORE  
  
 다른 비교를 시도하면 DB_E_BADCOMPAREOP가 반환됩니다.  
  
## <a name="bcp-support-for-udts"></a>UDT에 대한 BCP 지원  
 UDT 값은 문자나 이진 값으로만 가져오고 내보낼 수 있습니다.  
  
## <a name="down-level-client-behavior-for-udts"></a>UDT에 대한 하위 수준 클라이언트 동작  
 UDT에 적용되는 하위 수준 클라이언트와의 유형 매핑은 다음과 같습니다.  
  
|클라이언트 버전|DBTYPE_UDT<br /><br /> (8,000바이트 이하 길이)|DBTYPE_UDT<br /><br /> (8,000바이트를 초과하는 길이)|  
|--------------------|------------------------------------------------------------------|---------------------------------------------------------|  
|SQL Server 2005|UDT|varbinary(max)|  
|SQL Server 2008 이상|UDT|UDT|  
  
 때 **DataTypeCompatibility** "80"으로 설정 됩니다 (SSPROP_INIT_DATATYPECOMPATIBILITY), 큰 UDT 유형이 하위 수준 클라이언트에 대 한 나타나는 동일한 방식으로 클라이언트에 표시 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [큰 CLR 사용자 정의 형식](../../oledb/features/large-clr-user-defined-types.md)  
  
  

