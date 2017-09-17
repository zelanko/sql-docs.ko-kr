---
title: "고급 데이터 형식을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
caps.latest.revision: 58
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b74ed587d91e351f91db2e3ef2a45c41edf37918
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-advanced-data-types"></a>고급 데이터 형식 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] JDBC 고급 데이터 형식을 사용 하 여 변환 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 프로그래밍 언어 데이터 형식을 Java에서 인식할 수 있는 형식에 있습니다.  
  
## <a name="remarks"></a>주의  
 다음 표에서 고급 간의 기본 매핑을 나열 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], JDBC 및 Java 프로그래밍 언어 데이터 형식입니다.  
  
|SQL Server 형식|JDBC 형식(java.sql.Types)|Java 언어 형식|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|byte \(기본값), Blob, InputStream, String|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String(기본값), Clob, InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR(Java SE 6.0)|String(기본값), Clob, NClob(Java SE 6.0)|  
|xml|LONGVARCHAR<br /><br /> SQLXML(Java SE 6.0)|String(기본값), InputStream, Clob, byte[],Blob, SQLXML(Java SE 6.0)|  
|Udt<sup>1</sup>|VARBINARY|String(기본값), byte[], InputStream|  
  
 <sup>1</sup> 는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 전송 및 검색 이진 데이터로 CLR Udt를 지원 하지만 CLR 메타 데이터의 조작은 지원 하지 않습니다.  
  
 다음 섹션에서는 JDBC 드라이버와 고급 데이터 형식을 사용하는 방법의 예를 보여 줍니다.  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>BLOB, CLOB 및 NCLOB 데이터 형식  
 JDBC 드라이버는 java.sql.Blob, java.sql.Clob 및 java.sql.NClob 인터페이스의 모든 메서드를 구현합니다.  
  
> [!NOTE]  
>  CLOB 값은 함께 사용할 수 있습니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 이상의 큰 값 데이터 형식입니다. 특히 CLOB 형식은 사용할 수 있습니다는 **varchar (max)** 및 **nvarchar (max)** 데이터 형식 BLOB 형식을 사용 하 여 **varbinary (max)** 및 **이미지 ** NCLOB 형식 및 데이터 형식을 사용 하 여 **ntext** 및 **nvarchar (max)**합니다.  
  
## <a name="large-value-data-types"></a>큰 값 데이터 형식  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]특별 한 처리가 필요 큰 값 데이터 형식으로 작업 합니다. 큰 값 데이터 형식은 최대 행 크기가 8KB를 초과하는 데이터 형식입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]max 지정자에 대 한 소개 **varchar**, **nvarchar**, 및 **varbinary** 데이터 형식을 저장할 수 있도록 값의 2 ^31 바이트입니다. 테이블 열 및 [!INCLUDE[tsql](../../includes/tsql_md.md)] 변수를 지정할 수 **varchar (max)**, **nvarchar (max)**, 또는 **varbinary (max)** 데이터 형식입니다.  
  
 큰 값 형식을 사용하는 주요 시나리오는 큰 값 형식을 데이터베이스에서 검색하거나 데이터베이스에 추가하는 것입니다. 다음 섹션에서는 이러한 태스크를 수행하는 다양한 접근 방식에 대해 설명합니다.  
  
### <a name="retrieving-large-value-types-from-a-database"></a>데이터베이스에서 큰 값 형식 검색  
 이진이 아닌 큰 값 데이터 형식을 검색할 때-같은 **varchar (max)** 데이터 형식-데이터베이스에서 한 가지 방법은 해당 데이터를 문자 스트림으로 읽는 것입니다. 다음 예제에서는 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스는 데이터베이스에서 데이터를 검색 하 고 그 결과 집합 반환 하는 데 사용 됩니다. 그런 다음 [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) 의 메서드는 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스는 결과 집합에서 큰 값 데이터를 읽는 데 사용 됩니다.  
  
```  
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```  
  
> [!NOTE]  
>  에 대 한이 방법을 사용할 수도 있습니다는 **텍스트**, **ntext**, 및 **nvarchar (max)** 데이터 형식입니다.  
  
 이진 큰 값 데이터 형식을 검색할 때-같은 **varbinary (max)** 데이터 형식-데이터베이스에서 일부의 방식을 사용할 수 있는 합니다. 가장 효율적인 방법은 다음과 같이 데이터를 이진 스트림으로 읽는 것입니다.  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```  
  
 사용할 수도 있습니다는 [getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) 메서드를 다음과 같이 바이트 배열로 데이터를 읽습니다.  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```  
  
> [!NOTE]  
>  뿐만 아니라 데이터를 BLOB로 읽는 방법도 있습니다. 그러나 이 방법은 앞의 두 방법에 비해 효율이 떨어집니다.  
  
### <a name="adding-large-value-types-to-a-database"></a>데이터베이스에 큰 값 데이터 형식 추가  
 JDBC 드라이버로 큰 데이터를 업로드할 때 메모리 크기의 작업인 경우 원활하게 수행되지만 메모리 크기를 초과하는 작업의 경우에는 스트리밍이 최선의 수단입니다. 그러나 큰 데이터를 업로드하는 가장 효율적인 방법은 스트림 인터페이스를 사용하는 것입니다.  
  
 다음과 같이 문자열 또는 바이트를 사용하는 것도 한 가지 방법입니다.  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```  
  
> [!NOTE]  
>  에 저장 된 값에 대 한이 방법을 사용할 수도 있습니다 **텍스트**, **ntext**, 및 **nvarchar (max)** 열입니다.  
  
 서버에 이미지 라이브러리가 있는데 전체 이진 이미지 파일을 업로드 해야 하는 경우는 **varbinary (max)** 열의 JDBC 드라이버는 가장 효율적인 방법은 다음과 같이 스트림을 직접 사용 하 여입니다.  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)");  
File inputFile = new File("CLOBFile20mb.jpg");  
FileInputStream inStream = new FileInputStream(inputFile);  
int id = 1;  
pstmt.setInt(1,id);  
pstmt.setBinaryStream(2, inStream);  
pstmt.executeUpdate();  
inStream.close();  
```  
  
> [!NOTE]  
>  CLOB 또는 BLOB 메서드 중 하나를 사용하는 방법은 큰 데이터를 업로드하는 데는 적합하지 않습니다.  
  
### <a name="modifying-large-value-types-in-a-database"></a>데이터베이스에서 큰 값 데이터 형식 수정  
 대부분의 경우에서 업데이트 하거나 수정할 데이터베이스의 큰 값에 대 한 권장된 메서드를 통해 매개 변수를 전달 하는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 및 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스 사용 하 여 [!INCLUDE[tsql](../../includes/tsql_md.md)] UPDATE, WRITE 및 SUBSTRING와 같은 명령도 있습니다.  
  
 보관된 된 HTML 파일 처럼 큰 텍스트 파일에 포함 된 단어의 인스턴스를 교체 해야 하는 경우 다음과 같이 Clob 개체를 사용할 수 있습니다.  
  
```  
String SQL = "SELECT * FROM test1;";  
Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
ResultSet rs = stmt.executeQuery(SQL);  
rs.next();  
  
Clob clob = rs.getClob(2);  
long pos = clob.position("dog", 1);  
clob.setString(pos, "cat");  
rs.updateClob(2, clob);  
rs.updateRow();  
```  
  
 또한 서버에서 모든 작업을 수행하고 준비된 UPDATE 문에 매개 변수만 전달하는 방법도 있습니다.  
  
 큰 값 형식에 대한 자세한 내용은 SQL Server 온라인 설명서의 "큰 값 형식 사용"을 참조하십시오.  
  
## <a name="xml-data-type"></a>XML 데이터 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]제공 된 **xml** 데이터 형식 및 XML 문서를 저장할 수 있습니다에 조각의입니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. **xml** 데이터의 기본 제공 데이터 형식이 며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]와 같은 몇 가지 다른 기본 제공 유형과 비슷합니다는 **int** 및 **varchar**합니다. 다른 기본 제공 형식과 함께 사용할 수 있는 **xml** 테이블을 만들 때 열 유형으로; 변수 유형, 매개 변수 형식 또는 함수 반환 유형;로 또는에서 데이터 형식을 [!INCLUDE[tsql](../../includes/tsql_md.md)] CAST 및 CONVERT 함수입니다.  
  
 JDBC 드라이버에서는 **xml** 데이터 형식은 문자열, 바이트 배열, 스트림, CLOB, BLOB 또는 SQLXML 개체로 매핑될 수 있습니다. 기본값은 문자열입니다. JDBC 드라이버 버전 2.0 이상에서는 SQLXML 인터페이스가 추가된 JDBC 4.0 API가 지원됩니다. SQLXML 인터페이스는 XML 데이터에 대한 상호 작용 및 조작을 수행하는 메서드를 정의합니다. **SQLXML** 에 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** 데이터 형식입니다. 읽고으로 관계형 데이터베이스에 XML 데이터를 쓰는 방법에 대 한 자세한 내용은 **SQLXML** Java 데이터 형식 참조 [XML 데이터를 지 원하는](../../connect/jdbc/supporting-xml-data.md)합니다.  
  
 구현에서 **xml** JDBC 드라이버의 데이터 형식은 다음에 대 한 지원을 제공 합니다.  
  
-   가장 일반적인 프로그래밍 시나리오에서 표준 Java UTF-16 문자열로 XML에 액세스합니다.  
  
-   UTF-8 및 다른 8비트 인코딩 XML 입력을 지원합니다.  
  
-   다른 XML 프로세서 및 디스크 파일과의 교환을 위해 UTF-16으로 인코딩된 경우 선행 BOM이 있는 바이트 배열로 XML에 액세스합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]u t F-16으로 인코딩된 XML에 선행 BOM을 필요합니다. 응용 프로그램은 XML 매개 변수 값이 바이트 배열로 제공되는 경우에 이를 제공해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]utf-16 BOM 문자열 또는 포함 된 인코딩 선언에 항상 XML 값을 출력 합니다. XML 값을 byte[], BinaryStream 또는 BLOB로 검색하면 UTF-16 BOM이 값 앞에 붙습니다.  
  
 에 대 한 자세한 내용은 **xml** 에서 "xml 데이터 형식"을 참조 데이터 형식, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="user-defined-data-type"></a>사용자 정의 데이터 형식  
 사용자 정의 형식 (Udt)를 도입 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 개체 및 사용자 지정 데이터 구조에 데이터를 저장할 수 있도록 함으로써 SQL 형식 시스템이 확장는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다. UDT는 여러 데이터 형식과 동작이 포함될 수 있어 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 시스템 데이터 형식으로 구성된 일반적인 별칭 데이터 형식과 차별화됩니다. UDT는 검증할 수 있는 코드를 생성하는 Microsoft .NET CLR(공용 언어 런타임)에서 지원하는 언어를 사용하여 정의합니다. 이러한 언어에는 Microsoft Visual C# 및 Visual Basic .NET 등이 있습니다. 데이터는 .NET Framework 기반 클래스 또는 구조의 필드와 속성으로 노출되며 동작은 클래스 또는 구조의 메서드로 정의됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], UDT의 변수는 테이블의 열 정의로 사용할 수 있습니다는 [!INCLUDE[tsql](../../includes/tsql_md.md)] 일괄 처리 또는의 인수로 [!INCLUDE[tsql](../../includes/tsql_md.md)] 함수 또는 저장된 프로시저입니다.  
  
 사용자 정의 데이터 형식에 대 한 자세한 내용은 "수정" 인스턴스 사용 및 사용자 정의 형식의 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
