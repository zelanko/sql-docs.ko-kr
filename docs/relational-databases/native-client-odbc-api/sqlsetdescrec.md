---
title: SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 85c463faa7f6812bbd0b4526cbe0fe0a80c62537
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618151"
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  이 항목에서는 관련 된 SQLSetDescRec 기능 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client입니다.  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec 및 테이블 반환 매개 변수  
 SQLSetDescRec는 테이블 반환 매개 변수 및 테이블 반환 매개 변수 열의 설명자 필드 설정에 사용할 수 있습니다. 테이블 반환 매개 변수 열은 설명자 헤더 필드 SQL_SOPT_SS_PARAM_FOCUS가 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정된 레코드의 서수로 설정된 경우에만 사용할 수 있습니다. SQL_SOPT_SS_PARAM_FOCUS에 대 한 자세한 내용은 참조 하세요. [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)합니다.  
  
 다음 표에서는 매개 변수와 설명자 필드 간의 매핑에 대해 설명합니다.  
  
|매개 변수|테이블 반환 매개 변수 열을 비롯한 테이블 반환 매개 변수가 아닌 유형에 대한 관련 특성|테이블 반환 매개 변수에 대한 관련 특성|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*형식*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*SubType*|무시됨|SQL_DATETIME 또는 SQL_INTERVAL 유형의 레코드에 대해 이 값을 SQL_DESC_DATETIME_INTERVAL_CODE로 설정합니다.|  
|*길이*|SQL_DESC_OCTET_LENGTH|테이블 반환 매개 변수 유형 이름의 길이입니다. 유형 이름이 null로 끝나는 경우 SQL_NTS이고, 테이블 반환 매개 변수 유형 이름이 필요하지 않은 경우 0입니다.|  
|*전체 자릿수*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*소수 자릿수*|SQL_DESC_SCALE|사용되지 않습니다. 이 매개 변수는 0이어야 합니다.|  
|*DataPtr*|APD의 SQL_DESC_DATA_PTR|SQL_CA_SS_TYPE_NAME<br /><br /> 저장 프로시저 호출에서 이 매개 변수는 선택 사항이며, 필요하지 않은 경우 NULL을 지정할 수 있습니다. 프로시저 호출이 아닌 SQL 문에 대해서는 이 매개 변수를 지정해야 합니다.<br /><br /> *DataPtr* 응용 프로그램 가변 행 바인딩을 사용 하는 경우이 테이블 반환 매개 변수를 식별 하는 데 사용할 수 있는 고유한 값으로도 사용 됩니다.|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> 테이블 반환 매개 변수의 경우 이 값은 전송할 행 수나 SQL_DATA_AT_EXEC입니다. 이것이 SQLExecDirect를 사용 하 여 전송할 행 수를 유지 하는 값에 대 한 포인터입니다.|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 참조 하세요. [테이블 반환 매개 변수 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLSetDescRec 지원  
 날짜/시간 유형에 대해 허용되는 값은 다음과 같습니다.  
  
||*형식*|*SubType*|*길이*|*전체 자릿수*|*소수 자릿수*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|DATETIME|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|날짜|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|Time|SQL_SS_TIME2|0|10|0..7|0..7|  
|Datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLSetDescRec 지원  
 **SQLSetDescRec** 큰 CLR 사용자 정의 형식 (Udt)를 지원 합니다. 자세한 내용은 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQLSetDescRec](http://go.microsoft.com/fwlink/?LinkId=80704)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
