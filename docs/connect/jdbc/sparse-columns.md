---
title: "스파스 열 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7d4237e0-818f-4639-9093-d5ac9683fc71
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e70b83f9c419c6d619ce4e90697e40289f4d9ae4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sparse-columns"></a>스파스 열
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  스파스 열은 Null 값에 대해 최적화된 저장소가 있는 일반 열입니다. 스파스 열을 사용하면 Null 값에 대한 공간 요구 사항이 줄어드는 반면 Null이 아닌 값을 검색하는 데 더 많은 오버헤드가 발생합니다. 최소 20%에서 40% 사이의 공간이 절약되는 경우에는 스파스 열을 사용하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0에 연결할 때 스파스 열 지원는 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] (또는 이후 버전) 서버. 사용할 수 있습니다 [SQLServerDatabaseMetaData.getColumns](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md), [SQLServerDatabaseMetaData.getFunctionColumns](../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md), 또는 [SQLServerDatabaseMetaData.getProcedureColumns](../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md) 열이 스파스 열 및는 열은 열을 확인 하려면 열을 설정 합니다.  
  
 열 집합은 형식화되지 않은 XML 형식의 모든 스파스 열을 반환하는 계산된 열입니다. 테이블의 열 수가 많거나 1024개를 초과하고 개별 스파스 열에서 작업하는 것이 복잡한 경우 열 집합을 사용하는 것이 좋습니다. 열 집합에는 최대 30,000개의 열이 포함될 수 있습니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>Description  
 이 예제에서는 열 집합을 검색하는 방법을 보여 줍니다. 또한 열 집합의 XML 출력을 구문 분석하여 스파스 열에서 데이터를 가져오는 방법도 보여 줍니다.  
  
 첫 번째 코드 목록은 서버에서 실행해야 하는 Transact-SQL입니다.  
  
 두 번째 코드 목록은 Java 소스 코드입니다. 응용 프로그램을 컴파일하기 전에 연결 문자열의 서버 이름을 변경합니다.  
  
### <a name="code"></a>코드  
  
```  
use AdventureWorks  
CREATE TABLE ColdCalling  
(  
ID int IDENTITY(1,1) PRIMARY KEY,  
[Date] date,  
[Time] time,  
PositiveFirstName nvarchar(50) SPARSE,  
PositiveLastName nvarchar(50) SPARSE,  
SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
);  
GO  
  
INSERT ColdCalling ([Date], [Time])  
VALUES ('10-13-09','07:05:24')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:00:24', 'AA', 'B')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:15:00', 'CC', 'DD')  
GO  
```  
  
### <a name="code"></a>코드  
  
```  
import java.sql.*;  
  
import javax.xml.parsers.DocumentBuilder;  
import javax.xml.parsers.DocumentBuilderFactory;  
  
import org.xml.sax.InputSource;  
  
import java.io.StringReader;  
  
import org.w3c.dom.Document;  
import org.w3c.dom.Node;  
import org.w3c.dom.NodeList;  
  
public class SparseColumns {  
  
   public static void main(String args[]) {  
      final String connectionUrl = "jdbc:sqlserver://my_server;databaseName=AdventureWorks;integratedSecurity=true;";  
  
      Connection conn = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         conn = DriverManager.getConnection(connectionUrl);  
  
         stmt = conn.createStatement();  
         // Determine the column set column  
         String columnSetColName = null;  
         String strCmd = "SELECT name FROM sys.columns WHERE object_id=(SELECT OBJECT_ID('ColdCalling')) AND is_column_set = 1";  
         rs = stmt.executeQuery(strCmd);  
  
         if (rs.next()) {  
            columnSetColName = rs.getString(1);  
            System.out.println(columnSetColName + " is the column set column!");  
         }  
         rs.close();  
  
         rs = null;   
  
         strCmd = "SELECT * FROM ColdCalling";  
         rs = stmt.executeQuery(strCmd);  
  
         // Iterate through the result set  
         ResultSetMetaData rsmd = rs.getMetaData();  
  
         DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();  
         DocumentBuilder db = dbf.newDocumentBuilder();  
         InputSource is = new InputSource();  
         while (rs.next()) {  
            // Iterate through the columns  
            for (int i = 1; i <= rsmd.getColumnCount(); ++i) {  
               String name = rsmd.getColumnName(i);  
               String value = rs.getString(i);  
  
               // If this is the column set column  
               if (name.equalsIgnoreCase(columnSetColName)) {  
                  System.out.println(name);  
  
                  // Instead of printing the raw XML, parse it  
                  if (value != null) {  
                     // Add artificial root node "sparse" to ensure XML is well formed  
                     String xml = "<sparse>" + value + "</sparse>";  
  
                     is.setCharacterStream(new StringReader(xml));  
                     Document doc = db.parse(is);  
  
                     // Extract the NodeList from the artificial root node that was added  
                     NodeList list = doc.getChildNodes();  
                     // This is the <sparse> node  
                     Node root = list.item(0);   
                     // These are the xml column nodes  
                     NodeList sparseColumnList = root.getChildNodes();   
  
                     // Iterate through the XML document  
                     for (int n = 0; n < sparseColumnList.getLength(); ++n) {  
                        Node sparseColumnNode = sparseColumnList.item(n);  
                        String columnName = sparseColumnNode.getNodeName();  
                        // Note that the column value is not in the sparseColumNode, it is the value of the first child of it  
                        Node sparseColumnValueNode = sparseColumnNode.getFirstChild();  
                        String columnValue = sparseColumnValueNode.getNodeValue();  
  
                        System.out.println("\t" + columnName + "\t: " + columnValue);  
                     }  
                  }  
               } else {   // Just print the name + value of non-sparse columns  
                  System.out.println(name + "\t: " + value);  
               }  
            }  
            System.out.println();//New line between rows  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      } finally {  
         if (rs != null) {  
            try {  
               rs.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
         if (stmt != null) {  
            try {  
               stmt.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
         if (conn != null) {  
            try {  
               conn.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
      }  
   }        
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

