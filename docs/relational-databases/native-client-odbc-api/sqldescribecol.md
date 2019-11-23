---
title: SQLDescribeCol | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 54760d209b6cb0a646b7eb68d232e46f5ccaa7b6
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787252"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  실행 된 문의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 결과 집합의 열을 설명 하기 위해 서버를 쿼리할 필요가 없습니다. 이 경우 **SQLDescribeCol** 는 서버 왕복을 발생 시 키 지 않습니다. [Sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)및[Sqlnumresultcols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md)와 같이 준비 되었지만 실행 되지 않은 문에 대해 **SQLDescribeCol** 를 호출 하면 서버 왕복이 생성 됩니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문 일괄 처리에서 여러 결과 행 집합이 반환되는 경우 서수로 참조되는 열이 별도의 테이블에서 시작되거나 결과 집합의 완전히 다른 열을 참조할 수 있습니다. 각 집합에 대해 **SQLDescribeCol** 를 호출 해야 합니다. 결과 집합이 변경되면 애플리케이션에서는 행 결과를 인출하기 전에 데이터 값을 다시 바인딩해야 합니다. 여러 결과 집합 반환을 처리하는 방법은 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)를 참조하십시오.  
  
 준비된 SQL 문의 일괄 처리에서 여러 개의 결과 집합이 생성될 경우 첫 번째 결과 집합에 대해서만 열 특성이 보고됩니다.  
  
 대량 값 데이터 형식의 경우 *DataTypePtr* 에서 반환 되는 값은 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_NVARCHAR입니다. *ColumnSizePtr* 의 SQL_SS_LENGTH_UNLIMITED 값은 크기가 "제한 없음" 임을 나타냅니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 시작 하는 데이터베이스 엔진의 향상 된 기능으로 인해 SQLDescribeCol에서 예상 결과에 대 한 보다 정확한 설명을 얻을 수 있습니다. 이러한 보다 정확한 결과는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQLDescribeCol에서 반환 된 값과 다를 수 있습니다. 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLDescribeCol 지원  
 날짜/시간 형식에 대해 반환되는 값은 다음과 같습니다.  
  
||*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|---------------------|------------------------|  
|datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|Time|SQL_SS_TIME2|8, 10..16|0..7|  
|Datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|Datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 자세한 내용은 [ODBC&#41;의 날짜 및 시간 기능 향상 &#40;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLDescribeCol 지원  
 **SQLDescribeCol** 는 많은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC &#40;&#41;의 Large CLR 사용자 정의 형식](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLDescribeCol 함수](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
