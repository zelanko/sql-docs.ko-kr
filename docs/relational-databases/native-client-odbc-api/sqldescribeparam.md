---
title: SQLDescribeParam | 마이크로 소프트 문서
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efe1fdccbef4f5c4a393083f6eb81efee759be5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302590"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL 문의 매개 변수를 설명하기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 위해 네이티브 클라이언트 ODBC 드라이버는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 준비된 ODBC 문 핸들에서 SQLDescribeParam이 호출될 때 SELECT 문을 빌드하고 실행합니다. 결과 집합의 메타데이터에 따라 준비된 문의 매개 변수 특징이 결정됩니다. SQLDescribeParam 은 SQLExecute 또는 SQLExecDirect가 반환할 수 있는 오류 코드를 반환할 수 있습니다.  
  
 SQLDescribeParam을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 데이터베이스 엔진의 개선으로 인해 예상결과에 대한 보다 정확한 설명을 얻을 수 있습니다. 이러한 보다 정확한 결과는 이전 버전의 에서 SQLDescribeParam에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환된 값과 다를 수 있습니다. 자세한 내용은 [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)을 참조하세요.  
  
 또한 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]새로운 에서 " *ParameterSizePtr* 이제 [ODBC 사양에](https://go.microsoft.com/fwlink/?LinkId=207044)정의된 대로 해당 매개 변수 마커의 열 또는 식의 크기, 문자, 열 또는 식에 대한 정의와 정렬하는 값을 반환합니다. 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 네이티브 클라이언트에서 *ParameterSizePtr형식에* 대한 **SQL_DESC_OCTET_LENGTH** 해당 값또는 형식에 대해 SQLBindParameter에 제공된 관련없는 열 크기 값일 수 있으며, 그 값은 무시해야 SQL_INTEGER.SQL_INTEGER.)**SQL_INTEGER**  
  
 드라이버는 다음과 같은 상황에서 SQLDescribeParam 호출을 지원하지 않습니다.  
  
-   FROM 절을 포함하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모든 업데이트 또는 DELETE 문에 대한 SQLExecDirect 후.  
  
-   HAVING 절에 매개 변수를 포함하거나 SUM 함수 결과와 비교되는 ODBC 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우  
  
-   매개 변수가 포함된 하위 쿼리를 사용하는 ODBC 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우  
  
-   정량화된 조건자 또는 비교 like의 두 식에 모두 매개 변수 표식이 포함된 ODBC SQL 문의 경우  
  
-   매개 변수 중 하나가 함수에 대한 매개 변수인 쿼리의 경우  
  
-   명령에 주석 (/* \*/)이있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 경우.  
  
 명령문의 일괄 [!INCLUDE[tsql](../../includes/tsql-md.md)] 처리를 처리할 때 드라이버는 일괄 처리의 첫 번째 문 다음 문에서 매개 변수 마커에 대해 SQLDescribeParam 호출도 지원하지 않습니다.  
  
 준비된 저장 프로시저의 매개 변수를 설명할 때 SQLDescribeParam은 시스템 저장 프로시저 [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) 사용하여 매개 변수 특성을 검색합니다. sp_sproc_columns 현재 사용자 데이터베이스 내의 저장된 프로시저에 대한 데이터를 보고할 수 있습니다. 정규화된 저장 프로시저 이름을 준비하면 SQLDescribeParam이 데이터베이스 간에 실행할 수 있습니다. 예를 들어 시스템 저장 프로시저 [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 모든 데이터베이스에서 다음과 같이 준비하고 실행할 수 있습니다.  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 성공적인 준비 후 SQLDescribeParam을 실행하면 데이터베이스하지만 **마스터에**연결될 때 빈 행 집합이 반환됩니다. 다음과 같이 준비된 동일한 호출은 현재 사용자 데이터베이스에 관계없이 SQLDescribeParam이 성공하게 합니다.  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 큰 값 데이터 형식의 경우 *DataTypePtr에서* 반환되는 값은 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_NVARCHAR. 큰 값 데이터 형식 매개 변수의 크기가 "무제한"임을 나타내기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 *ParameterSizePtr을* 0으로 설정합니다. 표준 **varchar** 매개 변수에 대해 실제 크기 값이 반환됩니다.  
  
> [!NOTE]  
>  매개 변수가 이미 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR 매개 변수의 최대 크기와 바인딩되어 있으면 "제한 없음"이 아니라 매개 변수의 바인딩된 크기가 반환됩니다.  
  
 "제한 없음" 크기 입력 매개 변수를 바인딩하려면 실행 시 데이터를 사용해야 합니다. "무제한" 크기 출력 매개 변수를 바인딩할 수 없습니다(결과 집합에 대해 [SQLGetData와](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 같이 출력 매개 변수에서 데이터를 스트리밍하는 방법은 없습니다).  
  
 출력 매개 변수의 경우 버퍼를 바인딩해야 하며, 값이 너무 크면 버퍼가 채워지고 SQL_SUCCESS_WITH_INFO 메시지가 "문자열 데이터의 오른쪽이 잘렸습니다."라는 경고와 함께 반환됩니다. 잘린 데이터는 삭제됩니다.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam와 테이블 반환 매개 변수  
 응용 프로그램은 SQLDescribeParam을 사용 하 여 준비 된 문에 대 한 테이블 값 매개 변수 정보를 검색할 수 있습니다. 자세한 내용은 [준비된 명령문에 대한 테이블 값 매개 변수 메타데이터를](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)참조하십시오.  
  
 일반적으로 테이블 값 매개 변수에 대한 자세한 내용은 ODBC&#41;&#40;[테이블 값 매개 변수를 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)참조하십시오.  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLDescribeParam 지원  
 날짜/시간 형식에 대해 반환되는 값은 다음과 같습니다.  
  
||*데이터 타이핑 Ptr*|*매개 변수크기Ptr*|*소수 자릿수Ptr*|  
|-|-------------------|------------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 자세한 내용은 [ODBC&#41;&#40;날짜 및 시간 개선 을 ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)참조하십시오.  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLDescribeParam 지원  
 **SQLDescribeParam은** 큰 CLR 사용자 정의 형식(UDT)을 지원합니다. 자세한 내용은 [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQLDescribeParam 함수](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
