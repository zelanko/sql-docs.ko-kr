---
title: 고급 데이터 형식을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddef588be6f7e15c8a3f7f8e981a44cfcb5c9076
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736824"
---
# <a name="using-advanced-data-types"></a>고급 데이터 형식 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 JDBC 고급 데이터 형식을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 Java 프로그래밍 언어가 인식할 수 있는 형식으로 변환합니다.  
  
## <a name="remarks"></a>Remarks

다음 표에서는 고급 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], JDBC 및 Java 프로그래밍 언어 데이터 형식 간의 기본 매핑을 나열합니다.  
  
|SQL Server 형식|JDBC 형식(java.sql.Types)|Java 언어 형식|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|byte[]\(기본값), Blob, InputStream, String|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String(기본값), Clob, InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR(Java SE 6.0)|String(기본값), Clob, NClob|  
|xml|LONGVARCHAR<br /><br /> SQLXML|String(기본값), InputStream, Clob, byte[],Blob, SQLXML|  
|Udt<sup>1</sup>|VARBINARY|String(기본값), byte[], InputStream|  
|sqlvariant|SQLVARIANT|Object|  
|geometry<br /><br /> geography|VARBINARY|byte[]|  


<sup>1</sup> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 이진 데이터 형식으로 CLR UDT 전송 및 검색을 지원하지만 CLR 메타데이터의 조작은 지원하지 않습니다.  
  
다음 섹션에서는 JDBC 드라이버와 고급 데이터 형식을 사용하는 방법의 예를 보여 줍니다.  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>BLOB, CLOB 및 NCLOB 데이터 형식

JDBC 드라이버는 java.sql.Blob, java.sql.Clob 및 java.sql.NClob 인터페이스의 모든 메서드를 구현합니다.  
  
> [!NOTE]  
> CLOB 값은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상의 큰 값 데이터 형식과 함께 사용할 수 있습니다. 특히 CLOB 형식은 사용할 수 있습니다는 **varchar (max)** 하 고 **nvarchar (max)** 데이터 형식을 사용 하 여 BLOB 형식을 사용할 수 있습니다 **varbinary (max)** 고 **이미지**  데이터 형식 및 NCLOB 형식은 사용 될 수 있습니다 **ntext** 하 고 **nvarchar (max)** 합니다.  

## <a name="large-value-data-types"></a>큰 값 데이터 형식

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이전 버전에서는 큰 값 데이터 형식을 사용할 때 특별한 처리가 필요했습니다. 큰 값 데이터 형식은 최대 행 크기가 8KB를 초과하는 데이터 형식입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **varchar**, **nvarchar** 및 **varbinary** 데이터 형식에 대해 max 지정자를 제공하여 값을 2^31바이트로 스토리지할 수 있도록 합니다. 테이블 열과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변수에서 **varchar(max)**, **nvarchar(max)** 또는 **varbinary(max)** 데이터 형식을 지정할 수 있습니다.  

큰 값 형식을 사용하는 주요 시나리오는 큰 값 형식을 데이터베이스에서 검색하거나 데이터베이스에 추가하는 것입니다. 다음 섹션에서는 이러한 태스크를 수행하는 다양한 접근 방식에 대해 설명합니다.  

### <a name="retrieving-large-value-types-from-a-database"></a>데이터베이스에서 큰 값 형식 검색

**varchar(max)** 데이터 형식과 같이 이진이 아닌 큰 값 데이터 형식을 데이터베이스에서 검색할 때 사용할 수 있는 한 가지 방법은 해당 데이터를 문자 스트림으로 읽는 것입니다. 다음 예제에서는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드를 사용하여 데이터베이스에서 데이터를 검색하고 이를 결과 집합으로 반환합니다. 그런 다음 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스의 [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 메서드를 사용하여 결과 집합에서 큰 값 데이터를 읽습니다.  

```java
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```

> [!NOTE]
> 에 대 한 이와 동일한 방법을 사용할 수도 있습니다는 **텍스트**를 **ntext**, 및 **nvarchar (max)** 데이터 형식입니다.  

**varbinary(max)** 데이터 형식과 같은 이진 큰 값 데이터 형식을 데이터베이스에서 검색할 때 사용할 수 있는 방법에는 몇 가지가 있습니다. 가장 효율적인 방법은 다음과 같이 데이터를 이진 스트림으로 읽는 것입니다.  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```

또한 다음과 같이 [getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) 메서드를 사용하여 데이터를 바이트 배열로 읽을 수도 있습니다.  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```

> [!NOTE]  
> 뿐만 아니라 데이터를 BLOB로 읽는 방법도 있습니다. 그러나 이 방법은 앞의 두 방법에 비해 효율이 떨어집니다.  

### <a name="adding-large-value-types-to-a-database"></a>데이터베이스에 큰 값 데이터 형식 추가

JDBC 드라이버로 큰 데이터를 업로드할 때 메모리 크기의 작업인 경우 원활하게 수행되지만 메모리 크기를 초과하는 작업의 경우에는 스트리밍이 최선의 수단입니다. 그러나 큰 데이터를 업로드하는 가장 효율적인 방법은 스트림 인터페이스를 사용하는 것입니다.  

다음과 같이 문자열 또는 바이트를 사용하는 것도 한 가지 방법입니다.  

```java
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```

> [!NOTE]  
> 에 저장 된 값에 대 한이 접근 방식을 사용할 수도 있습니다 **텍스트**하십시오 **ntext**, 및 **nvarchar (max)** 열입니다.  

서버에 이미지 라이브러리가 있는데 전체 이진 이미지 파일을 **varbinary(max)** 열에 업로드해야 하는 경우 JDBC 드라이버를 사용하는 가장 효율적인 방법은 다음과 같이 스트림을 직접 사용하는 것입니다.  

```java
try (PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)")) { 
  File inputFile = new File("CLOBFile20mb.jpg");  
  try (FileInputStream inStream = new FileInputStream(inputFile)) {
    int id = 1;  
    pstmt.setInt(1,id);  
    pstmt.setBinaryStream(2, inStream);  
    pstmt.executeUpdate();
  }
}
```

> [!NOTE]  
> CLOB 또는 BLOB 메서드 중 하나를 사용하는 방법은 큰 데이터를 업로드하는 데는 적합하지 않습니다.  

### <a name="modifying-large-value-types-in-a-database"></a>데이터베이스에서 큰 값 데이터 형식 수정

대개의 경우 데이터베이스의 큰 값을 업데이트하거나 수정할 때 권장되는 방법은 `UPDATE`, `WRITE` 및 `SUBSTRING`과 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 사용하여 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스를 통해 매개 변수를 전달하는 것입니다.  

보관된 HTML 파일처럼 큰 텍스트 파일에서 단어의 인스턴스를 바꾸려면 다음과 같이 Clob 개체를 사용합니다.  

```java
String SQL = "SELECT * FROM test1;";  
try (Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE)
     ResultSet rs = stmt.executeQuery(SQL)) {
  rs.next();

  Clob clob = rs.getClob(2);  
  long pos = clob.position("dog", 1);  
  clob.setString(pos, "cat");  
  rs.updateClob(2, clob);  
  rs.updateRow();  
}
```

또한 서버에서 모든 작업을 수행하고 준비된 UPDATE 문에 매개 변수만 전달하는 방법도 있습니다.  

큰 값 형식에 대한 자세한 내용은 SQL Server 온라인 설명서의 "큰 값 형식 사용"을 참조하십시오.  

## <a name="xml-data-type"></a>XML 데이터 형식

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 XML 문서와 조각을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장할 수 있도록 하는 **xml** 데이터 형식을 제공합니다. **xml** 데이터 형식은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 제공 데이터 형식이며 **int** 및 **varchar**와 같은 다른 기본 제공 형식과 비슷합니다. 다른 기본 제공 유형과 마찬가지로 변수 유형, 매개 변수 유형, 함수 반환 형식 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST 및 CONVERT 함수로 테이블을 만들 때 **xml** 데이터 형식을 열 유형으로 사용할 수 있습니다.  
  
JDBC 드라이버에서 **xml** 데이터 형식은 문자열, 바이트 배열, 스트림, CLOB, BLOB 또는 SQLXML 개체로 매핑될 수 있습니다. 기본값은 문자열입니다. JDBC 드라이버 버전 2.0 이상에서는 SQLXML 인터페이스가 추가된 JDBC 4.0 API가 지원됩니다. SQLXML 인터페이스는 XML 데이터에 대한 상호 작용 및 조작을 수행하는 메서드를 정의합니다. **SQLXML** 데이터 형식에 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xml** 데이터 형식입니다. **SQLXML** Java 데이터 형식으로 관계형 데이터베이스에서 XML 데이터를 읽고 쓰는 방법은 [XML 데이터 지원](../../connect/jdbc/supporting-xml-data.md)을 참조하세요.  
  
JDBC 드라이버의 **xml** 데이터 형식 구현에서는 다음을 지원합니다.  
  
- 가장 일반적인 프로그래밍 시나리오에서 표준 Java UTF-16 문자열로 XML에 액세스합니다.  
  
- UTF-8 및 다른 8비트 인코딩 XML 입력을 지원합니다.  
  
- 다른 XML 프로세서 및 디스크 파일과의 교환을 위해 UTF-16으로 인코딩된 경우 선행 BOM이 있는 바이트 배열로 XML에 액세스합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 UTF-16으로 인코딩된 XML에 선행 BOM을 사용해야 합니다. 응용 프로그램은 XML 매개 변수 값이 바이트 배열로 제공되는 경우에 이를 제공해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 항상 BOM이나 포함된 인코딩 선언이 없는 UTF-16 문자열로 XML 값을 출력합니다. XML 값을 byte[], BinaryStream 또는 BLOB로 검색하면 UTF-16 BOM이 값 앞에 붙습니다.  
  
**xml** 데이터 형식에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 “xml 데이터 형식”을 참조하세요.  
  
## <a name="user-defined-data-type"></a>사용자 정의 데이터 형식  

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 UDT(사용자 정의 형식)를 도입하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 개체 및 사용자 지정 데이터 구조를 저장할 수 있도록 함으로써 SQL 형식 체계를 확장했습니다. UDT는 여러 데이터 형식과 동작이 포함될 수 있어 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터 형식으로 구성된 일반적인 별칭 데이터 형식과 차별화됩니다. UDT는 검증할 수 있는 코드를 생성하는 Microsoft .NET CLR(공용 언어 런타임)에서 지원하는 언어를 사용하여 정의합니다. 이러한 언어에는 Microsoft Visual C# 및 Visual Basic .NET 등이 있습니다. 데이터는 .NET Framework 기반 클래스 또는 구조의 필드와 속성으로 노출되며 동작은 클래스 또는 구조의 메서드로 정의됩니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 UDT를 테이블의 열 정의, [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리의 변수 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수나 저장 프로시저의 인수로 사용할 수 있습니다.  
  
사용자 정의 데이터 형식에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 “사용자 정의 형식 인스턴스 사용 및 수정”을 참조하세요.  
  
## <a name="sqlvariant-data-type"></a>Sql_variant 데이터 형식

Sql_variant 데이터 형식에 대 한 자세한 내용은 [Sql_variant 데이터 형식을 사용 하 여](../../connect/jdbc/using-sql-variant-datatype.md)입니다.  

## <a name="spatial-data-types"></a>공간 데이터 형식

공간 데이터 형식에 대 한 자세한 내용은 [공간 데이터 형식을 사용 하 여](../../connect/jdbc/use-spatial-datatypes.md)입니다.  

## <a name="see-also"></a>참고 항목

[JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
