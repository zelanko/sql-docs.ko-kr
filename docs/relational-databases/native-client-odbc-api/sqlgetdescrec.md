---
title: SQLGetDescRec | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42c8a45bb50e5fda8946cc3819aa4702f5c2fb3f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299563"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트에 특정한 SQLGetDescRec 기능에 대해 설명합니다.  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec 및 테이블 반환 매개 변수  
 SQLGetDescRec는 테이블 값 매개 변수 및 테이블 값 매개 변수 열의 특성에 대한 값을 얻는 데 사용할 수 있습니다. SQLGetDescRec의 *RecNumber* 매개 변수는 SQLBindParameter의 *ParameterNumber* 매개 변수에 해당 합니다.  
  
 테이블 반환 매개 변수 열은 설명자 헤더 필드 SQL_SOPT_SS_PARAM_FOCUS가 SQL_DESC_TYPE이 SQL_SS_TABLE로 설정된 레코드의 서수로 설정된 경우에만 사용할 수 있습니다. SQL_SOPT_SS_PARAM_FOCUS 대한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)을 참조하십시오.  
  
 SQLGetDescRec는 다음 데이터를 반환합니다.  
  
|매개 변수|테이블 반환 매개 변수|테이블 반환 매개 변수 열 및 기타 매개 변수|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*이름*|저장 프로시저 호출의 경우 형식 매개 변수 이름, 다른 경우 길이가 0인 문자열|테이블 반환 매개 변수 열 이름|  
|*타이핑 Ptr*|SQL_DESC_TYPE 테이블 반환 매개 변수의 경우 SQL_SS_TABLE|SQL_DESC_TYPE|  
|*하위 유형 Ptr*|정의되지 않음|SQL_DESC_DATETIME_INTERVAL_CODE(형식이 SQL_DATETIME 또는 SQL_INTERVAL인 레코드의 경우)|  
|*길이 Ptr*|0|SQL_DESC_OCTET_LENGTH|  
|*정밀Ptr*|0|SQL_DESC_PRECISION|  
|*스케일 Ptr*|0|SQL_DESC_SCALE|  
|*널러블 Ptr*|1|SQL_DESC_NULLABLE|  
  
 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;[&#40;테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLGetDescRec 지원  
 날짜/시간 형식에 대해 반환되는 값은 다음과 같습니다.  
  
||*타이핑 Ptr*|*하위 유형 Ptr*|*길이 Ptr*|*정밀Ptr*|*스케일 Ptr*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|Datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLGetDescRec 지원  
 **SQLGetDescRec는** 큰 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
