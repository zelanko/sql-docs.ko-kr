---
title: "상시 암호화와 JDBC 드라이버를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 12/30/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 64
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: fffb61c4c3dfa58edaf684f103046d1029895e7c
ms.openlocfilehash: cee7f5dbcf66a5357ae68192703d841ae1601a35
ms.contentlocale: ko-kr
ms.lasthandoff: 10/19/2017

---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>상시 암호화와 JDBC 드라이버 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서를 사용 하 여 Java 응용 프로그램을 개발 하는 방법에 대해 설명 [항상 암호화](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7) 및 Microsoft JDBC Driver 6.0 (또는 이상) for SQL Server.

항상 암호화 된 클라이언트가 중요 한 데이터를 암호화 하는 데이터 또는 SQL Server 또는 Azure SQL 데이터베이스에 암호화 키를 표시 하지 않을 수 있습니다. 상시 암호화 지원 드라이버 등 Microsoft JDBC Driver 6.0 (또는 그 이상) for SQL Server, 투명 하 게 암호화 하 고 클라이언트 응용 프로그램의 중요 한 데이터를 해독 하 여이 얻습니다. 드라이버는 쿼리를 자동으로 결정 매개 변수가 중요 데이터베이스 열 (상시 암호화를 사용 하 여 보호)에 해당 하 고 SQL Server 또는 Azure SQL 데이터베이스에 값을 전달 하기 전에 해당 매개 변수 값을 암호화 합니다. 마찬가지로, 이 드라이버는 쿼리 결과의 암호화된 데이터베이스 열에서 검색한 데이터의 암호를 투명하게 해독합니다. 자세한 내용은 참조 [상시 암호화 (데이터베이스 엔진)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7) 및 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.  


## <a name="prerequisites"></a>필수 구성 요소

- 데이터베이스에서 상시 암호화를 구성합니다. 상시 암호화를 구성하려면 상시 암호화 키를 프로비전하고 선택한 데이터베이스 열에 대한 암호화를 설정해야 합니다. 데이터베이스에 상시 암호화가 구성되지 않은 경우 [상시 암호화 시작](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_5)의 지침을 따르세요.
- 있는지 Microsoft JDBC Driver 6.0 (또는 이상) 확인 하십시오 SQL Server는 개발 컴퓨터에 설치 합니다. 
-   Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files를 다운로드하여 설치합니다.  zip 파일에 포함된 추가 정보에서 설치 지침 및 내보내기/가져오기 문제에 대한 자세한 내용을 읽어야 합니다.  
  
    -   정책 파일을 다운로드할 수 sqljdbc41.jar를 사용 하는 경우 [Java Cryptography Extension (JCE) 무제한 강도 Jurisdiction Policy Files 7 다운로드](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)  
  
    -   정책 파일을 다운로드할 수 sqljdbc42.jar를 사용 하는 경우 [Java Cryptography Extension (JCE) 무제한 강도 Jurisdiction Policy Files 8 다운로드](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)   
    
## <a name="enabling-always-encrypted-for-application-queries"></a>응용 프로그램 쿼리에 대해 Always Encrypted 사용  
값을 설정 하 여이 매개 변수를 암호화 및 암호화 된 열을 대상으로 하는 쿼리 결과의 암호 해독을 활성화 하는 가장 쉬운 방법은 **columnEncryptionSetting** 연결 문자열 키워드를  **활성화**합니다.

다음은 JDBC 드라이버에서 상시 암호화를 사용 하는 연결 문자열의 예입니다.
  
```  
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;"; 
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
     
```  
  
및 다음은 SQLServerDataSource 개체를 사용 하는 예제입니다.  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");  
SQLServerConnection con = (SQLServerConnection) ds.getConnection(); 
```    

상시 암호화는 개별 쿼리에도 사용할 수 있습니다. 참조는 **제어 성능 영향의 항상 암호화** 아래 섹션. 암호화 또는 암호 해독을 위해 상시 암호화를 사용하는 것은 적절하지 않습니다. 다음을 확인해야 합니다.
- 응용 프로그램에는 *VIEW ANY COLUMN MASTER KEY DEFINITION* 및 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 데이터베이스 권한이 있으며 데이터베이스에서 상시 암호화 키에 대한 메타데이터에 액세스하는 데 필요합니다. 자세한 내용은 [상시 암호화의 권한 섹션(데이터베이스 엔진)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7)을 참조하세요.
- 응용 프로그램은 열 암호화 키를 보호하는 열 마스터 키에 액세스하여 쿼리된 데이터베이스 열을 암호화할 수 있습니다. 연결 문자열에 추가 자격 증명을 제공 해야 할 Java 키 저장소 공급자를 사용 하는 note 합니다. 참조 **를 사용 하 여 Java 키 저장소 공급자** 자세한 내용은 섹션.

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>Java.sql.Time 값이 서버에 전송 방법 구성

**sendTimeAsDatetime** java.sql.Time 값을 서버에 보내는 방식을 구성할 연결 속성을 사용 합니다. 때 sendTimeAsDatetime = false, SQL Server 시간 유형으로 값은 전송 된 시간 및 시기 sendTimeAsDatetime = true, 날짜/시간 형식으로 값은 전송 된 시간입니다. 즉, 시간 열을 암호화할 때 sendTimeAsDatetime 속성이 해야 false 암호화 된 열에 시간 형식으로 날짜/시간 변환 지원 하지 않으므로 참고 합니다. 이 속성은 기본값은 true, 이때 수도 있으므로 시간 암호화 된 열을 사용할 경우 false로 설정 해야 합니다. 그렇지 않은 경우 드라이버는 예외로 throw 됩니다. SQLServerConnection 클래스에는 두 가지 방법,이 속성의 값을 프로그래밍 방식으로 구성 하려면 드라이버의 버전 6.0.
 
* public void setSendTimeAsDatetime (부울 sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

이 속성에 대 한 자세한 내용은 방문 [구성 방법을 java.sql.Time 값에는 서버에 보내집니다](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx)합니다. 

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>서버에 문자열 값은 전송 하는 방법을 구성 합니다.

**sendStringParametersAsUnicode** 연결 속성은 문자열 값을 SQL Server로 보내는 방법을 구성 하는 데 사용 합니다. 로 설정 하면 "true", 문자열 매개 변수는 전송 서버에 유니코드 형식으로. 문자열 매개 변수를 "false"로 설정 보내지면 유니코드가 아닌 ASCII/MBCS 등의 형식입니다. 이 속성에 대 한 기본값은 "true"입니다. 상시 암호화를 사용 하는 시기와 char/varchar/varchar(max) 열이 암호화의 가치 **sendStringParametersAsUnicode** true (또는 기본값으로 유지)로 설정 되어야 합니다. 이 속성을 false로 설정 되어 있으면 char/varchar/varchar(max) 암호화 된 열에 데이터를 삽입할 때 SQL Server 용 Microsoft JDBC 드라이버에서 예외가 throw 됩니다. 이 속성에 대 한 자세한 내용은 방문 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다. 
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>암호화된 열에서 데이터 검색 및 수정

응용 프로그램 쿼리에 대해 상시 암호화를 설정 하면 암호화 된 데이터베이스 열에 데이터를 검색 하거나 수정할 표준 JDBC Api를 사용할 수 있습니다. 암호화 된 열에서 검색 된 응용 프로그램에 필요한 데이터베이스 권한이 있고 액세스 열 마스터 키를 SQL Server 용 Microsoft JDBC Driver는 암호화할 수 암호화 된 열을 대상으로 하 고 데이터를 해독 하는 모든 쿼리 매개 변수를 가정 합니다. 데이터베이스 스키마의 열에 대 한 데이터 형식이 설정 JDBC 형식에 해당 하는 SQL Server의 일반 텍스트 값을 반환 합니다.
상시 암호화를 사용하지 않는 경우 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리가 실패합니다. 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없는 경우 쿼리가 암호화된 열에서 데이터를 검색할 수 있습니다. 그러나 Microsoft JDBC Driver for SQL Server에서 암호화 된 열에서 검색 된 값을 해독 하지 않으며 응용 프로그램 (바이트 배열)로 암호화 된 이진 데이터를 받게 됩니다.

아래 표에서는 상시 암호화 사용 여부에 따른 쿼리 동작을 요약합니다.

|쿼리 특성 | 상시 암호화가 설정되고 응용 프로그램에서 키 및 키 메타데이터에 액세스할 수 있는 경우|상시 암호화가 설정되고 응용 프로그램에서 키 또는 키 메타데이터에 액세스할 수 없는 경우 | 상시 암호화를 사용하지 않는 경우|
|:---|:---|:---|:---|
| 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리 | 매개 변수 값이 투명하게 암호화됩니다. | 오류 | 오류|
| 암호화된 열에서 데이터를 검색하는데, 암호화된 열을 대상으로 하는 매개 변수가 없는 쿼리| 암호화된 열의 결과가 투명하게 암호 해독됩니다. 응용 프로그램에서 암호화 된 열에 대해 구성 된 SQL Server 형식에 해당 하는 JDBC 데이터 형식을 유니코드로의 일반 텍스트 값을 받습니다. | 오류 | 암호화된 열의 결과가 암호 해독되지 않습니다. 응용 프로그램에서 암호화된 값을 바이트 배열(byte[])로 수신합니다.
      
 
### <a name="inserting-and-retrieving-encrypted-data-examples"></a>암호화 된 데이터 예제 삽입 및 검색 
다음 예제에는 암호화된 열에서 데이터를 검색 및 수정하는 방법을 설명합니다. 이 예제에서는 대상 테이블에 아래의 스키마가 있다고 가정합니다. SSN 및 BirthDate 열은 암호화되어 있습니다.

```
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1), 
 [SSN] [char](11) COLLATE Latin1_General_BIN2 
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC, 
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL, 
 [BirthDate] [date] 
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED, 
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256', 
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```
 
### <a name="inserting-data-example"></a>데이터 예제 삽입

이 예제에서는 Patients 테이블에 행을 삽입합니다. 다음에 유의하세요.
- 샘플 코드에는 암호화에 대한 내용이 없습니다. SQL Server 용 Microsoft JDBC 드라이버는 자동으로 검색 하 고 암호화 된 열을 대상으로 하는 매개 변수를 암호화 합니다. 이렇게 하면 응용 프로그램에 투명하게 암호화할 수 있습니다. 
- 데이터베이스 열을 포함 하는 암호화 된 열에 삽입 된 값은 SQLServerPreparedStatement를 사용 하 여 매개 변수로 전달 됩니다. 매개 변수를 사용 하 여는 (하지만,이 가장 좋습니다 SQL 주입 공격을 방지할 수 있으므로) 암호화 되지 않은 열에 값을 보낼 때 선택 사항 동안, 암호화 된 열을 대상으로 하는 값에 필요 합니다. SQL Server 용 Microsoft JDBC 드라이버는 암호화 된 대상 열에 있는 값을 확인 하지는 하므로 수 없기 때문에 쿼리가 실패 합니다 암호화 된 열에 삽입 된 값 쿼리 문에 포함 된 리터럴로 전달 된 경우 값을 암호화 합니다. 결과적으로, 암호화된 열과 호환 불가능한 것으로 간주하여 서버에서 거부합니다.
- Microsoft JDBC Driver for SQL Server가 암호화 된 열에서 검색 한 데이터를 투명 하 게 암호 해독 하는 대로 프로그램이 인쇄 하는 모든 값에 일반 텍스트로 됩니다.
- 수행 하려는 경우 사용 하 여 조회 절 WHERE 절에 사용 5d; 값을 매개 변수로 전달 될 SQL Server 용 Microsoft JDBC Driver는 투명 하 게 수행할 수 있도록 하는 경우 암호화 데이터베이스에 보내기 전에 합니다. SSN를 매개 변수로 전달 되지만 성 LastName로 리터럴로 전달 되는 아래 예제에서는 암호화 되지 않습니다.
- SSN 열을 대상으로 매개 변수에 사용 된 setter 방법은 setString() char/varchar SQL Server 데이터 형식으로 매핑됩니다. 이 매개 변수를 사용 하는 setter 메서드 있었던 setNString() nchar/nvarchar에 매핑되는 경우 항상 암호화에서는 암호화 된 nchar/nvarchar 값에서 암호화 된 char/varchar 값으로의 변환을 지원 하지 않으므로 쿼리가 실패 합니다.  

```
String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
try  
{           
     Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
     try (Connection sourceConnection = DriverManager.getConnection(connectionString))  
     {                  
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";        
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))  
        {
            insertStatement.setString(1, "795-73-9838");  
            insertStatement.setString(2, "Catherine");   
            insertStatement.setString(3, "Abel");                   
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));  
            insertStatement.executeUpdate();  
            System.out.println("1 record inserted.\n");  
        }         
     }  
}  
catch (Exception e)  
{  
    e.printStackTrace();  
}
```

### <a name="retrieving-plaintext-data-example"></a>일반 텍스트 데이터 검색 예제

다음 예제에서는 암호화된 값을 기준으로 데이터를 필터링하고 암호화된 열에서 일반 텍스트 데이터를 검색하는 방법을 보여 줍니다. 다음에 유의하세요.
- SQL Server 용 Microsoft JDBC Driver 암호화할 수 있도록 투명 하 게 하는 데이터베이스에 보내기 전에 매개 변수로 전달 될 필요한 SSN 열에서 필터링 할 WHERE 절에 사용 되는 값입니다.
- Microsoft JDBC Driver for SQL Server가 SSN 및 BirthDate 열에서 검색 한 데이터를 투명 하 게 암호 해독 하는 대로 프로그램이 인쇄 하는 모든 값에 일반 텍스트로 됩니다.

> [!NOTE]  
>  결정적 암호화를 사용하여 암호화된 경우 쿼리에서 열에 대해 동등 비교를 수행할 수 있습니다. 자세한 내용은 참조는 **선택 하면 결정적 또는 임의 암호화** 의 섹션은 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 항목입니다.  

```
String connectionString =  "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;" ;
String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";  

try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))  
{  
    selectStatement.setString(1, "795-73-9838");  
    ResultSet rs = selectStatement.executeQuery();   
    while(rs.next()) 
    {  
    System.out.println("SSN: " +rs.getString("SSN") + 
    ", FirstName: " + rs.getString("FirstName") + 
    ", LastName:"+ rs.getString("LastName")+
     ", Date of Birth: " + rs.getString("BirthDate"));  
          }  
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>암호화된 데이터 검색 예제

상시 암호화를 사용하지 않는 경우에도 쿼리에 암호화된 열을 대상으로 하는 매개 변수가 없으면 암호화된 열에서 데이터를 검색할 수 있습니다.

다음 예제에서는 암호화된 열에서 암호화된 이진 데이터를 검색하는 방법을 보여 줍니다. 다음에 유의하세요.

- 연결 문자열에서는 상시 암호화를 사용하지 않으므로 쿼리에서 SSN 및 BirthDate의 암호화된 값을 바이트 배열로 반환합니다(프로그램에서 값을 문자열로 변환).
- 암호화된 열을 대상으로 하는 매개 변수가 없으면 상시 암호화를 사용하지 않고 암호화된 열에서 데이터를 검색하는 쿼리에 매개 변수가 있을 수 있습니다. 위의 쿼리는 LastName을 기준으로 필터링되며 데이터베이스에서 암호화되지 않습니다. 쿼리가 SSN 또는 BirthDate를 기준으로 필터링되면 쿼리가 실패합니다.

```
String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;"; 
 
try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))  
{  
    selectStatement.setString(1, "Abel");  
    ResultSet rs = selectStatement.executeQuery();   
    while(rs.next())
    {  
        System.out.println("SSN: " + rs.getString("SSN") +
         ", FirstName: " + rs.getString("FirstName") + 
        ", LastName:"+ rs.getString("LastName")+ 
        ", Date of Birth: " + rs.getString("BirthDate"));  
    } 
}  
catch (Exception e)  
{  
    e.printStackTrace();  
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>암호화된 열 쿼리 시 일반적인 문제 방지

이 섹션에서는 방지 하는 방법에 대 한 몇 가지 지침 및 Java 응용 프로그램에서 암호화 된 열을 쿼리할 때 일반적인 오류 범주를 설명 합니다.

### <a name="unsupported-data-type-conversion-errors"></a>지원 되지 않는 데이터 형식 변환 오류

상시 암호화는 암호화된 데이터 형식에 대해 몇 가지 변환을 지원합니다. 참조 [상시 암호화 (데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 자세한 목록은 지원 되는 형식 변환에 대 한 합니다. 데이터 형식 변환 오류를 방지하려면 다음을 확인하세요.

- 적절 한 setter 메서드를 사용 하 여 전달 하는 경우 암호화 된 열을 대상으로 매개 변수 값 매개 변수의 SQL Server 데이터 형식이 되도록 정확히 동일한 대상 열 또는 매개 변수의 SQL Server 데이터 형식 변환의 형식으로 대상 열의 형식을 사용할 수 있습니다. Note는 새로운 API 메서드가 특정 SQL Server 데이터 형식에 해당 하는 매개 변수를 전달할 SQLServerPreparedStatement, SQLServerCallableStatement 및 SQLServerResultSet 클래스에 추가 되었습니다. 예를 들어, 열 암호화 되지 않은 경우에 datetime2 또는 날짜/시간 열의 매개 변수를 전달할 setTimestamp() 메서드를 사용할 수 있습니다. 하지만 열을 암호화할 때 데이터베이스에 있는 열의 유형을 나타내는 정확 하 게 메서드를 사용 해야 합니다. 예를 들어 setTimestamp()를 사용 하 여 하는 암호화 된 datetime2 열에 값을 전달 하 고 setDateTime()를 사용 하 여 암호화 된 datetime 열에 값을 전달 합니다. 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) 전체 목록은 새로운 Api입니다. 
- SQL Server 데이터 형식이 decimal 및 numeric인 열을 대상으로 하는 매개 변수의 정밀도 및 배율이 대상 열에 대해 구성된 정밀도 및 배율과 동일해야 합니다. Note는 새로운 API 메서드가 정밀도 배율을 decimal 및 numeric 데이터 형식을 나타내는 매개 변수/열에 대 한 데이터 값과 함께 적용 하려면 SQLServerPreparedStatement, SQLServerCallableStatement 및 SQLServerResultSet 클래스에 추가 되었습니다. 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) 오버 로드/새 Api의 전체 목록은 합니다.  
- datetime2, datetimeoffset, 또는 시간 SQL Server 데이터 형식 열을 대상으로 하는 매개 변수의 소수 자릿수 초의 자릿수/소수 대상 열의 값을 수정 하는 쿼리에서 대상 열에 대 한 보다 큽니다. Note는 새로운 API 메서드가 이러한 데이터 형식을 나타내는 매개 변수에 대 한 데이터 값과 함께 소수 자릿수 초의 자릿수/소수를 허용 하도록 SQLServerPreparedStatement, SQLServerCallableStatement 및 SQLServerResultSet 클래스에 추가 되었습니다. 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) 오버 로드/새 Api의 전체 목록은 합니다.   

### <a name="errors-due-to-incorrect-connection-properties"></a>잘못 된 연결 속성으로 인해 발생 오류
이 섹션에서는 상시 암호화 데이터를 사용 하 여 적절 하 게 연결 설정을 구성 하는 방법에 설명 합니다. 암호화 된 데이터 형식에는 제한 된 변환을 지 원하는, 암호화 된 열을 사용 하는 경우 'sendTimeAsDatetime' 및 'sendStringParametersAsUnicode' 연결 설정을 제대로 구성을 해야 합니다. 사항을 확인 합니다. 
- [sendTimeAsDatetime](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx) 시간 열을 암호화 된 데이터를 삽입 하는 경우 연결 설정이 false로 설정 되어 있습니다. 자세한 내용은 '구성 서버에 java.sql.Time 값이 전송 방법' 섹션을 참조 합니다.
- [sendStringParametersAsUnicode](../../connect/jdbc/setting-the-connection-properties.md) 연결 설정이로 설정 되어 true (또는 기본값으로 유지) 데이터를 삽입 char/varchar/varchar(max) 열을 암호화 하는 경우. 자세한 내용은 '구성 서버에 문자열 값 전송 방법' 섹션을 참조 합니다.

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>암호화 된 값 대신 일반 텍스트로 전달 된 오류

암호화된 열을 대상으로 하는 모든 값은 응용 프로그램 내에서 암호화해야 합니다. 암호화된 열에서 삽입/수정하거나 일반 텍스트 값을 기준으로 필터링하면 다음과 같은 오류가 발생합니다.


```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

이러한 오류를 방지하려면 다음을 확인합니다.
- 항상 암호화 (연결 문자열에 대해 또는 특정 쿼리에 대해) 암호화 된 열을 대상으로 하는 응용 프로그램 쿼리에 대해 활성화 됩니다.
- 준비 된 문을 사용 하 고 암호화 된 열을 데이터 대상으로 보낼 매개 변수입니다. 아래 예제를 기준으로 잘못 필터링 암호화 된 열 (SSN)에서 리터럴/상수 리터럴 내부 매개 변수로 전달 하는 대신 쿼리를 보여 줍니다. 이 쿼리가 실패 합니다.

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");  
```

## <a name="working-with-column-master-key-stores"></a>열 마스터 키 저장소 작업
매개 변수 값을 암호화 하거나 쿼리 결과의 데이터를 해독 하는 Microsoft JDBC Driver for SQL Server 대상 열에 대해 구성 된 열 암호화 키를 가져올 해야 합니다. 열 암호화 키는 데이터베이스 메타 데이터에 암호화 된 형태로 저장 됩니다. 각 열 암호화 키에는 열 암호화 키를 암호화하는 데 사용된 해당 열 마스터 키가 있습니다. 데이터베이스 메타데이터에는 열 마스터 키가 저장되지 않습니다. 특정 열 마스터 키가 포함된 키 저장소와 키 저장소에서의 키 위치에 대한 정보만 저장됩니다.

열 암호화 키의 일반 텍스트 값을 가져오려면 Microsoft JDBC Driver for SQL Server 먼저 메타 데이터를 가져온 열 암호화 키 및 해당 열 마스터 키를 둘 다에 대 한 다음을 사용 하 여 정보 메타 데이터에 키에 게 문의 하십시오. 열 마스터 키가 포함 된 저장소 및 암호화 된 열 암호화 키를 암호 해독 합니다. 파생 된 클래스의 인스턴스는 열 마스터 키 저장소 공급자-사용 키 저장소와 통신 하는 SQL Server 용 Microsoft JDBC Driver **SQLServerColumnEncryptionKeyStoreProvider** 클래스입니다.


### <a name="using-built-in-column-master-key-store-providers"></a>기본 제공 열 마스터 키 저장소 공급자 사용
  
SQL Server 용 Microsoft JDBC 드라이버는 다음과 같은 기본 제공 열 마스터 키 저장소 공급자 함께 제공 됩니다. Note 됩니다 (공급자 조회에 사용) 특정 공급자 이름으로 미리 등록 된 이러한 공급자 중 일부를 일부 추가 자격 증명이 나 명시적 등록 해야 합니다.

| 클래스 | 설명 | 공급자 (조회) 이름 |미리 등록?|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Azure 키 자격 증명 모음에 대 한 키 저장소에 대 한 공급자입니다.| AZURE_KEY_VAULT|아니요|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Windows 인증서 저장소에 대 한 공급자입니다.|MSSQL_CERTIFICATE_STORE|예
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Java keystore에 대 한 공급자|MSSQL_JAVA_KEYSTORE|예|

미리 등록 된 키 저장소 공급자에 대 한 다음이 공급자를 사용 하지만 다음 사항에 주의를 응용 프로그램 코드 변경할 필요가 없습니다.

- 사용자 또는 DBA는 열 마스터 키 메타데이터에 구성된 공급자 이름이 정확하고 열 마스터 키 경로가 특정 공급자에 대해 적합한 키 경로 형식을 준수해야 합니다. CREATE COLUMN MASTER KEY(Transact-SQL) 문을 실행할 때 적합한 공급자 이름 및 키 경로를 자동으로 생성하는 SQL Server Management Studio 등의 도구를 사용하여 키를 구성하는 것이 좋습니다.
- 응용 프로그램에서 키 저장소의 키에 액세스할 수 있어야 합니다. 이는 키 저장소를 기준으로 응용 프로그램 액세스를 키 및/또는 키 저장소에 부여하거나 다른 키 저장소 관련 구성 단계를 수행하는 것과 관련이 있습니다. 예를 들어는 SQLServerColumnEncryptionJavaKeyStoreProvider 사용에 대 한 필요한 위치 및 연결 속성에서 키 저장소의 암호를 제공 합니다. 

이러한 키 저장소 공급자를 모두 아래에서 자세히 설명 되어 있습니다.
  
### <a name="using-azure-key-vault-provider"></a>Azure 주요 자격 증명 모음 공급자 사용
Azure 주요 자격 증명 모음은 상시 암호화에 대한 열 마스터 키를 저장 및 관리하는 편리한 옵션입니다(특히 응용 프로그램이 Azure에서 호스트되는 경우). SQL Server 용 Microsoft JDBC Driver Azure 키 자격 증명 모음에 저장 된 키가 있는 응용 프로그램에 대 한 기본 제공된 공급자, SQLServerColumnEncryptionAzureKeyVaultProvider가 포함 되어 있습니다. 이 공급자의 이름은 AZURE_KEY_VAULT입니다. Azure 키 자격 증명 모음 저장소 공급자를 사용 하려면 응용 프로그램 개발자를 Azure에서 자격 증명 모음 및 키 만들고 키에 액세스할 수 응용 프로그램을 구성 해야 합니다. 주요 자격 증명 모음을 설정 하 고 열 마스터 키 생성 하는 방법에 대 한 자세한 내용은를 참조 [Azure 키 자격 증명 모음 – 키 자격 증명 모음 설정에 대 한 자세한 내용은 단계별](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) 및 [Azure 키 자격 증명 모음의열마스터키만들기](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2).  
  
Azure 키 자격 증명 모음을 사용 하려면 클라이언트 응용 프로그램의 SQLServerColumnEncryptionAzureKeyVaultProvider 인스턴스화하고 드라이버에 등록 해야 합니다.

SQLServerColumnEncryptionAzureKeyVaultProvider 초기화의 예는 다음과 같습니다.  
  
```  
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey); 
```

응용 프로그램을 사용 하 여 SQL Server에 대 한 Microsoft JDBC 드라이버에서 인스턴스를 등록 해야 응용 프로그램 SQLServerColumnEncryptionAzureKeyVaultProvider의 인스턴스를 만든 후의 Sqlserverconnection.registercolumnencryptionkeystoreproviders () 메서드입니다. 이 가장 좋습니다, 그리고 AZURE_KEY_VAULT SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API를 호출 하 여 가져올 수 있는 기본 조회 이름을 사용 하 여 인스턴스에 등록 하는 합니다. 기본 이름을 사용 하 여 하면 프로 비전 할 SQL Server Management Studio 또는 PowerShell 등의 도구를 사용 하 고 상시 암호화 키 (도구 열 마스터 키 메타 데이터 개체를 생성 하는 기본 이름을 사용 하는 데 사용)를 관리할 수 있습니다. 아래 예제에서는 Azure 키 자격 증명 모음 공급자 등록 보여 줍니다. Sqlserverconnection.registercolumnencryptionkeystoreproviders () 메서드에 대 한 자세한 내용은 참조 하십시오. [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다. 

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();   
keyStoreMap.put(akvProvider.getName(), akvProvider);   
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);   
```
  
> [!IMPORTANT]  
>  JDBC 드라이버의 Azure 주요 자격 증명 모음 구현 (GitHub)에서 이러한 라이브러리에 의존 합니다.  
>   
>  [java에 대 한 azure sdk](https://github.com/Azure/azure-sdk-for-java)  
>   
>  [azure-active directory-라이브러리-에-java 라이브러리](https://github.com/AzureAD/azure-activedirectory-library-for-java)  
  
### <a name="using-windows-certificate-store-provider"></a>Windows 인증서 저장소 공급자를 사용 하 여
Windows 인증서 저장소에 열 마스터 키를 저장 하는 SQLServerColumnEncryptionCertificateStoreProvider는 사용할 수 있습니다. SQL Server Management Studio (SSMS)에서 상시 암호화 마법사 또는 기타 지원 되는 도구를 사용 하 여 데이터베이스에 열 마스터 키와 열 암호화 키 정의 만들 수 있습니다. 수 있는 Windows 인증서 저장소에서 자체 서명 된 인증서를 생성 하는 동일한 마법사를 사용할 수는 항상 암호화 된 데이터에 대 한 열 마스터 키로 사용 합니다. 열 마스터 키와 열 암호화에 대 한 자세한 내용은 키 T-SQL 구문 방문 [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) 및 [CREATE COLUMN ENCRPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 각각.

SQLServerColumnEncryptionCertificateStoreProvider의 이름은 "MSSQL_CERTIFICATE_STORE" 이며 공급자 개체의 getName() API에서 쿼리할 수 있습니다. 드라이버에 의해 자동으로 등록 하 고 모든 응용 프로그램 변경 없이 원활 하 게 사용할 수 있습니다.

> [!IMPORTANT]  
>  JDBC 드라이버의 SQLServerColumnEncryptionCertificateStoreProvider 구현은 Windows 운영 체제에만 사용할 수 및 드라이버 패키지에서 사용할 수 있는 sqljdbc_auth.dll에 종속 되어 있습니다.  이 공급자를 사용 하려면 JDBC 드라이버를 설치한 컴퓨터에서 Windows 시스템 경로에 있는 디렉터리를 sqljdbc_auth.dll 파일을 복사 합니다. 또는 java.libary.path 시스템 속성에 sqljdbc_auth.dll의 디렉터리를 지정할 수도 있습니다. 32비트 JVM(Java Virtual Machine)을 실행할 경우 운영 체제가 x64 버전이라도 x86 폴더에 있는 sqljdbc_auth.dll 파일을 사용하십시오. x64 프로세서에서 64비트 JVM을 실행할 경우 x64 폴더의 sqljdbc_auth.dll 파일을 사용하십시오. 예를 들어 32 비트 JVM을 사용 하는 경우 JDBC 드라이버는 기본 디렉터리에 설치 되어 있으면 Java 응용 프로그램을 시작 하는 경우에 다음 가상 컴퓨터 (VM) 인수를 사용 하 여 DLL의 위치를 지정할 수 있습니다.  
`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`
        
### <a name="using-java-key-store-provider"></a>Java 키 저장소 공급자를 사용 하 여  
JDBC 드라이버는 기본 제공된 키와 함께 제공 저장소 공급자 구현을 Java 키 저장소에 대 한 합니다. 드라이버 자동으로 인스턴스화하고 경우 Java 키 저장소에 대 한 공급자를 등록 된 **keyStoreAuthentication** 연결 문자열 속성이 연결 문자열에 있고 "JavaKeyStorePassword"로 설정 됩니다 (참조 하세요 자세한 내용은 아래)입니다. Java 키 저장소 공급자 이름은 MSSQL_JAVA_KEYSTORE 합니다. 이 이름은 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API에서 쿼리할 수도 있습니다. 

3 개의 새 연결 문자열 키워드는 드라이버가 Java 키 저장소에 인증 하는 데 필요한 자격 증명을 선언적으로 지정 하는 클라이언트 응용 프로그램을 허용 하도록 제공 됩니다. 드라이버는 특정 연결에 대 한 연결 문자열의 다음 세 가지 속성의 값을 기반으로 하는 공급자를 초기화 합니다. 
  
 **keyStoreAuthentication:** 사용 하는 키 저장소를 식별 합니다. SQL Server 용 Microsoft JDBC Driver 6.0,이 속성을 통해 Java 키 저장소에 인증할 수 있습니다. Java 키 저장소에 대 한이 속성에 대 한 값 "JavaKeyStorePassword" 이어야 합니다.   
  
 **keyStoreLocation:** 열 마스터 키를 저장 하는 Java keystore 파일의 경로입니다. 경로는 키 저장소 파일 이름을 참고 합니다.  
  
 **keyStoreSecret:** 키 뿐만 아니라 keystore에 사용할 보안/암호입니다. Java 키 저장소 키 저장소를 사용 하 여에 대 한 사항에 유의 하 고 키 암호가 동일 해야 합니다.  

연결 문자열에 이러한 자격 증명 제공에 예제는 다음과 같습니다.

    String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
    
이러한 설정은 set/get SQLServerDataSource 개체를 사용 하 여 될 수도 있습니다. 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md) 자세한 정보에 대 한 합니다.     
  
이 자격 증명은 연결 속성에 나타나야 하는 경우 JDBC 드라이버는 SQLServerColumnEncryptionJavaKeyStoreProvider를 자동으로 인스턴스화합니다. 
  
### <a name="creating-a-column-master-key-for-the-java-key-store"></a>Java 키 저장소에 대 한 열 마스터 키 만들기
SQLServerColumnEncryptionJavaKeyStoreProvider JKS, PKCS12 키 저장소 유형을 사용할 수 있습니다. 만들기 또는 가져오기에이 공급자와 함께 사용할 키를 사용 하 여이 Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) 유틸리티입니다. 키 자체 키 저장소와 동일한 암호를 갖도록 note 하십시오. 공개 키와 keytool 유틸리티를 사용 하 여 연결된 된 개인 키를 만드는 방법의 예를 들면 다음과 같습니다.

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks    

이 명령은 공개 키를 만들고이 자체 서명 된 인증서의의 연결 된 개인 키와 함께 ' keystore.jks' 키 저장소에 저장 되는 X.509에 래핑합니다. 키 저장소에이 항목은 'AlwaysEncryptedKey' 별칭으로 식별 됩니다. 

사용 하 여 동일한 PKCS12 storetype의 예를 들면 다음과 같습니다. 

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword   

키 저장소의 경우 형식이 PKCS12 키 암호 및 키 암호에 대 한 keytool 유틸리티 라는 메시지가 표시 되지 않습니다는 SQLServerColumnEncryptionJavaKeyStoreProvider 키 저장소 및 키 있다고의 필요에 따라-keypass 옵션으로 제공 해야 합니다.는 동일한 암호입니다.

.Pfx 형식으로 Windows 인증서 저장소에서 인증서를 내보낼 하 고는 SQLServerColumnEncryptionJavaKeyStoreProvider 함께 사용 하는 수도 있습니다. 내보낸된 인증서 Java 키 저장소에 JKS 키 저장소 형식으로 가져올 수도 있습니다. 

Keytool 항목을 만든 후 키 저장소 공급자 이름 및 키 경로 데이터베이스에 열 마스터 키 메타 데이터를 만들 해야 합니다. 열 마스터 키 메타 데이터를 만드는 방법에 대 한 자세한 내용은 방문 [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)합니다. SQLServerColumnEncryptionJavaKeyStoreProvider, 키 경로 키의 별칭만입니다. 및는 SQLServerColumnEncryptionJavaKeyStoreProvider 이름은 'MSSQL_JAVA_KEYSTORE'. 또한 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스의 getName() 공용 API를 사용 하 여이 이름을 쿼리할 수 있습니다. 

열 마스터 키를 만들기 위한 T-SQL 구문은 다음과 같습니다.

```  
CREATE COLUMN MASTER KEY [<CMK_name>]  
WITH  
(  
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',  
    KEY_PATH = N'<key_alias>'  
)  
```  

'AlwaysEncryptedKey' 위에서 만든에 대 한 열 마스터 키 정의 합니다.

```  
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```  
    
> [!NOTE]  
>  기본 제공 SQL Server management Studio 기능은 만들 수 없습니다 열 T-SQL 명령을 사용 해야 하는 Java 키 저장소에 대 한 마스터 키 정의 합니다.  
  
### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>Java 키 저장소에 대 한 열 암호화 키 만들기
SQL Server management Studio 또는 다른 도구 사용할 수 없습니다 Java 키 저장소에 열 마스터 키를 사용 하 여 암호화 키 열을 만들려면 note 합니다. 클라이언트 응용 프로그램이 프로그래밍 방식으로 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스를 사용 하 여 열 암호화 키를 만들어야 합니다. 자세한 내용은 '를 사용 하 여 열 마스터 키 저장소 공급자 프로그래밍 방식으로 키 프로 비전에 대 한 ' 섹션을 참조 하십시오. 

  
### <a name="implementing-a-custom-column-master-key-store-provider"></a>사용자 지정 열 마스터 키 저장소 공급자 구현
기존 공급자에서 지원 되지 않는 키 저장소에 열 마스터 키를 저장 하려는 경우 SQLServerColumnEncryptionKeyStoreProvider 클래스를 확장 하 고 사용 하 여 공급자를 등록 하 여 사용자 지정 공급자를 구현할 수 있습니다는 Sqlserverconnection.registercolumnencryptionkeystoreproviders () 메서드입니다.
  
```  
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";
    
    public void setName(String name)
    {
        this.name = name;
    }
    
    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)  
    {  
        // Logic for encrypting the column encryption key  
    }  
    
    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)  
    {  
        // Logic for decrypting the column encryption key  
    }  
}  
  
```  
  
 공급자를 등록합니다.  
  
```  
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();  
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();  
keyStoreMap.put(storeProvider.getName(), storeProvider);  
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);  
  
```  
  
## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>열 마스터 키 저장소 공급자를 사용하여 프로그래밍 방식으로 키 프로비전

암호화 된 열에 액세스할 때는 SQL Server 용 Microsoft JDBC Driver 투명 하 게 찾아서 열 암호화 키의 암호를 해독 하려면 오른쪽 열 마스터 키 저장소 공급자를 호출 합니다. 일반적으로 정상적인 응용 프로그램 코드는 열 마스터 키 저장소 공급자를 직접 호출하지 않습니다. 그러나 명시적으로 공급자를 시작 및 호출하여 프로그래밍 방식으로 상시 암호화 키를 프로비전 및 관리하고, 암호화된 열 암호화 키를 생성하고, 열 암호화 키의 암호를 해독할 수 있습니다(예: 열 마스터 키 순환의 일부로). 자세한 내용은 [상시 암호화를 위한 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)를 참조하세요.
사용자 지정 키 저장소 공급자를 사용하는 경우에만 고유한 키 관리 도구를 구현해야 합니다. Windows 인증서 저장소 또는 Azure 키 자격 증명 모음에 저장 된 키를 사용할 때 관리 하 고 키를 프로 비전 할 SQL Server Management Studio 또는 PowerShell과 같은 기존 도구를 사용할 수 있습니다. Java 키 저장소에 저장 된 키를 사용할 때 키를 프로그래밍 방식으로 프로 비전 해야 합니다. 아래 예제에서는 Java 키 저장소에 저장 된 키를 사용 하 여 키를 암호화 하 SQLServerColumnEncryptionJavaKeyStoreProvider 클래스를 사용 하 여 보여 줍니다.

```  
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<proide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore. 
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider = 
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key 
                 * For more details on the syntax refer: 
                 * https://msdn.microsoft.com/library/mt146372.aspx
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY " 
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = " 
                        + columnMasterKeyName
                        + " , ALGORITHM =  '" 
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x" 
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by  SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation : 
         *      Path where keystore is located, including the keystore file name. 
         * 2) keyStoreSecret : 
         *      Password of the keystore and the key.  
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}

```  
  
## <a name="force-encryption-on-input-parameters"></a>입력된 매개 변수에서 암호화 적용
  
암호화 적용 기능 상시 암호화를 사용 하는 경우 매개 변수의 암호화를 적용 합니다. 암호화 적용을 사용 하는 경우 SQL Server에 암호화 매개 변수가 필요 하지 않은 드라이버에 알립니다 매개 변수를 사용 하면 쿼리가 실패 합니다. 이 속성은 데이터 노출을 야기할 수 있는 잘못된 암호화 메타데이터를 클라이언트에게 제공하는 손상된 SQL Server를 포함하는 보안 공격에 대한 추가 보호를 제공합니다. SQLServerPreparedStatement 및 SQLServerCallableStatement 클래스 및 업데이트의 집합 * 메서드\* force 암호화 설정을 지정 하려면 부울 인수를 허용 하려면 SQLServerResultSet 클래스의 메서드는 오버 로드 합니다. 이 인수의 값이 false 이면 드라이버는 매개 변수에 대 한 암호화를 요구 하지 않습니다. 암호화 적용 설정 되어 있으면 true, 쿼리 매개 변수를만 보낼 대상 열이 암호화 하 고 연결 또는 명령문에 상시 암호화 사용 합니다. 추가 계층을 데이터가 실수로에 전송 되도록 SQL Server 텍스트로 암호화 되도록 예상 되는 경우 보안을 제공 합니다.  
  
 Force 암호화 설정으로 오버 로드 된 SQLServerPreparedStatement 및 SQLServerCallableStatement 방법에 자세한 내용은 참조 [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-performance-impact-of-always-encrypted"></a>상시 암호화의 성능 영향 제어

상시 암호화는 클라이언트 쪽 암호화 기술이므로 데이터베이스가 아닌 클라이언트 쪽에서 대부분의 성능 오버헤드가 발생합니다. 암호화 및 암호 해독 작업의 비용 외에 클라이언트 쪽 성능 오버헤드의 원인은 다음과 같습니다.
- 쿼리 매개 변수에 대한 메타데이터를 검색하기 위해 데이터베이스에 대한 추가 왕복
- 열 마스터 키에 액세스하기 위한 열 마스터 키 저장소 호출

이 섹션에서는 SQL Server와는 위의 두 성능 요소 영향을 제어 하는 방법에 대 한 Microsoft JDBC 드라이버에서 기본 제공 성능 최적화를 설명 합니다.

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>쿼리 매개 변수에 대한 메타데이터를 검색하기 위한 왕복 제어

항상 암호화가 설정 되어 연결을 기본적으로 SQL Server 용 Microsoft JDBC Driver를 호출 합니다 [sys.sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396) 전달 (없이 쿼리 문을 각 매개 변수가 있는 쿼리에 대 한 매개 변수 값) SQL Server에 있습니다. [sys.sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396) 매개 변수를 암호화 해야 하 고, 이러한 각 작업에 대 한 반환 된 경우 SQL Server 용 Microsoft JDBC 드라이버 사용 하면 되는 암호화 관련 정보를 확인 하려면 쿼리 문을 분석 하 여 매개 변수 값을 암호화 합니다. 위의 동작은 클라이언트 응용 프로그램에 대한 높은 수준의 투명도를 보장합니다. 응용 프로그램 (및 응용 프로그램 개발자) 않습니다 암호화 된 열을 대상으로 값이 SQL Server 용 Microsoft JDBC Driver를 매개 변수로 전달 됩니다으로 어떤 쿼리가 암호화 된 열 액세스 주의 해야 할 필요는 없습니다.


#### <a name="setting-always-encrypted-at-the-query-level"></a>쿼리 수준에서 상시 암호화 설정

매개 변수화된 쿼리의 암호화 메타데이터 검색을 위한 성능 영향을 제어하려면 연결이 아닌 개별 쿼리에 대해 상시 암호화를 설정합니다. 이렇게 하면 암호화된 열을 대상으로 하는 매개 변수가 있는 쿼리에 대해서만 sys.sp_describe_parameter_encryption을 호출할 수 있습니다. 단, 이 경우 암호화의 투명성이 저하될 수 있습니다. 데이터베이스 열의 암호화 속성을 변경한 경우 스키마 변경에 맞게 응용 프로그램 코드를 변경해야 할 수 있습니다.


개별 쿼리의 상시 암호화 동작을 제어 하려면 SQLServerStatementColumnEncryptionSetting 데이터는 전송 및 읽고 쓸 때 받은 방법을 지정 하는 열거형을 전달 하 여 개별 statement 개체를 구성 해야 암호화 된 열에 대해 특정 설명 합니다. 다음은 몇 가지 유용한 지침입니다.
- 대부분이 데이터베이스 연결 액세스 암호화된 열을 통해 전송하는 클라이언트 응용 프로그램을 쿼리하는 경우:
    - ColumnEncryptionSetting 연결 문자열 키워드 사용으로 설정 합니다.
    - 암호화 된 모든 열을 액세스 하지 않는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.Disabled를 설정 합니다. 이렇게 하면 sys.sp_describe_parameter_encryption이 호출되지 않고 결과 집합 값의 암호 해독도 시도되지 않습니다.
    - 암호화를 요구 하는 모든 매개 변수가 없는 없지만 암호화 된 열에서 데이터를 검색 하는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.ResultSet를 설정 합니다. sys.sp_describe_parameter_encryption 호출 및 매개 변수 암호화가 사용되지 않습니다. 쿼리가 암호화 열에서 결과를 해독할 수 없습니다.
- 대부분이 암호화된 열에 액세스하지 않는 데이터베이스 연결을 통해 보내는 클라이언트 응용 프로그램을 쿼리하는 경우:
    - ColumnEncryptionSetting 연결 문자열 키워드 사용 안 함으로 설정 합니다.
    - 암호화 해야 하는 모든 매개 변수가 있는 개별 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.Enabled를 설정 합니다. 이렇게 하면 sys.sp_describe_parameter_encryption이 호출될 뿐만 아니라 암호화된 열에서 검색된 모든 쿼리 결과의 암호가 해독됩니다.
    - 암호화를 요구 하는 매개 변수가 없지만 암호화 된 열에서 데이터를 검색 하는 쿼리에 대해 SQLServerStatementColumnEncryptionSetting.ResultSet를 설정 합니다. sys.sp_describe_parameter_encryption 호출 및 매개 변수 암호화가 사용되지 않습니다. 쿼리가 암호화 열에서 결과를 해독할 수 없습니다.

Note SQLServerStatementColumnEncryptionSetting 설정을 암호화를 무시 하 고 일반 텍스트 데이터에 액세스를 사용할 수 없습니다. 문에서 열 암호화를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [상시 암호화 API 참조 JDBC 드라이버에 대 한](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)합니다.  

아래 예제에서는 데이터베이스 연결에 대해 상시 암호화가 사용되지 않습니다. 응용 프로그램에서 실행하는 쿼리에는 암호화되지 않은 LastName 열을 대상으로 하는 매개 변수가 있습니다. 쿼리는 암호화된 SSN 및 BirthDate 열에서 데이터를 검색합니다. 이러한 경우 암호화 메타데이터를 검색할 때 sys.sp_describe_parameter_encryption을 호출하지 않아도 됩니다. 그러나 응용 프로그램에서 두 암호화된 열에서 일반 텍스트 값을 가져올 수 있도록 쿼리 결과에 대한 암호 해독을 설정해야 합니다. 되도록 SQLServerStatementColumnEncryptionSetting.ResultSet 설정이 사용 됩니다.

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";  
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord, 
        ResultSet.TYPE_FORWARD_ONLY, 
        ResultSet.CONCUR_READ_ONLY, 
        connection.getHoldability(), 
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");  
ResultSet rs = selectStatement.executeQuery();  
while(rs.next()) {  
    System.out.println("First name: " + rs.getString("FirstName"));  
    System.out.println("Last name: " + rs.getString("LastName"));  
    System.out.println("SSN: " + rs.getString("SSN"));  
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));  
}  
rs.close();
selectStatement.close();
connection.close();
```


### <a name="column-encryption-key-caching"></a>열 암호화 키 캐싱

열 암호화 키를 해독 하는 열 마스터 키 저장소에 대 한 호출의 수를 줄이려면 SQL Server 용 Microsoft JDBC Driver는 메모리에 일반 텍스트 열 암호화 키를 캐시 합니다. 데이터베이스 메타데이터에서 암호화된 열 암호화 키 값을 받은 후 드라이버는 제일 먼저 암호화된 키 값에 해당하는 일반 텍스트 열 암호화 키를 찾습니다. 드라이버는 캐시에서 암호화된 열 암호화 키 값을 찾을 수 없는 경우에만 열 마스터 키가 포함된 키 저장소를 호출합니다.

SQLServerConnection 클래스의 setColumnEncryptionKeyCacheTtl(), API를 사용 하 여 캐시에 열 암호화 키 항목에 대 한 활성 시간 값을 구성할 수 있습니다. 열 암호화 키 항목이 캐시에 대 한 기본 활성 시간 값은 2 시간입니다. 캐싱 해제 하려면 값 0 사용 합니다. 설정 하려면 활성 시간 값 사용 되는 모든 API:
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
   
예를 들어 10 분의 활성 시간 값을 설정 하려면 사용
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)

Note 시간 단위로 일, 시, 분 또는 초, 지원 됩니다.  


## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>SQLServerBulkCopy를 사용 하 여 암호화 된 데이터를 복사 합니다.

SQLServerBulkCopy를 이미 암호화 되 고 데이터를 해독 하지 않고 한 테이블을 다른 테이블에 저장 된 데이터를 복사할 수 있습니다. 이렇게 하려면 다음을 수행합니다.

- 대상 테이블의 암호화 구성이 원본 테이블의 구성과 일치하는지 확인합니다. 특히 두 테이블에 동일한 암호화 열이 있고 동일한 암호화 형식 및 암호화 키를 사용하여 열이 암호화되어야 합니다. 참고: 대상 열 중 하나가 해당 원본 열과 다르게 암호화된 경우 복사 작업 후 대상 테이블의 데이터 암호를 해독할 수 없습니다. 데이터가 손상됩니다.
- 상시 암호화를 사용하지 않고 원본 테이블과 대상 테이블에 대한 데이터베이스 연결을 구성합니다. 
- AllowEncryptedValueModifications 옵션을 설정 합니다. 참조 [JDBC 드라이버를 사용 하 여 대량 복사를 사용 하 여](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md) 자세한 정보에 대 한 합니다.
 
SQL Server 용 Microsoft JDBC Driver는 데이터가 암호화 되었는지, 또는 동일한 암호화를 사용 하 여 올바르게 암호화 하는 경우를 검사 하지 않기 때문에 데이터베이스를 손상 될 수 AllowEncryptedValueModifications를 지정할 때는 주의 하 참고: 형식, 알고리즘 및 키에 대상 열으로 합니다.

## <a name="see-also"></a>관련 항목:  
 [상시 암호화(데이터베이스 엔진)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  

