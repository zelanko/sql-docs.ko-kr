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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a083aa6d17a84ff4c801ad5f5b270c7f0ddcb355
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301915"
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client와 관련 된 SQLSetDescRec 기능에 대해 설명 합니다.  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec 및 테이블 반환 매개 변수  
 SQLSetDescRec를 사용 하 여 테이블 반환 매개 변수 및 테이블 반환 매개 변수 열의 설명자 필드를 설정할 수 있습니다. 테이블 반환 매개 변수 열은 설명자 헤더 필드 SQL_SOPT_SS_PARAM_FOCUS가 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정된 레코드의 서수로 설정된 경우에만 사용할 수 있습니다. SQL_SOPT_SS_PARAM_FOCUS에 대한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 다음 표에서는 매개 변수와 설명자 필드 간의 매핑에 대해 설명합니다.  
  
|매개 변수|테이블 반환 매개 변수 열을 포함 하 여 비 테이블 반환 매개 변수 형식에 대 한 관련 특성|테이블 반환 매개 변수에 대한 관련 특성|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*Type*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*하위 형식*|무시됨|SQL_DATETIME 또는 SQL_INTERVAL 유형의 레코드에 대해 이 값을 SQL_DESC_DATETIME_INTERVAL_CODE로 설정합니다.|  
|*길이*|SQL_DESC_OCTET_LENGTH|테이블 반환 매개 변수 유형 이름의 길이입니다. 유형 이름이 null로 끝나는 경우 SQL_NTS이고, 테이블 반환 매개 변수 유형 이름이 필요하지 않은 경우 0입니다.|  
|*정밀도*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*규모*|SQL_DESC_SCALE|사용되지 않습니다. 이 매개 변수는 0이어야 합니다.|  
|*DataPtr*|APD의 SQL_DESC_DATA_PTR|SQL_CA_SS_TYPE_NAME<br /><br /> 저장 프로시저 호출에서 이 매개 변수는 선택 사항이며, 필요하지 않은 경우 NULL을 지정할 수 있습니다. 프로시저 호출이 아닌 SQL 문에 대해서는 이 매개 변수를 지정해야 합니다.<br /><br /> *Dataptr* 은 가변 행 바인딩이 사용 될 때 응용 프로그램에서이 테이블 반환 매개 변수를 식별 하는 데 사용할 수 있는 고유 값으로도 사용 됩니다.|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> 테이블 반환 매개 변수의 경우 이 값은 전송할 행 수나 SQL_DATA_AT_EXEC입니다. SQLExecDirect를 사용 하 여 전송할 행 수를 보유 하는 값에 대 한 포인터입니다.|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLSetDescRec 지원  
 날짜/시간 유형에 대해 허용되는 값은 다음과 같습니다.  
  
||*Type*|*하위 형식*|*길이*|*정밀도*|*규모*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|Datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLSetDescRec 지원  
 **SQLSetDescRec** 는 많은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC&#41;&#40;LARGE CLR 사용자 정의 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLSetDescRec](https://go.microsoft.com/fwlink/?LinkId=80704)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
