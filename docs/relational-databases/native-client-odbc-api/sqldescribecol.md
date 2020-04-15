---
title: SQLDescribeCol | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e0e9a03b2e8635618afbdc615a6f77dfe05c533e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302588"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  실행된 문의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경우 네이티브 클라이언트 ODBC 드라이버는 결과 집합의 열을 설명하기 위해 서버를 쿼리할 필요가 없습니다. 이 경우 **SQLDescribeCol** 서버 왕복을 발생 하지 않습니다. [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)및[SQLNumResultCols와](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)마찬가지로 준비되었지만 실행되지 않은 명령문에 **SQLDescribeCol을** 호출하면 서버 왕복이 생성됩니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문 일괄 처리에서 여러 결과 행 집합이 반환되는 경우 서수로 참조되는 열이 별도의 테이블에서 시작되거나 결과 집합의 완전히 다른 열을 참조할 수 있습니다. **SQLDescribeCol각** 집합에 대 한 호출 해야 합니다. 결과 집합이 변경되면 애플리케이션에서는 행 결과를 인출하기 전에 데이터 값을 다시 바인딩해야 합니다. 여러 결과 집합 반환을 처리하는 방법은 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 참조하십시오.  
  
 준비된 SQL 문의 일괄 처리에서 여러 개의 결과 집합이 생성될 경우 첫 번째 결과 집합에 대해서만 열 특성이 보고됩니다.  
  
 큰 값 데이터 형식의 경우 *DataTypePtr에서* 반환되는 값은 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_NVARCHAR. *ColumnSizePtr의* SQL_SS_LENGTH_UNLIMITED 값은 크기가 "무제한"임을 나타냅니다.  
  
 SQLDescribeCol을 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 통해 데이터베이스 엔진의 개선으로 인해 예상결과에 대한 보다 정확한 설명을 얻을 수 있습니다. 이러한 보다 정확한 결과는 이전 버전의 에서 SQLDescribeCol에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환한 값과 다를 수 있습니다. 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLDescribeCol 지원  
 날짜/시간 형식에 대해 반환되는 값은 다음과 같습니다.  
  
||*데이터 타이핑 Ptr*|*열크기Ptr*|*소수 자릿수Ptr*|  
|-|-------------------|---------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLDescribeCol 지원  
 **SQLDescribeCol은** 대규모 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLDescribeCol 함수](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
