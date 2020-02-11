---
title: SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa74f982a5ff1894651d68f06689cba476a16452
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73787109"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL 문의 매개 변수를 설명 하기 위해 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] odbc 드라이버는 준비 된 ODBC 문 핸들 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 대해 SQLDescribeParam가 호출 될 때 SELECT 문을 작성 하 고 실행 합니다. 결과 집합의 메타데이터에 따라 준비된 문의 매개 변수 특징이 결정됩니다. SQLDescribeParam는 SQLExecute 또는 SQLExecDirect에서 반환할 수 있는 오류 코드를 반환할 수 있습니다.  
  
 로 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 시작 하는 데이터베이스 엔진의 향상 된 기능을 통해 SQLDescribeParam를 통해 예상 결과에 대 한 보다 정확한 설명을 얻을 수 있습니다. 이러한 더 정확한 결과는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 SQLDescribeParam에 의해 반환 된 값과 다를 수 있습니다. 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.  
  
 또한에서 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]새로 만들기, *ParameterSizePtr* 는 이제 [ODBC 사양](https://go.microsoft.com/fwlink/?LinkId=207044)에 정의 된 대로 해당 매개 변수 표식의 열 또는 식 크기 (문자 수)에 대 한 정의를 사용 하 여 정렬 하는 값을 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 Native Client에서 *ParameterSizePtr* 은 형식에 대 한 **SQL_DESC_OCTET_LENGTH** 의 해당 값 또는 형식에 대해 SQLBindParameter에 제공 된 관련이 없는 열 크기 값 (예:**SQL_INTEGER**) 일 수 있습니다.  
  
 드라이버는 다음과 같은 상황에서 SQLDescribeParam 호출을 지원 하지 않습니다.  
  
-   SQLExecDirect 이후 FROM 절 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이 포함 된 UPDATE 또는 DELETE 문에 대해  
  
-   HAVING 절에 매개 변수를 포함하거나 SUM 함수 결과와 비교되는 ODBC 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우  
  
-   매개 변수가 포함된 하위 쿼리를 사용하는 ODBC 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우  
  
-   정량화된 조건자 또는 비교 like의 두 식에 모두 매개 변수 표식이 포함된 ODBC SQL 문의 경우  
  
-   매개 변수 중 하나가 함수에 대한 매개 변수인 쿼리의 경우  
  
-   명령에 주석 (/* \*/)이 있는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 일괄 처리를 처리 하는 경우 드라이버는 일괄 처리의 첫 번째 문 다음에 있는 문의 매개 변수 표식에 대해 SQLDescribeParam를 호출 하는 것도 지원 하지 않습니다.  
  
 준비 된 저장 프로시저의 매개 변수를 설명할 때 SQLDescribeParam는 시스템 저장 프로시저 [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) 를 사용 하 여 매개 변수 특징을 검색 합니다. sp_sproc_columns는 현재 사용자 데이터베이스 내의 저장 프로시저에 대 한 데이터를 보고할 수 있습니다. 정규화 된 저장 프로시저 이름을 준비 하면 SQLDescribeParam에서 데이터베이스를 실행할 수 있습니다. 예를 들어 다음과 같은 시스템 저장 프로시저 [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 을 준비 하 고 모든 데이터베이스에서 실행할 수 있습니다.  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 준비가 완료 된 후 SQLDescribeParam를 실행 하면 데이터베이스에 연결 되었지만 **master**에는 빈 행 집합이 반환 됩니다. 다음과 같이 준비 된 동일한 호출로 인해 현재 사용자 데이터베이스에 관계 없이 SQLDescribeParam이 성공 합니다.  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 대량 값 데이터 형식의 경우 *DataTypePtr* 에서 반환 되는 값은 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_NVARCHAR입니다. 큰 값 데이터 형식 매개 변수의 크기가 "제한 없음" 임을 나타내려면 Native Client ODBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *ParameterSizePtr* 를 0으로 설정 합니다. 표준 **varchar** 매개 변수에 대 한 실제 크기 값이 반환 됩니다.  
  
> [!NOTE]  
>  매개 변수가 이미 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR 매개 변수의 최대 크기와 바인딩되어 있으면 "제한 없음"이 아니라 매개 변수의 바인딩된 크기가 반환됩니다.  
  
 "제한 없음" 크기 입력 매개 변수를 바인딩하려면 실행 시 데이터를 사용해야 합니다. "무제한" 크기의 출력 매개 변수를 바인딩할 수 없습니다 (예: SQLGetData는 결과 집합에 대 한 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 와 마찬가지로 출력 매개 변수에서 데이터를 스트리밍하는 방법은 없음).  
  
 출력 매개 변수의 경우 버퍼를 바인딩해야 하며, 값이 너무 크면 버퍼가 채워지고 SQL_SUCCESS_WITH_INFO 메시지가 "문자열 데이터의 오른쪽이 잘렸습니다."라는 경고와 함께 반환됩니다. 잘린 데이터는 삭제됩니다.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam와 테이블 반환 매개 변수  
 응용 프로그램은 SQLDescribeParam를 사용 하 여 준비 된 문에 대 한 테이블 반환 매개 변수 정보를 검색할 수 있습니다. 자세한 내용은 [준비 된 문의 테이블 반환 매개 변수 메타 데이터](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)를 참조 하세요.  
  
 일반적으로 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLDescribeParam 지원  
 날짜/시간 형식에 대해 반환되는 값은 다음과 같습니다.  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 향상 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)을 참조 하세요.  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLDescribeParam 지원  
 **SQLDescribeParam** 는 많은 CLR udt (사용자 정의 형식)를 지원 합니다. 자세한 내용은 [ODBC&#41;&#40;LARGE CLR 사용자 정의 형식 ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLDescribeParam 함수](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
