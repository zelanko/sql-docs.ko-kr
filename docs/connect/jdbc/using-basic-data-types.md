---
title: 기본 데이터 형식 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4608bd48607244c50e7d6fd03b74919448fa074
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924062"
---
# <a name="using-basic-data-types"></a>기본 데이터 형식 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 JDBC 기본 데이터 형식을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 Java 프로그래밍 언어가 인식할 수 있는 형식으로 변환하며 그 반대 과정도 수행합니다. JDBC 드라이버는 JDBC 4.0 API를 지원하며, 여기에는 **SQLXML** 데이터 형식, 그리고 국가별(유니코드) 데이터 형식(예: **NCHAR**, **NVARCHAR**, **LONGNVARCHAR**, **NCLOB**)이 포함됩니다.  
  
## <a name="data-type-mappings"></a>데이터 형식 매핑

다음 표에서는 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], JDBC 및 Java 프로그래밍 언어 데이터 형식 간의 기본 매핑을 나열합니다.  
  
| SQL Server 형식   | JDBC 형식(java.sql.Types)                        | Java 언어 형식          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| bigint             | bigint                                             | long                         |
| binary             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | boolean                      |
| char               | CHAR                                               | String                       |
| date               | DATE                                               | java.sql.Date                |
| Datetime           | timestamp                                          | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset(2) | microsoft.sql.Types.DATETIMEOFFSET                 | microsoft.sql.DateTimeOffset |
| decimal            | DECIMAL                                            | java.math.BigDecimal         |
| float              | DOUBLE                                             | double                       |
| 이미지              | LONGVARBINARY                                      | byte[]                       |
| int                | INTEGER                                            | int                          |
| money              | DECIMAL                                            | java.math.BigDecimal         |
| nchar              | CHAR<br /><br /> NCHAR(Java SE 6.0)               | String                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR(Java SE 6.0) | String                       |
| numeric            | NUMERIC                                            | java.math.BigDecimal         |
| nvarchar           | VARCHAR<br /><br /> NVARCHAR(Java SE 6.0)         | String                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR(Java SE 6.0)         | String                       |
| real               | real                                               | float                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| smallint           | SMALLINT                                           | short                        |
| smallmoney         | DECIMAL                                            | java.math.BigDecimal         |
| text               | LONGVARCHAR                                        | String                       |
| time               | TIME(1)                                           | java.sql.Time(1)            |
| timestamp          | BINARY                                             | byte[]                       |
| tinyint            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| uniqueidentifier   | CHAR                                               | String                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | String                       |
| varchar(max)       | VARCHAR                                            | String                       |
| Xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR(Java SE 6.0) | String<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Object                       |
| geometry           | VARBINARY                                          | byte[]                       |
| geography          | VARBINARY                                          | byte[]                       |
  
(1) time [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식과 함께 java.sql.Time을 사용하려면 **sendTimeAsDatetime** 연결 속성을 false로 설정해야 합니다.  
  
(2) **DateTimeOffset 클래스**를 사용하여 [datetimeoffset](../../connect/jdbc/reference/datetimeoffset-class.md) 값에 프로그래밍 방식으로 액세스할 수 있습니다.  
  
다음 섹션에서는 JDBC 드라이버와 기본 데이터 형식을 사용하는 방법의 예를 보여 줍니다. Java 애플리케이션에서 기본 데이터 형식을 사용하는 방법에 대한 자세한 예는 [기본 데이터 형식 샘플](../../connect/jdbc/basic-data-types-sample.md)을 참조하세요.  
  
## <a name="retrieving-data-as-a-string"></a>데이터를 문자열로 검색

JDBC 기본 데이터 형식에 매핑되는 데이터 원본에서 데이터를 검색하여 문자열로 봐야 하거나 강력한 형식의 데이터가 필요하지 않은 경우 다음과 같이 [SQLServerResultSet](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) 클래스의 [getString](../../connect/jdbc/reference/sqlserverresultset-class.md) 메서드를 사용합니다.  
  
[!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>데이터 형식별 데이터 검색

데이터 원본에서 데이터를 검색해야 하고 검색할 데이터 형식을 알고 있는 경우 SQLServerResultSet 클래스의 get\<Type> 메서드(*getter 메서드*라고도 함) 중 하나를 사용합니다. get\<Type> 메서드는 다음과 같이 열 이름 또는 열 인덱스와 함께 사용할 수 있습니다.  
  
[!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> getUnicodeStream과 getBigDecimal(크기 조정 메서드 포함)은 사용하지 않으므로 JDBC 드라이버에서 지원하지 않습니다.

## <a name="updating-data-by-data-type"></a>데이터 형식별 데이터 업데이트

데이터 원본의 필드 값을 업데이트해야 하는 경우 SQLServerResultSet 클래스의 update\<Type> 메서드 중 하나를 사용합니다. 다음 예제에서는 [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) 메서드와 [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 메서드를 함께 사용하여 데이터 원본의 데이터를 업데이트합니다.  
  
[!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> JDBC 드라이버는 127자보다 긴 열 이름을 가진 SQL Server 열을 업데이트할 수 없습니다. 127자보다 긴 이름을 가진 열을 업데이트하려고 하면 예외가 발생합니다.  
  
## <a name="updating-data-by-parameterized-query"></a>매개 변수가 있는 쿼리로 데이터 업데이트

매개 변수가 있는 쿼리를 사용하여 데이터 원본의 데이터를 업데이트해야 하는 경우 \<SQLServerPreparedStatement[ 클래스의 set](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)Type> 메서드*setter 메서드*라고도 함 중 하나를 사용하여 매개 변수의 데이터 형식을 설정합니다. 다음 예제에서는 [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) 메서드를 사용하여 매개 변수가 있는 쿼리를 미리 컴파일한 다음, [setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) 메서드로 매개 변수의 문자열 값을 설정한 후 [executeUpdate](../../connect/jdbc/reference/executeupdate-method.md) 메서드를 호출합니다.  
  
[!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
매개 변수가 있는 쿼리에 대한 자세한 내용은 [매개 변수가 있는 SQL 문 사용](../../connect/jdbc/using-an-sql-statement-with-parameters.md)을 참조하세요.  

## <a name="passing-parameters-to-a-stored-procedure"></a>저장 프로시저에 매개 변수 전달

형식화된 매개 변수를 저장 프로시저에 전달하려면 \<SQLServerCallableStatement[ 클래스의 ](../../connect/jdbc/reference/sqlservercallablestatement-class.md)Type> 메서드 중 하나를 사용하여 인덱스 또는 이름으로 매개 변수를 설정합니다. 다음 예제에서는 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 메서드를 사용하여 저장 프로시저 호출을 설정한 다음, [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) 메서드로 호출에 필요한 매개 변수를 설정한 후 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드를 호출합니다.  
  
[!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> 이 예제에서는 저장 프로시저 실행 결과가 들어 있는 결과 집합을 반환합니다.

저장 프로시저 및 입력 매개 변수와 함께 JDBC 드라이버를 사용하는 방법은 [입력 매개 변수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)을 참조하십시오.  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>저장 프로시저에서 매개 변수 검색

저장 프로시저에서 다시 매개 변수를 검색하려면 먼저 SQLServerCallableStatement 클래스의 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 메서드를 사용하여 이름 또는 인덱스로 출력 매개 변수를 등록한 다음, 저장 프로시저 호출을 실행한 후 반환된 출력 매개 변수를 해당 변수에 지정해야 합니다. 다음 예제에서는 prepareCall 메서드를 사용하여 저장 프로시저 호출을 설정하고 registerOutParameter 메서드로 출력 매개 변수를 설정한 다음, [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) 메서드를 사용하여 호출에 필요한 매개 변수를 설정한 후 executeQuery 메서드를 호출합니다. 저장 프로시저의 출력 매개 변수가 반환하는 값은 [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) 메서드를 사용하여 검색합니다.  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> 반환된 출력 매개 변수 외에도 저장 프로시저 실행 결과가 들어 있는 결과 집합이 반환될 수 있습니다.  
  
저장 프로시저 및 출력 매개 변수와 함께 JDBC 드라이버를 사용하는 방법은 [ 매개 변수가 있는 저장 프로시저 사용](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)을 참조하십시오.  

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
