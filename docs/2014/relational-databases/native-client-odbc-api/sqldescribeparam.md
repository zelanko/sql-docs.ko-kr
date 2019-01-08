---
title: SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d52d68cc0cd31e9dbb3da25c46901e126252607
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359495"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
  SQL 문의 매개 변수를 설명 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 작성 하 고 실행을 [!INCLUDE[tsql](../../includes/tsql-md.md)] SQLDescribeParam 준비 된 ODBC 문 핸들에서 호출 되 면 SELECT 문의 합니다. 결과 집합의 메타데이터에 따라 준비된 문의 매개 변수 특징이 결정됩니다. SQLDescribeParam은 SQLExecute 또는 SQLExecDirect를 반환할 수 있는 오류 코드를 반환할 수 있습니다.  
  
 부터 데이터베이스 엔진의 개선 사항 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SQLDescribeParam 예상된 결과 대 한 보다 정확한 설명의 얻을를 허용 합니다. 이전 버전의 SQLDescribeParam 반환한 값에서 다를 수 있습니다 이러한 보다 정확한 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 자세한 내용은 [메타데이터 검색](../native-client/features/metadata-discovery.md)을 참조하세요.  
  
 새로운 기능 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]하십시오 *ParameterSizePtr* 이제에 정의 된 열 또는 식의 해당 매개 변수 표식 문자 크기에 대 한 정의 사용 하 여 정렬 되는 값을 반환 합니다 [ODBC 사양](https://go.microsoft.com/fwlink/?LinkId=207044)합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client *ParameterSizePtr* 의 해당 값 수 `SQL_DESC_OCTET_LENGTH` 형식 또는 값 형식에 대 한 SQLBindParameter에 제공 된 관련이 없는 열 크기 값에 대 한 무시 해야 하는 중 (`SQL_INTEGER`예를 들어).  
  
 드라이버는 다음과 같은 상황에서 호출 SQLDescribeParam를 지원 하지 않습니다.  
  
-   에 대 한 SQLExecDirect 후 [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE 또는 DELETE 문의 FROM 절을 포함 합니다.  
  
-   HAVING 절에 매개 변수를 포함하거나 SUM 함수 결과와 비교되는 ODBC 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우  
  
-   매개 변수가 포함된 하위 쿼리를 사용하는 ODBC 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 경우  
  
-   정량화된 조건자 또는 비교 like의 두 식에 모두 매개 변수 표식이 포함된 ODBC SQL 문의 경우  
  
-   매개 변수 중 하나가 함수에 대한 매개 변수인 쿼리의 경우  
  
-   경우 주석 (/ * \*/)에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령입니다.  
  
 일괄 처리 하는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 드라이버 또한 없습니다 일괄 처리의 첫 번째 문 다음에 나오는 문의 매개 변수 표식에 대 한 SQLDescribeParam를 호출 합니다.  
  
 SQLDescribeParam 시스템 저장 프로시저를 사용 하 여 준비 된 저장된 프로시저의 매개 변수를 설명 하는, 하는 경우 [sp_sproc_columns](/sql/relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql) 에 매개 변수 특징을 검색 합니다. sp_sproc_columns 현재 사용자 데이터베이스 내의 저장된 프로시저에 대 한 데이터를 보고할 수 있습니다. 정규화 된 저장된 프로시저 이름을 준비 SQLDescribeParam을 데이터베이스에서 실행할 수 있습니다. 예를 들어, 시스템 저장 프로시저 [sp_who](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) 준비 하 고 모든 데이터베이스에서 실행할 수 있습니다.  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 준비에 성공한 빈 행 집합이 데이터베이스에 연결 하는 경우 반환 된 후 SQLDescribeParam를 실행 하지만 `master`합니다. 다음과 같이 준비 하는 동일한 호출에서 현재 사용자 데이터베이스에 관계 없이 되려면 SQLDescribeParam을 발생 시킵니다.  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 큰 값 데이터 형식에서 값 반환 *DataTypePtr* 은 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_NVARCHAR입니다. 큰 값 데이터 형식 매개 변수의 크기가 "제한" 임을 나타내려면 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 집합 *ParameterSizePtr* 0입니다. 표준 `varchar` 매개 변수에 대해서는 실제 크기 값이 반환됩니다.  
  
> [!NOTE]  
>  매개 변수가 이미 SQL_VARCHAR, SQL_VARBINARY 또는 SQL_WVARCHAR 매개 변수의 최대 크기와 바인딩되어 있으면 "제한 없음"이 아니라 매개 변수의 바인딩된 크기가 반환됩니다.  
  
 "제한 없음" 크기 입력 매개 변수를 바인딩하려면 실행 시 데이터를 사용해야 합니다. "제한 없음된" 크기 출력 매개 변수를 바인딩할 수 없으면 (같은 출력 매개 변수에서 데이터 스트리밍에 대 한 메서드가 없는 [SQLGetData](sqlgetdata.md) 결과 집합).  
  
 출력 매개 변수의 경우 버퍼를 바인딩해야 하며, 값이 너무 크면 버퍼가 채워지고 SQL_SUCCESS_WITH_INFO 메시지가 "문자열 데이터의 오른쪽이 잘렸습니다."라는 경고와 함께 반환됩니다. 잘린 데이터는 삭제됩니다.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam와 테이블 반환 매개 변수  
 응용 프로그램 SQLDescribeParam 사용 하 여 준비 된 문에 대 한 테이블 반환 매개 변수 정보를 검색할 수 있습니다. 자세한 내용은 [Prepared 문 테이블 반환 매개 변수 메타 데이터](../native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)입니다.  
  
 일반적으로 참조 한 테이블 반환 매개 변수에 대 한 자세한 내용은 [테이블 반환 매개 변수 &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)합니다.  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>향상된 날짜 및 시간 기능에 대한 SQLDescribeParam 지원  
 날짜/시간 형식에 대해 반환되는 값은 다음과 같습니다.  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|Time|SQL_SS_TIME2|8, 10..16|0..7|  
|Datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 자세한 내용은 [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)합니다.  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>큰 CLR UDT에 대한 SQLDescribeParam 지원  
 `SQLDescribeParam`는 큰 CLR UDT(사용자 정의 형식)를 지원합니다. 자세한 내용은 [Large CLR User-Defined 형식 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLDescribeParam 함수](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
