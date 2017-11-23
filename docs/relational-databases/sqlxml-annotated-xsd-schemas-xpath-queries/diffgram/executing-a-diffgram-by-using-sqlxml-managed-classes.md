---
title: "관리 되는 클래스 SQLXML을 사용 하 여 DiffGram 실행 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], Managed Classes
- SQLXML Managed Classes, DiffGrams
- Managed Classes [SQLXML], DiffGrams
- SQLXML, Managed Classes
ms.assetid: 81c687ca-8c9f-4f58-801f-8dabcc508a06
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32b5ddd71a02ae931d4e79ce12ebf2afdcf590cb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="executing-a-diffgram-by-using-sqlxml-managed-classes"></a>SQLXML 관리되는 클래스를 사용하여 DiffGram 실행
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]DiffGram 파일을 실행 하는 방법을 보여 주는이 예제는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 데이터를 적용 하려면.NET Framework 환경 업데이트를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLXML 관리 되는 클래스 (Microsoft.Data.SqlXml)를 사용 하 여 테이블입니다.  
  
 이 예에서 DiffGram은 고객 ALFKI의 고객 정보(CompanyName 및 ContactName)를 업데이트합니다.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 **\<하기 전에 >** 블록을 포함 한  **\<고객 >** 요소 (**diffgr: id = "Customer1"**). **\<DataInstance >** 블록은 해당 포함  **\<고객 >** 가 같은 요소 **id**합니다.  **\<고객 >** 요소에는  **\<NewDataSet >** 지정 **diffgr: haschanges = "modified"**합니다. 이는 업데이트 작업임을 나타내며 이에 따라 Cust 테이블의 고객 레코드가 업데이트됩니다. 되는 경우는 **diffgr: haschanges** 특성이 지정 되지 않은 DiffGram 처리 논리는이 요소를 무시 하 고 업데이트가 수행 되지 않습니다.  
  
 다음은 C# 자습서 응용 프로그램에 위의 DiffGram을 실행 하 고 두 개의 테이블 (Cust, Ord)에서 만들도 업데이트를 SQLXML 관리 되는 클래스를 사용 하는 방법을 보여 주는 코드는 **tempdb** 데이터베이스입니다.  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=MyServer;database=tempdb;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlAdapter ad;  
      // Need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandStream = new FileStream("MyDiffgram.xml", FileMode.Open, FileAccess.Read);  
      cmd.CommandType = SqlXmlCommandType.DiffGram;  
      cmd.SchemaPath = "DiffGramSchema.xml";  
      // Load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
### <a name="to-test-the-application"></a>응용 프로그램을 테스트하려면  
  
1.  컴퓨터에 .NET Framework가 설치되어 있는지 확인합니다.  
  
2.  다음 XSD 스키마(DiffGramSchema.xml)를 폴더에 저장합니다.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
     </xsd:annotation>  
     <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
     </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  에 이러한 테이블을 만듭니다는 **tempdb** 데이터베이스입니다.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
4.  다음 예제 데이터를 추가합니다.  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
5.  위 DiffGram을 복사한 후 텍스트 파일에 붙여넣습니다. 파일을 1단계에 사용된 폴더와 같은 폴더에 MyDiffGram.xml로 저장합니다.  
  
6.  위의 C# 코드(DiffgramSample.cs)를 이전 단계에서 DiffGramSchema.xml 및 MyDiffGram.xml을 저장한 폴더와 같은 폴더에 저장합니다.  
  
    > [!NOTE]  
    >  연결 문자열에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름 '`MyServer`'는 실제 설치된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름으로 업데이트해야 합니다.  
  
     다른 폴더에 파일을 저장하는 경우 코드를 편집하여 매핑 스키마에 적합한 디렉터리 경로를 지정해야 합니다.  
  
7.  코드를 컴파일합니다. 다음을 사용하여 명령 프롬프트에서 코드를 컴파일합니다.  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DiffgramSample.cs  
    ```  
  
     이렇게 하면 실행 파일(DiffgramSample.exe)이 생성됩니다.  
  
8.  명령 프롬프트에서 DiffgramSample.exe를 실행합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DiffGram 예 &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)  
  
  
