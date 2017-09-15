---
title: "기본 데이터 형식을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e7333b711d828981a93c51b98b7e84fb62a7749b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-basic-data-types"></a>기본 데이터 형식 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] JDBC 기본 데이터 형식을 사용 하 여 변환 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식을 Java 프로그래밍 언어에 따라 그 반대의 인식할 수 있는 형식에 있습니다. JDBC 드라이버에서는 포함 된 JDBC 4.0 API에 대 한 지원의 **SQLXML** 데이터 형식 및 국가별 (유니코드) 데이터 형식이 같은 **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, 및 **NCLOB**합니다.  
  
## <a name="data-type-mappings"></a>데이터 형식 매핑  
 다음 표에서 기본 간의 기본 매핑을 나열 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], JDBC 및 Java 프로그래밍 언어 데이터 형식:  
  
|SQL Server 형식|JDBC 형식(java.sql.Types)|Java 언어 형식|  
|----------------------|-----------------------------------|-------------------------|  
|bigint|bigint|long|  
|binary|BINARY|byte[]|  
|bit|BIT|boolean|  
|char|CHAR|문자열|  
|date|DATE|java.sql.Date|  
|datetime|timestamp|java.sql.Timestamp|  
|datetime2|timestamp|java.sql.Timestamp|  
|datetimeoffset(2)|microsoft.sql.Types.DATETIMEOFFSET|microsoft.sql.DateTimeOffset|  
|decimal|DECIMAL|java.math.BigDecimal|  
|float|DOUBLE|double|  
|image|LONGVARBINARY|byte[]|  
|int|INTEGER|int|  
|money|DECIMAL|java.math.BigDecimal|  
|nchar|CHAR<br /><br /> NCHAR(Java SE 6.0)|문자열|  
|ntext|LONGVARCHAR<br /><br /> LONGNVARCHAR(Java SE 6.0)|문자열|  
|numeric|NUMERIC|java.math.BigDecimal|  
|nvarchar|VARCHAR<br /><br /> NVARCHAR(Java SE 6.0)|문자열|  
|nvarchar(max)|VARCHAR<br /><br /> NVARCHAR(Java SE 6.0)|문자열|  
|real|REAL|float|  
|smalldatetime|timestamp|java.sql.Timestamp|  
|smallint|SMALLINT|short|  
|smallmoney|DECIMAL|java.math.BigDecimal|  
|text|LONGVARCHAR|문자열|  
|time|TIME(1)|java.sql.Time(1)|  
|timestamp|BINARY|byte[]|  
|tinyint|TINYINT|short|  
|udt|VARBINARY|byte[]|  
|uniqueidentifier|CHAR|문자열|  
|varbinary|VARBINARY|byte[]|  
|varbinary(max)|VARBINARY|byte[]|  
|varchar|VARCHAR|문자열|  
|varchar(max)|VARCHAR|문자열|  
|xml|LONGVARCHAR<br /><br /> LONGNVARCHAR(Java SE 6.0)|문자열<br /><br /> SQLXML|  
  
 (시간 함께 java.sql.Time을 사용 하는 방법 1) [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 설정 해야 형식에는 **sendTimeAsDatetime** 연결 속성을 false입니다.  
  
 (의 값에 프로그래밍 방식으로 액세스할 수 2) **datetimeoffset** 와 [DateTimeOffset 클래스](../../connect/jdbc/reference/datetimeoffset-class.md)합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sqlvariant 데이터 형식은 현재 JDBC 드라이버에서 지원 되지 않습니다. sqlvariant 데이터 형식의 열이 포함된 테이블에서 쿼리를 사용하여 데이터를 검색하면 예외가 발생합니다.  
  
 다음 섹션에서는 JDBC 드라이버와 기본 데이터 형식을 사용하는 방법의 예를 보여 줍니다. Java 응용 프로그램의 기본 데이터 형식을 사용 하는 방법의 더 자세한 예제를 보려면 [기본 데이터 형식 샘플](../../connect/jdbc/basic-data-types-sample.md)합니다.  
  
## <a name="retrieving-data-as-a-string"></a>데이터를 문자열로 검색  
 강력한 형식의 데이터가 필요 하지 않은 경우 사용할 수 있습니다 또는 여 문자열로 봐야에 대 한 JDBC 기본 데이터 형식 중 하나에 매핑되는 데이터 원본에서 데이터를 검색할 수 있는 경우는 [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 다음과 같이 클래스:  
  
 [!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>데이터 형식별 데이터 검색  
 데이터 원본에서 데이터를 검색 해야 하는 경우를 검색 하는 데이터의 형식을 알고 get 중 하나를 사용\<유형 > 라고도 SQLServerResultSet의 메서드 클래스는 *getter 메서드*합니다. 이 사용은 열 이름이 나 열 인덱스를 사용할 수 있습니다\<유형 > 메서드를 다음과 같이 합니다.  
  
 [!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
>  GetUnicodeStream 및 눈금 메서드로 getBigDecimal는 사용 되지 않으며 JDBC 드라이버에서 지원 되지 않습니다.  
  
## <a name="updating-data-by-data-type"></a>데이터 형식별 데이터 업데이트  
 데이터 원본에 있는 필드의 값을 업데이트 해야 할 경우 업데이트 중 하나를 사용\<유형 > SQLServerResultSet 클래스의 메서드. 다음 예제에서는 [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) 메서드를 함께에서 사용 되는 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 데이터 원본의 데이터를 업데이트 하는 메서드:  
  
 [!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
>  JDBC 드라이버는 127자보다 긴 열 이름을 가진 SQL Server 열을 업데이트할 수 없습니다. 127자보다 긴 이름을 가진 열을 업데이트하려고 하면 예외가 발생합니다.  
  
## <a name="updating-data-by-parameterized-query"></a>매개 변수가 있는 쿼리로 데이터 업데이트  
 매개 변수가 있는 쿼리를 사용 하 여 데이터 원본에 데이터를 업데이트 해야 할 경우 집합 중 하나를 사용 하 여 데이터 형식의 매개 변수를 설정할 수 있습니다\<형식 >의 메서드는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 라고도 클래스는 *setter 메서드*합니다. 다음 예제에서는 [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) 메서드를 사용 하 여 매개 변수가 있는 쿼리를 한 다음은 [setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) 메서드는 하기전에매개변수의문자열값을설정하는[executeUpdate](../../connect/jdbc/reference/executeupdate-method.md) 메서드를 호출 합니다.  
  
 [!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
 매개 변수가 있는 쿼리에 대 한 자세한 내용은 참조 하십시오. [매개 변수가 있는 SQL 문을 사용 하 여](../../connect/jdbc/using-an-sql-statement-with-parameters.md)합니다.  
  
## <a name="passing-parameters-to-a-stored-procedure"></a>저장 프로시저에 매개 변수 전달  
 집합 중 하나를 사용 하 여 이름 또는 인덱스에 의해 매개 변수를 저장된 프로시저에 입력 된 매개 변수를 전달 해야 하는 경우 설정할 수 있습니다\<형식 >의 메서드는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스입니다. 다음 예제에서는 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 메서드 저장된 프로시저에 대 한 호출을 설정 하는 한 다음은 [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) 메서드 설정 하기 전에 호출에 대 한 매개 변수를 사용 하는 [ executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드를 호출 합니다.  
  
 [!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
>  이 예제에서는 저장 프로시저 실행 결과가 들어 있는 결과 집합을 반환합니다.  
  
 저장된 프로시저 및 입력된 매개 변수와 함께 JDBC 드라이버를 사용 하는 방법에 대 한 자세한 내용은 참조 [입력 매개 변수가 있는 저장 프로시저를 사용 하 여](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)합니다.  
  
## <a name="retrieving-parameters-from-a-stored-procedure"></a>저장 프로시저에서 매개 변수 검색  
 저장된 프로시저에서 다시 매개 변수를 검색 해야 할 경우 먼저 등록 해야는 out 매개 변수 이름별 또는 인덱스를 사용 하 여는 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 다음 할당 및 SQLServerCallableStatement 클래스의 메서드는 저장된 프로시저에 대 한 호출을 실행 한 후 out 매개 변수를 해당 변수에 반환 합니다. 저장된 프로시저에 대 한 호출을 설정 하려면 다음 예제에서는 prepareCall 메서드를 사용, out 매개 변수를 설정 하 고 registerOutParameter 메서드를 사용 하는 다음의 [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) 메서드 설정에 대 한 매개 변수를 사용 하는 executeQuery 메서드를 호출 하기 전에 호출 합니다. 사용 하 여 저장된 프로시저의 out 매개 변수에서 반환 되는 값이 검색은 [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) 메서드.  
  
 [!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
>  반환된 출력 매개 변수 외에도 저장 프로시저 실행 결과가 들어 있는 결과 집합이 반환될 수 있습니다.  
  
 저장된 프로시저 및 출력 매개 변수와 함께 JDBC 드라이버를 사용 하는 방법에 대 한 자세한 내용은 참조 [출력 매개 변수가 있는 저장 프로시저를 사용 하 여](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
