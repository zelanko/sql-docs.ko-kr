---
title: CLR 및 XML을 사용한 연락처 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: b5185c1e-56de-41a8-a9c3-eec663750cde
caps.latest.revision: 15
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6e7e534ec77dce09c99ba9172f6917308e39022c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213773"
---
# <a name="contact-creation-using-clr-and-xml"></a>CLR 및 XML을 사용한 연락처 만들기
  SQL Server의 연락처 예제는 기본 AdventureWorks2012 예제 데이터베이스의 맨 위에 추가 기능 계층을 형성하는 몇 가지 유용한 유틸리티를 제공합니다. 첫 번째 유틸리티는 AdventureWorks2012 데이터베이스와 관련이 있는 여러 부류의 사람에 대한 연락처 레코드를 만듭니다. 연락처 정보는 XML을 사용하여 지정하고 C# 기반 또는 VB 저장 프로시저로 전달되어 XML을 만들고 이 XML을 데이터베이스의 적합한 테이블에 배치합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 프로젝트를 만들고 실행하려면 다음 소프트웨어가 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 설명서 및 예제 [웹 사이트](http://go.microsoft.com/fwlink/?LinkId=31046)에서 무료로 구할 수 있습니다.  
  
-    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개발자 [웹 사이트](http://go.microsoft.com/fwlink/?linkid=62796)에서 제공되는 AdventureWorks 데이터베이스  
  
-   .NET Framework SDK 2.0 이상 또는 Microsoft Visual Studio 2005 이상. .NET Framework SDK는 무료로 구할 수 있습니다.  
  
-   또한 다음 조건을 충족해야 합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 CLR 통합이 설정되어 있어야 합니다.  
  
-   CLR 통합을 설정하려면 다음 단계를 수행합니다.  
  
    #### <a name="enabling-clr-integration"></a>CLR 통합 사용  
  
    -   다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령을 실행합니다.  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  CLR을 설정하려면 `ALTER SETTINGS` 서버 수준 사용 권한이 있어야 합니다. 이 사용 권한은 `sysadmin` 및 `serveradmin` 고정 서버 역할의 멤버가 암시적으로 소유합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 AdventureWorks 데이터베이스를 설치해야 합니다.  
  
-   사용하고 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 관리자가 아닌 경우 설치를 완료하기 위해 관리자로부터 **CreateAssembly**  권한을 부여 받아야 합니다.  
  
## <a name="building-the-sample"></a>예제 빌드  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>다음 지침을 사용하여 예제를 만들고 실행합니다.  
  
1.  Visual Studio 또는 .NET Framework 명령 프롬프트를 엽니다.  
  
2.  필요한 경우 예제에 대한 디렉터리를 만듭니다. 이 예에서는 C:\MySample을 사용합니다.  
  
3.  c:\MySample에서 `Contacts.vb`(Visual Basic 예제용) 또는 `Contacts.cs`(C# 예제용)를 만들고 적합한 Visual Basic 또는 C# 예제 코드(아래)를 파일에 복사합니다.  
  
4.  선택하는 언어에 따라 다음 중 하나를 실행하여 명령줄 프롬프트에서 예제 코드를 컴파일합니다.  
  
5.  `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /target:library Contacts.vb`  
  
6.  `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /target:library Contacts.cs`  
  
7.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 코드를 파일에 복사하고 해당 파일을 예제 디렉터리에 `Install.sql` 로 저장합니다.  
  
8.  예제가 `C:\MySample\`이외의 디렉터리에 설치된 경우 해당 위치를 가리키도록 표시된 대로 `Install.sql` 파일을 편집합니다.  
  
9. 다음을 실행하여 어셈블리 및 저장 프로시저를 배포합니다.  
  
    -   `sqlcmd -E -I -i install.sql`  
  
10. [!INCLUDE[tsql](../../includes/tsql-md.md)] 테스트 명령 스크립트를 파일에 복사하고 해당 파일을 예제 디렉터리에 `test.sql` 로 저장합니다.  
  
11. 다음 명령으로 테스트 스크립트를 실행합니다.  
  
    -   `sqlcmd -E -I -i test.sql`  
  
12. [!INCLUDE[tsql](../../includes/tsql-md.md)] 정리 스크립트를 파일에 복사하고 해당 파일을 예제 디렉터리에 `cleanup.sql` 로 저장합니다.  
  
13. 다음 명령으로 스크립트를 실행합니다.  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>예제 코드  
 다음은 이 예제에 대한 코드 목록입니다.  
  
 C#  
  
```csharp  
using System;  
using System.IO;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Collections.Generic;  
using System.Globalization;  
using System.Runtime.Serialization;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
    /// <summary>  
    /// Utility class for creating contact information.  A row in the contact table  
    /// is inserted.  Additionally, rows in one or more other tables are inserted based on  
    /// the information provided in the XML document passed to the CreateContact function.  
    /// For individuals and employees, the contact record is one to one relationship with   
    /// the respective tables so those rows are created when the contact record is created.  
    /// For stores and vendors, there is a one to many relationship for contacts, so a row is added to   
    /// either the Sales.StoreContact or Purchasing.VendorContact table (as appropriate), but   
    /// neither store or vendor rows are inserted into the database.  
    ///   
    /// </summary>  
    public sealed class ContactUtils  
    {  
  
        private ContactUtils()  
        {  
        }  
  
        public static void CreateContact(SqlString contactData,  
                                         out SqlInt32 contactId,  
                                         out SqlInt32 customerId)  
        {  
            //TODO: When we can pass XML from T-SQL then contactData can be a SqlXmlReader  
using (StringReader sr = new StringReader(contactData.Value))  
{  
XmlReader reader = XmlReader.Create(sr);  
ContactCreator creator = null;  
  
try  
{  
reader.MoveToContent();  
EnsureEqual(reader.LocalName, "Contact");  
reader.MoveToContent();  
reader.ReadStartElement();  
  
switch (reader.LocalName)  
{  
case "Individual": creator = new IndividualCreator(); break;  
case "Store": creator = new StoreCreator(); break;  
case "Vendor": creator = new VendorCreator(); break;  
case "Employee": creator = new EmployeeCreator(); break;  
default: break;  
}  
  
if (creator != null)  
{  
reader.ReadStartElement();  
reader.MoveToContent();  
creator.LoadDictionary(reader);  
creator.Create();  
contactId = creator.ContactId;  
customerId = creator.CustomerId;  
}  
else  
{  
contactId = -1;  
customerId = -1;  
  
throw new AWUtilitiesContactParseException(  
"Individual | Store | Vendor | Employee", reader.LocalName);  
}  
}  
finally  
{  
reader.Close();  
}  
}  
        }  
  
        public static void EnsureEqual(String localName,  
                                       String desiredLocalName)  
        {  
if (localName == null) throw new ArgumentNullException("localName");  
            if (!localName.Equals(desiredLocalName))  
            {  
                throw new AWUtilitiesContactParseException(desiredLocalName,  
                                                       localName);  
            }  
        }  
    }  
  
    /// <summary>  
    ///Base class for all the contact creation classes.  Responsible for parsing the XML,  
    ///providing the public API for all types of contacts, and for inserting the row   
    ///in the Person.Contact table.  
    /// </summary>  
  
    public abstract class ContactCreator  
    {  
  
        internal int parameterCount;  
        internal int valueCount;  
  
        internal Dictionary<String, String> contactDictionary = new Dictionary<  
            String, String>();  
  
        private static readonly String[] xmlColumns = new String[] {  
"AdditionalContactInfo", "Demographics"  
};  
  
        private static readonly String[] nestedColumns = new String[] {  
"Address"  
};  
  
        public int ContactId  
        {  
            get  
            {  
                String val;  
                if (contactDictionary.TryGetValue("ContactID", out val))  
                    return Int32.Parse(val, CultureInfo.InvariantCulture);  
                else  
                    return -1;  
            }  
            set  
            {  
                contactDictionary["ContactID"]  
                    = value.ToString(CultureInfo.InvariantCulture);  
            }  
        }  
  
        public int CustomerId  
        {  
            get  
            {  
                string val;  
  
                if (contactDictionary.TryGetValue("CustomerID", out val))  
                    return Int32.Parse(val, CultureInfo.InvariantCulture);  
                else  
  
                    //Not every contact is for a customer.  Return -1 in that case.  
                    return -1;  
            }  
            set  
            {  
                contactDictionary["CustomerID"]  
                    = value.ToString(CultureInfo.InvariantCulture);  
            }  
        }  
  
        public void LoadDictionary(XmlReader reader)  
        {  
            while (reader.IsStartElement())  
            {  
                String key = reader.LocalName;  
                String val;  
  
                if (Array.IndexOf(xmlColumns, key) > -1)  
                    val = reader.ReadInnerXml();  
                else if (Array.IndexOf(nestedColumns, key) > -1)  
                {  
                    reader.ReadStartElement();  
                    LoadDictionary(reader);  
                    reader.ReadEndElement();  
                    continue;  
                }  
                else  
                    val = reader.ReadElementString();  
  
                contactDictionary.Add(key, val);  
            }  
        }  
  
        protected void ResetCounters(int valueForReset)  
        {  
            parameterCount = valueForReset;  
            valueCount = valueForReset;  
        }  
  
        public String MaybeParameter(String name)  
        {  
            if (contactDictionary.ContainsKey(name))  
            {  
                if (parameterCount++ == 0)  
                    return name;  
                else  
                    return ", " + name;  
            }  
            else  
                return string.Empty;  
        }  
  
        public String MaybeValue(String name)  
        {  
            if (contactDictionary.ContainsKey(name))  
            {  
                if (valueCount++ == 0)  
                    return "@" + name;  
                else  
                    return ", @" + name;  
            }  
            else  
                return string.Empty;  
        }  
  
public static object TypeConvert(String valueToConvert, SqlDbType parameterType)  
        {  
if (valueToConvert == null)   
throw new ArgumentNullException("valueToConvert");  
            switch (parameterType)  
            {  
                case SqlDbType.BigInt:  
                    return Int64.Parse(valueToConvert,  
                        CultureInfo.InvariantCulture);  
  
                case SqlDbType.Int:  
                    return Int32.Parse(valueToConvert,  
                        CultureInfo.InvariantCulture);  
  
                case SqlDbType.SmallInt:  
                    return Int16.Parse(valueToConvert,  
                        CultureInfo.InvariantCulture);  
  
                case SqlDbType.TinyInt:  
                    return Byte.Parse(valueToConvert,  
                        CultureInfo.InvariantCulture);  
  
                case SqlDbType.Bit:  
                    {  
                        if (valueToConvert.Equals("1") ||  
                            valueToConvert.Equals("true")) return 1;  
                        else  
                            return 0;  
                    }  
  
                case SqlDbType.NVarChar:  
                case SqlDbType.VarChar:  
                case SqlDbType.NChar:  
                case SqlDbType.NText:  
                case SqlDbType.Text:  
                case SqlDbType.Char:  
                case SqlDbType.Xml:  
                    return valueToConvert;  
  
                case SqlDbType.DateTime:  
                    return DateTime.Parse(valueToConvert,  
                        CultureInfo.InvariantCulture);  
  
                case SqlDbType.Money:  
                    return Decimal.Parse(valueToConvert,  
                        CultureInfo.InvariantCulture);  
  
                default:  
                    return "unknown conversion";  
            }  
        }  
  
        public void MaybeAddCommandParameter(String keyName, String parameterName,  
                                             SqlCommand command,  
                                             SqlDbType parameterType,  
                                             bool isRequired,  
                                             String defaultValue)  
        {  
            if (isRequired || contactDictionary.ContainsKey(keyName))  
            {  
                SqlParameter param =  
                             new SqlParameter("@" + parameterName, parameterType);  
                String val = (contactDictionary.ContainsKey(keyName)) ?  
                             contactDictionary[keyName] : defaultValue;  
  
                param.Value = TypeConvert(val, parameterType);  
                command.Parameters.Add(param);  
            }  
        }  
        public void MaybeAddCommandParameter(String name, SqlCommand command,  
                                             SqlDbType parameterType,  
                                             bool isRequired,  
                                             String defaultValue)  
        {  
            MaybeAddCommandParameter(name, name, command, parameterType,  
                                     isRequired, defaultValue);  
        }  
  
        public void MaybeAddCommandParameter(String name, SqlCommand command,  
                                             SqlDbType parameterType, int size,  
                                             bool isRequired,  
                                             String defaultValue)  
        {  
            if (isRequired || contactDictionary.ContainsKey(name))  
            {  
                MaybeAddCommandParameter(name, command, parameterType,  
                                         isRequired, defaultValue);  
                command.Parameters[command.Parameters.Count - 1].Size = size;  
            }  
        }  
  
        public void MaybeAddCommandParameter(String keyName, String paramName, SqlCommand command,  
                                             SqlDbType parameterType, int size,  
                                             bool isRequired,  
                                             String defaultValue)  
        {  
            if (isRequired || contactDictionary.ContainsKey(keyName))  
            {  
                MaybeAddCommandParameter(keyName, paramName, command, parameterType,  
                                         isRequired, defaultValue);  
                command.Parameters[command.Parameters.Count - 1].Size = size;  
            }  
        }  
  
        public virtual void Create()  
        {  
            using (SqlConnection conn = new SqlConnection("context connection=true"))  
            {  
                SqlCommand command = conn.CreateCommand();  
  
                ResetCounters(1);  
  
                string parameters = String.Format(CultureInfo.InvariantCulture,  
                    "NameStyle{0}, FirstName{1}, LastName{2}{3}{4}{5}, "  
                    + "PasswordHash, PasswordSalt{6}",  
                    MaybeParameter("Title"), MaybeParameter("MiddleName"),  
                    MaybeParameter("Suffix"), MaybeParameter("EmailAddress"),  
                    MaybeParameter("EmailPromotion"), MaybeParameter("Phone"),  
                    MaybeParameter("AdditionalContactInfo"));  
                string values = String.Format(CultureInfo.InvariantCulture,  
                    "@NameStyle{0}, @FirstName{1}, @LastName{2}{3}{4}{5}, "  
                    + "@PasswordHash, @PasswordSalt{6}",  
                    MaybeValue("Title"), MaybeValue("MiddleName"),  
                    MaybeValue("Suffix"), MaybeValue("EmailAddress"),  
                    MaybeValue("EmailPromotion"), MaybeValue("Phone"),  
                    MaybeValue("AdditionalContactInfo"));  
  
                String text = String.Format(CultureInfo.InvariantCulture,  
                    "INSERT INTO Person.Contact ({0}) VALUES ({1}); "  
                    + "SELECT CAST(SCOPE_IDENTITY() as Int);",  
                    parameters, values);  
                command.CommandText = text;  
                MaybeAddCommandParameter("NameStyle", command,  
                    SqlDbType.Bit, true, "0");  
                MaybeAddCommandParameter("Title", command,  
                    SqlDbType.NVarChar, 8, false, null);  
                MaybeAddCommandParameter("FirstName", command,  
                    SqlDbType.NVarChar, 50, true, string.Empty);  
                MaybeAddCommandParameter("MiddleName", command,  
                    SqlDbType.NVarChar, 50, false, null);  
                MaybeAddCommandParameter("LastName", command,  
                    SqlDbType.NVarChar, 50, true, string.Empty);  
                MaybeAddCommandParameter("Suffix", command,  
                    SqlDbType.NVarChar, 10, false, null);  
                MaybeAddCommandParameter("EmailAddress", command,  
                    SqlDbType.NVarChar, 50, true, string.Empty);  
                MaybeAddCommandParameter("EmailPromotion", command,  
                    SqlDbType.Int, false, null);  
                MaybeAddCommandParameter("Phone", command,  
                    SqlDbType.NVarChar, 25, false, null);  
                MaybeAddCommandParameter("PasswordHash", command,  
                    SqlDbType.VarChar, 40, true, string.Empty);  
                MaybeAddCommandParameter("PasswordSalt", command,  
                    SqlDbType.VarChar, 10, true, string.Empty);  
                MaybeAddCommandParameter("AdditionalContactInfo", command,  
                    SqlDbType.Xml, false, null);  
                conn.Open();  
                this.ContactId = (int)command.ExecuteScalar();  
            }  
        }  
    }  
  
    /// <summary>  
    ///A base class based on ContactCreator which is responsible for inserting information about  
    ///a customer by inserting a row in the   
    ///Sales.Customer table.  Currently only used by the IndividualCreator class, but  
    ///it might be useful if there was a variant made of the StoreCreator which actually inserted  
    ///a Sales.Store row.   
    /// </summary>  
  
    public abstract class CustomerCreator : ContactCreator  
    {  
        public override void Create()  
        {  
            base.Create();  
            using (SqlConnection conn   
                = new SqlConnection("context connection=true"))  
            {  
                SqlCommand command = conn.CreateCommand();  
  
                if (!contactDictionary.ContainsKey("CustomerType"))  
                    contactDictionary["CustomerType"] = "I";  
                ResetCounters(0);  
                string parameters = String.Format(CultureInfo.InvariantCulture,   
                    "{0}{1}{2}", MaybeParameter("SalesPersonID"),  
                    MaybeParameter("TerritoryID"),  
                    //CustomerType is always present, but we  
                    //need to get the commas right  
                    MaybeParameter("CustomerType"));  
                string values = String.Format(CultureInfo.InvariantCulture,   
                    "{0}{1}{2}", MaybeValue("SalesPersonID"),  
                    MaybeValue("TerritoryID"), MaybeValue("CustomerType"));  
                command.CommandText = String.Format(CultureInfo.InvariantCulture,  
                    "INSERT INTO Sales.Customer ({0}) VALUES ({1}); "  
                    + "SELECT CAST(SCOPE_IDENTITY() as Int);",  
                    parameters, values);  
                MaybeAddCommandParameter("SalesPersonID", command,  
                    SqlDbType.Int, false, null);  
                MaybeAddCommandParameter("TerritoryID", command,  
                    SqlDbType.Int, false, null);  
                MaybeAddCommandParameter("CustomerType", command,  
                    SqlDbType.NChar, 1, true, "I");  
                conn.Open();  
                this.CustomerId = (int)command.ExecuteScalar();  
            }  
        }  
    }  
  
    /// <summary>  
    ///Responsible for adding information about an individual purchasing by   
    ///inserting a row in the Sales.Individual table.  
    /// </summary>  
  
    public class IndividualCreator : CustomerCreator  
    {  
        public override void Create()  
        {  
            base.Create();  
            using (SqlConnection conn  
                = new SqlConnection("context connection=true"))  
            {  
                SqlCommand command = conn.CreateCommand();  
  
                ResetCounters(2);  
                String parameters = String.Format(CultureInfo.InvariantCulture,  
                    "CustomerID, ContactID{0}", MaybeParameter("Demographics"));  
                String values = String.Format(CultureInfo.InvariantCulture,  
                    "@CustomerID, @ContactID{0}", MaybeValue("Demographics"));  
                command.CommandText =  
                    String.Format(CultureInfo.InvariantCulture,  
                    "INSERT INTO Sales.Individual ({0}) VALUES ({1});",  
                    parameters, values);  
                MaybeAddCommandParameter("CustomerID", command,  
                    SqlDbType.Int, true, string.Empty);  
                MaybeAddCommandParameter("ContactID", command,  
                    SqlDbType.Int, true, string.Empty);  
                MaybeAddCommandParameter("Demographics", command,  
                    SqlDbType.Xml, false, null);  
                conn.Open();  
                command.ExecuteNonQuery();  
            }  
        }  
    }  
  
    /// <summary>  
    ///Responsible for relating a contact to a store by inserting a row in the   
    ///Sales.StoreContact table.  
    /// </summary>  
  
    public class StoreCreator : ContactCreator  
    {  
        public override void Create()  
        {  
            base.Create();  
            using (SqlConnection conn   
                = new SqlConnection("context connection=true"))  
            {  
                SqlCommand command = conn.CreateCommand();  
  
                command.CommandText =  
                    String.Format(CultureInfo.InvariantCulture,  
                    "INSERT INTO Sales.StoreContact (CustomerID, ContactID, "  
                    + "ContactTypeID) VALUES (@CustomerID, @ContactID, @ContactTypeID);");  
                MaybeAddCommandParameter("CustomerID", command,  
                    SqlDbType.Int, true, string.Empty);  
                MaybeAddCommandParameter("ContactID", command,  
                    SqlDbType.Int, true, string.Empty);  
                MaybeAddCommandParameter("ContactTypeID", command,  
                    SqlDbType.TinyInt, true, string.Empty);  
                conn.Open();  
                command.ExecuteNonQuery();  
            }  
        }  
    }  
  
    /// <summary>  
    ///Responsible for relating a contact to a vendor by inserting a row in the   
    ///Purchasing.VendorContact table.  
    /// </summary>  
  
    public class VendorCreator : ContactCreator  
    {  
        public override void Create()  
        {  
            base.Create();  
            using (SqlConnection conn   
                = new SqlConnection("context connection=true"))  
            {  
                SqlCommand command = conn.CreateCommand();  
  
                String parameters = "VendorID, ContactID, ContactTypeID";  
                String values = String.Format(CultureInfo.InvariantCulture,   
                    "@VendorID, @ContactID, @ContactTypeID");  
  
                command.CommandText =  
                    String.Format(CultureInfo.InvariantCulture,  
                    "INSERT INTO Purchasing.VendorContact ({0}) VALUES ({1});",  
                    parameters, values);  
                MaybeAddCommandParameter("VendorID", command,  
                    SqlDbType.Int, true, string.Empty);  
                MaybeAddCommandParameter("ContactID", command,  
                    SqlDbType.Int, true, string.Empty);  
                MaybeAddCommandParameter("ContactTypeID", command,  
                    SqlDbType.TinyInt, true, string.Empty);  
                conn.Open();  
                command.ExecuteNonQuery();  
            }  
        }  
    }  
  
    /// <summary>  
    ///Responsible for adding information about an employee by creating an address and then  
    ///inserting a row in the HumanResources.Employee table.  
    /// </summary>  
  
    public class EmployeeCreator : ContactCreator  
    {  
        public override void Create()  
        {  
            base.Create();  
            CreateAddress();  
            int employeeID = -1;  
            using (SqlConnection conn = new SqlConnection("context connection=true"))  
            {  
                SqlCommand command = conn.CreateCommand();  
  
                ResetCounters(3);  
                String parameters = String.Format(CultureInfo.InvariantCulture,  
                    "NationalIDNumber, ContactID, LoginID{0}, Title, "  
                    + "BirthDate, MaritalStatus, Gender, HireDate, "  
                    + "SalariedFlag, VacationHours, SickLeaveHours",  
                    MaybeParameter("ManagerID"));  
                String values = String.Format(CultureInfo.InvariantCulture,  
                    "@NationalIDNumber, @ContactID, @LoginID{0}, @Title, "  
                    + "@BirthDate, @MaritalStatus, @Gender, @HireDate, "  
                    + "@SalariedFlag, @VacationHours, @SickLeaveHours",  
                    MaybeValue("ManagerID"));  
  
                command.CommandText =  
                    String.Format(CultureInfo.InvariantCulture,  
                    "INSERT INTO HumanResources.Employee ({0}) VALUES ({1}); "   
                    + "SELECT CAST(SCOPE_IDENTITY() as Int);",   
                    parameters, values);  
                MaybeAddCommandParameter("NationalIDNumber", command,  
                    SqlDbType.NVarChar, 15, true, string.Empty);  
                MaybeAddCommandParameter("ContactID", command,  
                    SqlDbType.Int, true, string.Empty);  
                MaybeAddCommandParameter("LoginID", command,  
                    SqlDbType.NVarChar, 256, true, string.Empty);  
                MaybeAddCommandParameter("ManagerID", command,  
                    SqlDbType.Int, false, null);  
                MaybeAddCommandParameter("JobTitle", "Title", command,  
                    SqlDbType.NVarChar, 50, true, string.Empty);  
                MaybeAddCommandParameter("BirthDate", command,  
                    SqlDbType.DateTime, true, string.Empty);  
                MaybeAddCommandParameter("MaritalStatus", command,  
                    SqlDbType.NChar, 1, true, string.Empty);  
                MaybeAddCommandParameter("Gender", command,  
                    SqlDbType.NChar, 1, true, string.Empty);  
                MaybeAddCommandParameter("HireDate", command,  
                    SqlDbType.DateTime, true, string.Empty);  
                MaybeAddCommandParameter("SalariedFlag", command,  
                    SqlDbType.Bit, true, "1");  
                MaybeAddCommandParameter("VacationHours", command,  
                    SqlDbType.SmallInt, true, "0");  
                MaybeAddCommandParameter("SickLeaveHours", command,  
                    SqlDbType.SmallInt, true, "0");  
                conn.Open();  
                employeeID = (int)command.ExecuteScalar();  
            }  
            CreateEmployeeAdddress(employeeID,  
                int.Parse(contactDictionary["AddressID"],  
                System.Globalization.CultureInfo.InvariantCulture));  
            CreateEmployeeDepartmentHistory(employeeID,  
                int.Parse(contactDictionary["DepartmentID"],  
                System.Globalization.CultureInfo.InvariantCulture),  
                int.Parse(contactDictionary["ShiftID"],  
                System.Globalization.CultureInfo.InvariantCulture));  
  
        }  
  
        public void CreateAddress()  
        {  
            using (SqlConnection conn   
                = new SqlConnection("context connection=true"))  
            {  
                SqlCommand command = conn.CreateCommand();  
  
                ResetCounters(4);  
  
                String parameters = String.Format(CultureInfo.InvariantCulture,  
                    "AddressLine1{0}, City, StateProvinceID, PostalCode",  
                    MaybeParameter("AddressLine2"));  
                String values = String.Format(CultureInfo.InvariantCulture,  
                "@AddressLine1{0}, @City, @StateProvinceID, @PostalCode",  
                    MaybeValue("AddressLine2"));  
  
                command.CommandText =  
                    String.Format(CultureInfo.InvariantCulture,  
                    "INSERT INTO Person.Address ({0}) VALUES ({1}); "  
                    + "SELECT CAST(SCOPE_IDENTITY() as Int);",  
                    parameters, values);  
                MaybeAddCommandParameter("AddressLine1", command,  
                    SqlDbType.NVarChar, 60, true, string.Empty);  
                MaybeAddCommandParameter("AddressLine2", command,  
                    SqlDbType.NVarChar, 60, false, null);  
                MaybeAddCommandParameter("City", command,  
                    SqlDbType.NVarChar, 30, true, string.Empty);  
                MaybeAddCommandParameter("StateProvinceID", command,  
                    SqlDbType.Int, true, string.Empty);  
                MaybeAddCommandParameter("PostalCode", command,  
                    SqlDbType.NVarChar, 15, true, string.Empty);  
                conn.Open();  
                contactDictionary["AddressID"] = command.ExecuteScalar().ToString();  
            }  
        }  
  
        public static void CreateEmployeeAdddress(int employeeId, int addressId)  
        {  
            using (SqlConnection conn   
                = new SqlConnection("context connection=true"))  
            {  
                SqlCommand cmd = conn.CreateCommand();  
                cmd.CommandText = "INSERT INTO HumanResources.EmployeeAddress "   
                    + "(EmployeeID, AddressID) VALUES (@EmployeeID, @AddressID)";  
                cmd.Parameters.AddWithValue("@EmployeeID", employeeId);  
                cmd.Parameters.AddWithValue("@AddressID", addressId);  
                conn.Open();  
                cmd.ExecuteNonQuery();  
            }  
        }  
  
        public static void CreateEmployeeDepartmentHistory(int employeeId, int departmentId, int shiftId)  
        {  
            using (SqlConnection conn   
                = new SqlConnection("context connection=true"))  
            {  
                SqlCommand cmd = conn.CreateCommand();  
                cmd.CommandText = "INSERT INTO HumanResources.EmployeeDepartmentHistory "   
                    + "(EmployeeID, DepartmentID, ShiftID, StartDate) VALUES "   
                    + "(@EmployeeID, @DepartmentID, @ShiftID, @StartDate)";  
                cmd.Parameters.AddWithValue("@EmployeeID", employeeId);  
                cmd.Parameters.AddWithValue("@DepartmentID", departmentId);  
                cmd.Parameters.AddWithValue("@ShiftID", shiftId);  
                cmd.Parameters.AddWithValue("@StartDate", DateTime.Now);  
                conn.Open();  
                cmd.ExecuteNonQuery();  
            }  
        }  
    }  
  
    /// <summary>  
    ///Used to indicate when parsing the xml document for creating a contact is   
    ///not in the proper form.  
    /// </summary>  
    [Serializable]  
    public class AWUtilitiesContactParseException : Exception  
    {  
        private String expected = "Unknown";  
  
        private String actual = "Unknown";  
  
        public String Expected  
        {  
            get  
            {  
                return expected;  
            }  
            set  
            {  
                expected = value;  
            }  
        }  
  
        public String Actual  
        {  
            get  
            {  
                return actual;  
            }  
            set  
            {  
                actual = value;  
            }  
        }  
  
        public AWUtilitiesContactParseException()  
        {  
        }  
  
        public AWUtilitiesContactParseException(String message)  
            : base(message)  
        {  
        }  
  
        public AWUtilitiesContactParseException(string message, Exception innerException)  
            : base(message, innerException)  
        {  
        }  
  
        protected AWUtilitiesContactParseException(SerializationInfo info, StreamingContext context)  
            : base(info, context)  
        {  
        }  
  
        public AWUtilitiesContactParseException(String expected, String actual)  
        {  
            this.Expected = expected;  
            this.Actual = actual;  
        }  
  
        public override String ToString()  
        {  
            return String.Format(CultureInfo.CurrentUICulture,  
                "Parsing error during contact creation, expected element {0}, found element {1}.",  
                this.Expected, this.Actual);  
        }  
  
        [System.Security.Permissions.SecurityPermission(System.Security.Permissions.SecurityAction.Demand, SerializationFormatter = true)]  
        public override void GetObjectData(SerializationInfo info, StreamingContext context)  
        {  
            // Use the method of the base class.  
            base.GetObjectData(info, context);  
        }  
    }  
  
```  
  
 VB.NET  
  
```  
      Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.IO  
Imports System.Xml  
Imports System.Collections  
Imports System.Collections.Generic  
Imports System.Globalization  
Imports Microsoft.SqlServer.Server  
Imports Microsoft.VisualBasic  
Imports System.Diagnostics  
  
Public NotInheritable Class ContactUtils  
    Private Sub New()  
    End Sub  
  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub CreateContact(ByVal contactData As SqlString, ByRef contactId As SqlInt32, ByRef customerId As SqlInt32)  
        ' TODO: When we can pass XML from T-SQL then contactData can be a SqlXmlReader  
        Using sr As New StringReader(contactData.Value)  
            Dim reader As XmlReader = XmlReader.Create(sr)  
  
            reader.MoveToContent()  
            EnsureEqual(reader.LocalName, "Contact")  
            reader.MoveToContent()  
            reader.ReadStartElement()  
  
            Dim creator As ContactCreator = Nothing  
  
            Select Case reader.LocalName  
                Case "Individual"  
                    creator = New IndividualCreator()  
  
                Case "Store"  
                    creator = New StoreCreator()  
  
                Case "Vendor"  
                    creator = New VendorCreator()  
  
                Case "Employee"  
                    creator = New EmployeeCreator()  
  
                Case Else  
            End Select  
  
            If (creator IsNot Nothing) Then  
                reader.ReadStartElement()  
                reader.MoveToContent()  
                creator.LoadDictionary(reader)  
                reader.Close()  
                creator.Create()  
                contactId = creator.ContactID  
                customerId = creator.CustomerID  
            Else  
                contactId = -1  
                customerId = -1  
  
                Throw New AWUtilsContactParseException("Individual | Store | Vendor | Employee", reader.LocalName)  
            End If  
        End Using  
    End Sub  
  
    Public Shared Sub EnsureEqual(ByVal localName As String, ByVal desiredLocalName As String)  
        If localName Is Nothing Then  
            Throw New ArgumentNullException("localName")  
        End If  
        If Not localName.Equals(desiredLocalName) Then  
            Throw New AWUtilsContactParseException(desiredLocalName, localName)  
        End If  
    End Sub  
End Class  
<Serializable()> _  
Public Class AWUtilsContactParseException  
    Inherits ApplicationException  
    Private _expected As String = "unknown"  
  
    Private _actual As String = "unknown"  
  
    Public Property Expected() As String  
        Get  
            Return _expected  
        End Get  
        Set(ByVal Value As String)  
            _expected = Value  
        End Set  
    End Property  
  
    Public Property Actual() As String  
        Get  
            Return _actual  
        End Get  
        Set(ByVal Value As String)  
            _actual = Value  
        End Set  
    End Property  
  
    Public Sub New()  
    End Sub  
  
    Public Sub New(ByVal expected As String, ByVal actual As String)  
        Me.Expected = expected  
        Me.Actual = actual  
    End Sub  
  
    Public Overrides Function ToString() As String  
        Return String.Format(System.Globalization.CultureInfo.InvariantCulture, _  
            "Parsing error during contact creation, expected element {0}, found element {1}.", _  
            Me.Expected, Me.Actual)  
    End Function  
End Class  
Public MustInherit Class CustomerCreator  
    Inherits ContactCreator  
  
    Protected Sub New()  
    End Sub  
  
    Public Overrides Sub Create()  
        MyBase.Create()  
        Using conn As New SqlConnection("context connection=true")  
            Dim command As SqlCommand = conn.CreateCommand()  
  
            If Not contactDictionary.ContainsKey("CustomerType") Then  
                contactDictionary("CustomerType") = "I"  
            End If  
  
            ResetCounters(0)  
  
            Dim parameters As String = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "{0}{1}{2}", _  
                MaybeParameter("SalesPersonID"), _  
                MaybeParameter("TerritoryID"), _  
                MaybeParameter("CustomerType"))  
            ' CustomerType is always present, but we need to get the commas right  
            Dim values As String = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "{0}{1}{2}", _  
                MaybeValue("SalesPersonID"), _  
                MaybeValue("TerritoryID"), _  
                MaybeValue("CustomerType"))  
  
            command.CommandText = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "INSERT INTO Sales.Customer ({0}) VALUES ({1}); SELECT CAST(SCOPE_IDENTITY() as Int);", _  
                parameters, values)  
            MaybeAddCommandParameter("SalesPersonID", command, SqlDbType.Int, False, Nothing)  
            MaybeAddCommandParameter("TerritoryID", command, SqlDbType.Int, False, Nothing)  
            MaybeAddCommandParameter("CustomerType", command, SqlDbType.NChar, 1, True, "I")  
            conn.Open()  
            Me.CustomerID = CType(command.ExecuteScalar(), Integer)  
        End Using  
    End Sub  
End Class  
Public MustInherit Class ContactCreator  
    Protected parameterCount As Integer  
  
    Protected valueCount As Integer  
  
    Protected contactDictionary As New Dictionary(Of String, String)()  
  
    Private Shared ReadOnly xmlColumns() As String = {"AdditionalContactInfo", "Demographics"}  
    Private Shared ReadOnly nestedColumns() As String = {"Address"}  
  
    Protected Sub New()  
    End Sub  
  
    Public Property ContactID() As Integer  
        Get  
            Dim val As String = String.Empty  
  
            If contactDictionary.TryGetValue("ContactID", val) Then  
                Return Integer.Parse(val, CultureInfo.InvariantCulture)  
            Else  
                Return -1  
            End If  
        End Get  
        Set(ByVal Value As Integer)  
            contactDictionary("ContactID") = Value.ToString(CultureInfo.InvariantCulture)  
        End Set  
    End Property  
  
    Public Property CustomerID() As Integer  
        Get  
            Dim val As String = String.Empty  
  
            If contactDictionary.TryGetValue("CustomerID", val) Then  
                Return Integer.Parse(val, CultureInfo.InvariantCulture)  
            Else  
                ' Not every contact is for a customer.  Return -1 in that case.  
                Return -1  
            End If  
        End Get  
        Set(ByVal Value As Integer)  
            contactDictionary("CustomerID") _  
                = Value.ToString(CultureInfo.InvariantCulture)  
        End Set  
    End Property  
  
    Public Sub LoadDictionary(ByVal reader As XmlReader)  
        While reader.IsStartElement()  
            Dim key As String = reader.LocalName  
            Dim val As String  
  
            If Array.IndexOf(xmlColumns, key) > -1 Then  
                val = reader.ReadInnerXml()  
            ElseIf Array.IndexOf(nestedColumns, key) > -1 Then  
                reader.ReadStartElement()  
                LoadDictionary(reader)  
                reader.ReadEndElement()  
                GoTo ContinueWhile1  
            Else  
                val = reader.ReadElementString()  
            End If  
  
            contactDictionary.Add(key, val)  
  
ContinueWhile1:  
        End While  
    End Sub  
  
    Protected Sub ResetCounters(ByVal valueForReset As Integer)  
        parameterCount = valueForReset  
        valueCount = valueForReset  
    End Sub  
  
    Public Function MaybeParameter(ByVal name As String) As String  
        If contactDictionary.ContainsKey(name) Then  
            parameterCount = parameterCount + 1  
            If parameterCount = 1 Then  
                Return name  
            Else  
                Return ", " & name  
            End If  
        Else  
            Return String.Empty  
        End If  
    End Function  
  
    Public Function MaybeValue(ByVal name As String) As String  
        If contactDictionary.ContainsKey(name) Then  
            valueCount = valueCount + 1  
            If valueCount = 1 Then  
                Return "@" & name  
            Else  
                Return ", @" & name  
            End If  
        Else  
            Return String.Empty  
        End If  
    End Function  
  
    Public Shared Function TypeConvert(ByVal valueToConvert As String, ByVal parameterType As SqlDbType) As Object  
        If valueToConvert Is Nothing Then  
            Throw New ArgumentNullException("valueToConvert")  
        End If  
        Select Case parameterType  
            Case SqlDbType.BigInt  
                Return Int64.Parse(valueToConvert, CultureInfo.InvariantCulture)  
  
            Case SqlDbType.Int  
                Return Integer.Parse(valueToConvert, CultureInfo.InvariantCulture)  
  
            Case SqlDbType.SmallInt  
                Return Int16.Parse(valueToConvert, CultureInfo.InvariantCulture)  
  
            Case SqlDbType.TinyInt  
                Return Byte.Parse(valueToConvert, CultureInfo.InvariantCulture)  
  
            Case SqlDbType.Bit  
                If valueToConvert.Equals("1") OrElse valueToConvert.Equals("true") Then  
                    Return 1  
                Else  
                    Return 0  
                End If  
  
            Case SqlDbType.NVarChar, SqlDbType.VarChar, SqlDbType.NChar, SqlDbType.NText, SqlDbType.Text, SqlDbType.Char, SqlDbType.Xml  
                Return valueToConvert  
  
            Case SqlDbType.DateTime  
                Return DateTime.Parse(valueToConvert, CultureInfo.InvariantCulture)  
  
            Case SqlDbType.Money  
                Return Decimal.Parse(valueToConvert, CultureInfo.InvariantCulture)  
  
            Case Else  
                Return "unknown conversion"  
        End Select  
    End Function  
  
    Public Overloads Sub MaybeAddCommandParameter(ByVal keyName As String, ByVal paramName As String, ByVal command As SqlCommand, ByVal parameterType As SqlDbType, ByVal isRequired As Boolean, ByVal defaultValue As String)  
        If isRequired OrElse contactDictionary.ContainsKey(keyName) Then  
            Dim param As New SqlParameter("@" & paramName, parameterType)  
            Dim val As String  
  
            If (contactDictionary.ContainsKey(keyName)) Then  
                val = contactDictionary(keyName)  
            Else  
                val = defaultValue  
            End If  
  
            param.Value = TypeConvert(val, parameterType)  
            command.Parameters.Add(param)  
        End If  
    End Sub  
  
    Public Overloads Sub MaybeAddCommandParameter(ByVal name As String, ByVal command As SqlCommand, ByVal parameterType As SqlDbType, ByVal isRequired As Boolean, ByVal defaultValue As String)  
        MaybeAddCommandParameter(name, name, command, parameterType, isRequired, defaultValue)  
    End Sub  
  
    Public Overloads Sub MaybeAddCommandParameter(ByVal name As String, ByVal command As SqlCommand, ByVal parameterType As SqlDbType, ByVal size As Integer, ByVal isRequired As Boolean, ByVal defaultValue As String)  
        If isRequired OrElse contactDictionary.ContainsKey(name) Then  
            MaybeAddCommandParameter(name, command, parameterType, isRequired, defaultValue)  
            command.Parameters(command.Parameters.Count - 1).Size = size  
        End If  
    End Sub  
  
    Public Overloads Sub MaybeAddCommandParameter(ByVal keyName As String, ByVal paramName As String, ByVal command As SqlCommand, ByVal parameterType As SqlDbType, ByVal size As Integer, ByVal isRequired As Boolean, ByVal defaultValue As String)  
        If isRequired OrElse contactDictionary.ContainsKey(keyName) Then  
            MaybeAddCommandParameter(keyName, paramName, command, parameterType, isRequired, defaultValue)  
            command.Parameters(command.Parameters.Count - 1).Size = size  
        End If  
    End Sub  
  
    Public Overridable Sub Create()  
        Using conn As New SqlConnection("context connection=true")  
  
            Dim command As SqlCommand = conn.CreateCommand()  
  
            ResetCounters(1)  
  
            Dim parameters As String = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "NameStyle{0}, FirstName{1}, LastName{2}{3}{4}{5}, PasswordHash, PasswordSalt{6}", _  
                MaybeParameter("Title"), MaybeParameter("MiddleName"), _  
                MaybeParameter("Suffix"), MaybeParameter("EmailAddress"), _  
                MaybeParameter("EmailPromotion"), MaybeParameter("Phone"), _  
                MaybeParameter("AdditionalContactInfo"))  
            Dim values As String = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "@NameStyle{0}, @FirstName{1}, @LastName{2}{3}{4}{5}, @PasswordHash, @PasswordSalt{6}", _  
                MaybeValue("Title"), MaybeValue("MiddleName"), MaybeValue("Suffix"), _  
                MaybeValue("EmailAddress"), MaybeValue("EmailPromotion"), _  
                MaybeValue("Phone"), MaybeValue("AdditionalContactInfo"))  
  
            Dim formatText As String = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "INSERT INTO Person.Contact ({0}) VALUES ({1}); SELECT CAST(SCOPE_IDENTITY() AS Int);", _  
                parameters, values)  
  
            command.CommandText = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                formatText)  
            MaybeAddCommandParameter("NameStyle", command, SqlDbType.Bit, True, "0")  
            MaybeAddCommandParameter("Title", command, SqlDbType.NVarChar, 8, False, Nothing)  
            MaybeAddCommandParameter("FirstName", command, SqlDbType.NVarChar, 50, True, String.Empty)  
            MaybeAddCommandParameter("MiddleName", command, SqlDbType.NVarChar, 50, False, Nothing)  
            MaybeAddCommandParameter("LastName", command, SqlDbType.NVarChar, 50, True, String.Empty)  
            MaybeAddCommandParameter("Suffix", command, SqlDbType.NVarChar, 10, False, Nothing)  
            MaybeAddCommandParameter("EmailAddress", command, SqlDbType.NVarChar, 50, True, String.Empty)  
            MaybeAddCommandParameter("EmailPromotion", command, SqlDbType.Int, False, Nothing)  
            MaybeAddCommandParameter("Phone", command, SqlDbType.NVarChar, 25, False, Nothing)  
            MaybeAddCommandParameter("PasswordHash", command, SqlDbType.VarChar, 40, True, String.Empty)  
            MaybeAddCommandParameter("PasswordSalt", command, SqlDbType.VarChar, 10, True, String.Empty)  
            MaybeAddCommandParameter("AdditionalContactInfo", command, SqlDbType.Xml, False, Nothing)  
            conn.Open()  
            Me.ContactID = CType(command.ExecuteScalar(), Integer)  
            Dim st As New StackTrace(True)  
        End Using  
    End Sub  
End Class  
Public Class EmployeeCreator  
    Inherits ContactCreator  
  
    Public Overrides Sub Create()  
        MyBase.Create()  
        CreateAddress()  
        Dim employeeID As Integer = -1  
        Using conn As New SqlConnection("context connection=true")  
  
            Dim command As SqlCommand = conn.CreateCommand()  
  
            ResetCounters(3)  
            Dim parameters As String = String.Format(CultureInfo.InvariantCulture, _  
                "NationalIDNumber, ContactID, LoginID{0}, Title, BirthDate, MaritalStatus, Gender, HireDate, SalariedFlag, VacationHours, SickLeaveHours", _  
                MaybeParameter("ManagerID"))  
            Dim values As String = String.Format(CultureInfo.InvariantCulture, _  
                "@NationalIDNumber, @ContactID, @LoginID{0}, @Title, @BirthDate, @MaritalStatus, @Gender, @HireDate, @SalariedFlag, @VacationHours, @SickLeaveHours", _  
                MaybeValue("ManagerID"))  
  
            command.CommandText = String.Format(CultureInfo.InvariantCulture, _  
                "INSERT INTO HumanResources.Employee ({0}) VALUES ({1}); SELECT CAST(SCOPE_IDENTITY() as Int);", _  
                parameters, values)  
            MaybeAddCommandParameter("NationalIDNumber", command, SqlDbType.NVarChar, 15, True, String.Empty)  
            MaybeAddCommandParameter("ContactID", command, SqlDbType.Int, True, String.Empty)  
            MaybeAddCommandParameter("LoginID", command, SqlDbType.NVarChar, 256, True, String.Empty)  
            MaybeAddCommandParameter("ManagerID", command, SqlDbType.Int, False, Nothing)  
            MaybeAddCommandParameter("JobTitle", "Title", command, SqlDbType.NVarChar, 50, True, String.Empty)  
            MaybeAddCommandParameter("BirthDate", command, SqlDbType.DateTime, True, String.Empty)  
            MaybeAddCommandParameter("MaritalStatus", command, SqlDbType.NChar, 1, True, String.Empty)  
            MaybeAddCommandParameter("Gender", command, SqlDbType.NChar, 1, True, String.Empty)  
            MaybeAddCommandParameter("HireDate", command, SqlDbType.DateTime, True, String.Empty)  
            MaybeAddCommandParameter("SalariedFlag", command, SqlDbType.Bit, True, "1")  
            MaybeAddCommandParameter("VacationHours", command, SqlDbType.SmallInt, True, "0")  
            MaybeAddCommandParameter("SickLeaveHours", command, SqlDbType.SmallInt, True, "0")  
            conn.Open()  
  
            employeeID = CInt(command.ExecuteScalar())  
        End Using  
  
        CreateEmployeeAdddress(employeeID, Integer.Parse(contactDictionary("AddressID"), _  
            System.Globalization.CultureInfo.InvariantCulture))  
        CreateEmployeeDepartmentHistory(employeeID, Integer.Parse( _  
            contactDictionary("DepartmentID"), _  
            System.Globalization.CultureInfo.InvariantCulture), _  
            Integer.Parse(contactDictionary("ShiftID"), _  
            System.Globalization.CultureInfo.InvariantCulture))  
    End Sub  
  
    Public Sub CreateAddress()  
        Using conn As New SqlConnection("context connection=true")  
            Dim command As SqlCommand = conn.CreateCommand()  
  
            ResetCounters(4)  
  
            Dim parameters As String = String.Format(CultureInfo.InvariantCulture, _  
                "AddressLine1{0}, City, StateProvinceID, PostalCode", _  
                MaybeParameter("AddressLine2"))  
            Dim values As String = String.Format(CultureInfo.InvariantCulture, _  
                "@AddressLine1{0}, @City, @StateProvinceID, @PostalCode", _  
                MaybeValue("AddressLine2"))  
  
            command.CommandText = String.Format(CultureInfo.InvariantCulture, _  
                "INSERT INTO Person.Address ({0}) VALUES ({1}); SELECT CAST(SCOPE_IDENTITY() as Int);", _  
                parameters, values)  
            MaybeAddCommandParameter("AddressLine1", command, SqlDbType.NVarChar, 60, True, String.Empty)  
            MaybeAddCommandParameter("AddressLine2", command, SqlDbType.NVarChar, 60, False, Nothing)  
            MaybeAddCommandParameter("City", command, SqlDbType.NVarChar, 30, True, String.Empty)  
            MaybeAddCommandParameter("StateProvinceID", command, SqlDbType.Int, True, String.Empty)  
            MaybeAddCommandParameter("PostalCode", command, SqlDbType.NVarChar, 15, True, String.Empty)  
            conn.Open()  
  
            contactDictionary("AddressID") = command.ExecuteScalar().ToString()  
        End Using  
    End Sub  
  
    Public Shared Sub CreateEmployeeAdddress(ByVal employeeID As Integer, ByVal addressID As Integer)  
        Using conn As New SqlConnection("context connection=true")  
  
            Dim cmd As SqlCommand = conn.CreateCommand()  
            cmd.CommandText = "INSERT INTO HumanResources.EmployeeAddress " + "(EmployeeID, AddressID) VALUES (@EmployeeID, @AddressID)"  
            cmd.Parameters.AddWithValue("@EmployeeID", employeeID)  
            cmd.Parameters.AddWithValue("@AddressID", addressID)  
            conn.Open()  
            cmd.ExecuteNonQuery()  
        End Using  
    End Sub  
  
    Public Shared Sub CreateEmployeeDepartmentHistory(ByVal employeeID As Integer, ByVal departmentID As Integer, ByVal shiftID As Integer)  
        Using conn As New SqlConnection("context connection=true")  
  
            Dim cmd As SqlCommand = conn.CreateCommand()  
            cmd.CommandText = "INSERT INTO HumanResources.EmployeeDepartmentHistory " + "(EmployeeID, DepartmentID, ShiftID, StartDate) VALUES " + "(@EmployeeID, @DepartmentID, @ShiftID, @StartDate)"  
            cmd.Parameters.AddWithValue("@EmployeeID", employeeID)  
            cmd.Parameters.AddWithValue("@DepartmentID", departmentID)  
            cmd.Parameters.AddWithValue("@ShiftID", shiftID)  
            cmd.Parameters.AddWithValue("@StartDate", DateTime.Now)  
            conn.Open()  
            cmd.ExecuteNonQuery()  
        End Using  
    End Sub  
End Class  
Public Class IndividualCreator  
    Inherits CustomerCreator  
  
    Public Overrides Sub Create()  
        MyBase.Create()  
        Using conn As New SqlConnection("context connection=true")  
            Dim command As SqlCommand = conn.CreateCommand()  
  
            ResetCounters(2)  
            Dim parameters As String = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "CustomerID, ContactID{0}", MaybeParameter("Demographics"))  
            Dim values As String = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "@CustomerID, @ContactID{0}", MaybeValue("Demographics"))  
            command.CommandText = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "INSERT INTO Sales.Individual ({0}) VALUES ({1});", parameters, values)  
            MaybeAddCommandParameter("CustomerID", command, SqlDbType.Int, True, String.Empty)  
            MaybeAddCommandParameter("ContactID", command, SqlDbType.Int, True, String.Empty)  
            MaybeAddCommandParameter("Demographics", command, SqlDbType.Xml, False, Nothing)  
            conn.Open()  
            command.ExecuteNonQuery()  
        End Using  
    End Sub  
End Class  
Public Class StoreCreator  
    Inherits ContactCreator  
  
    Public Overrides Sub Create()  
        MyBase.Create()  
        Using conn As New SqlConnection("context connection=true")  
  
            Dim command As SqlCommand = conn.CreateCommand()  
  
            command.CommandText = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "INSERT INTO Sales.StoreContact (CustomerID, ContactID, ContactTypeID) VALUES (@CustomerID, @ContactID, @ContactTypeID);")  
            MaybeAddCommandParameter("CustomerID", command, SqlDbType.Int, True, String.Empty)  
            MaybeAddCommandParameter("ContactID", command, SqlDbType.Int, True, String.Empty)  
            MaybeAddCommandParameter("ContactTypeID", command, SqlDbType.TinyInt, True, String.Empty)  
            conn.Open()  
            command.ExecuteNonQuery()  
        End Using  
    End Sub  
End Class  
Public Class VendorCreator  
    Inherits ContactCreator  
  
    Public Overrides Sub Create()  
        MyBase.Create()  
        Using conn As New SqlConnection("context connection=true")  
  
            Dim command As SqlCommand = conn.CreateCommand()  
  
            Dim parameters As String = "VendorID, ContactID, ContactTypeID"  
            Dim values As String = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "@VendorID, @ContactID, @ContactTypeID")  
  
            command.CommandText = String.Format( _  
                System.Globalization.CultureInfo.InvariantCulture, _  
                "INSERT INTO Purchasing.VendorContact ({0}) VALUES ({1});", _  
                parameters, values)  
            MaybeAddCommandParameter("VendorID", command, SqlDbType.Int, True, String.Empty)  
            MaybeAddCommandParameter("ContactID", command, SqlDbType.Int, True, String.Empty)  
            MaybeAddCommandParameter("ContactTypeID", command, SqlDbType.TinyInt, True, String.Empty)  
            conn.Open()  
            command.ExecuteNonQuery()  
        End Using  
    End Sub  
  
End Class  
  
```  
  
 이는 어셈블리를 배포하고 데이터베이스 내에서 저장 프로시저를 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 설치 스크립트(`Install.sql`)입니다.  
  
```tsql  
use AdventureWorks  
GO  
  
DECLARE @contactID Int;  
DECLARE @customerID Int;  
  
EXEC dbo.usp_CreateContact N'<Contact xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactData"><Individual>  
<Title>Dr.</Title>  
<FirstName>Kim</FirstName>  
<LastName>Smith</LastName>  
<EmailAddress>kim@proseware.com</EmailAddress>  
<PasswordHash>F1AF7A6028F2FEA29292C09603F1C209BB84B518</PasswordHash>  
<PasswordSalt>2Hdr7Jc=</PasswordSalt>  
<Demographics>  
<IndividualSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/IndividualSurvey">  
<TotalChildren>2</TotalChildren>  
<NumberChildrenAtHome>1</NumberChildrenAtHome>  
</IndividualSurvey>  
</Demographics>  
</Individual>  
</Contact>', @contactID OUTPUT, @customerID OUTPUT;  
  
PRINT 'Individual Contact ID = ' + CAST(@contactID as varchar(10));  
PRINT 'Individual Customer ID = ' + CAST(@customerID as varchar(10));  
  
EXEC dbo.usp_CreateContact N'  
<Contact xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactData"><Store>  
<FirstName>Catherine</FirstName>  
<LastName>Smith</LastName>  
<EmailAddress>catherine@proseware.com</EmailAddress>  
<PasswordHash>D584F3AC519BA083DD814023495F267E6A613F7C</PasswordHash>  
<PasswordSalt>bseDC8g=</PasswordSalt>  
<CustomerID>391</CustomerID>  
<ContactTypeID>14</ContactTypeID>  
</Store>  
</Contact>', @contactID OUTPUT, @customerID OUTPUT;  
  
PRINT 'Store Contact ID = ' + CAST(@contactID as varchar(10));  
PRINT 'Store Customer ID = ' + CAST(@customerID as varchar(10));  
  
EXEC dbo.usp_CreateContact N'  
<Contact xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactData"><Vendor>  
<FirstName>Amy</FirstName>  
<LastName>Smith</LastName>  
<EmailAddress>amy@proseware.com</EmailAddress>  
<PasswordHash>00753C6EEC3659B4A5C30AC048F258C610EBE248</PasswordHash>  
<PasswordSalt>wyUl4hA=</PasswordSalt>  
<VendorID>7</VendorID>  
<ContactTypeID>17</ContactTypeID>  
</Vendor>  
</Contact>', @contactID OUTPUT, @customerID OUTPUT;  
  
PRINT 'Vendor Contact ID = ' + CAST(@contactID as varchar(10));  
PRINT 'Vendor Customer ID = ' + CAST(@customerID as varchar(10));  
  
EXEC dbo.usp_CreateContact N'  
<Contact xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactData"><Employee>  
<FirstName>Ramona</FirstName>  
<LastName>Smith</LastName>  
<EmailAddress>ramona@proseware.com</EmailAddress>  
<PasswordHash>4BE320740C7461F79A3CE3E177EA03A9FE3DDD26</PasswordHash>  
<PasswordSalt>Pfz9Qzg=</PasswordSalt>  
<NationalIDNumber>739117</NationalIDNumber>  
<LoginID>ramonas</LoginID>  
<DepartmentID>11</DepartmentID>  
<ManagerID>42</ManagerID>  
<ShiftID>1</ShiftID>  
<JobTitle>Information System Specialist</JobTitle>  
<Address>  
<AddressLine1>3 Penny Lane</AddressLine1>  
<AddressLine2>Apartment 2A</AddressLine2>  
<City>Seattle</City>  
<StateProvinceID>79</StateProvinceID>  
<PostalCode>98121</PostalCode>  
</Address>  
<BirthDate>1972-04-01T03:29:17-08:00</BirthDate>  
<MaritalStatus>M</MaritalStatus>  
<Gender>F</Gender>  
<HireDate>1999-08-07T13:35:17-08:00</HireDate>  
<SalariedFlag>true</SalariedFlag>  
<VacationHours>12</VacationHours>  
<SickLeaveHours>8</SickLeaveHours>  
</Employee>  
</Contact>', @contactID OUTPUT, @customerID OUTPUT;  
  
PRINT 'Employee Contact ID = ' + CAST(@contactID as varchar(10));  
  
PRINT 'Employee Customer ID = ' + CAST(@customerID as varchar(10));  
```  
  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 데이터베이스에서 어셈블리, 저장 프로시저 및 삽입된 데이터를 제거합니다.  
  
```  
USE AdventureWorks  
GO  
--Individual  
DECLARE @ContactID int;  
DECLARE @customerID int;  
SELECT  @ContactID = co.ContactID, @customerID = c.CustomerID   
FROM Sales.Customer AS c   
JOIN Sales.Individual AS i on c.CustomerID = i.CustomerID   
JOIN Person.Contact AS co on i.ContactID = co.ContactID   
WHERE co.EmailAddress='kim@proseware.com';  
DELETE Sales.Individual WHERE ContactID = @ContactID;  
DELETE Sales.Customer WHERE CustomerID = @customerID;  
DELETE Person.Contact WHERE ContactID = @ContactID;  
GO  
  
-- Store Contact  
  
DECLARE @ContactID int;  
SELECT  @ContactID = co.ContactID   
FROM Person.Contact AS co   
WHERE co.EmailAddress='catherine@proseware.com';  
DELETE Sales.StoreContact WHERE ContactID = @ContactID;  
DELETE Person.Contact WHERE ContactID = @ContactID;  
GO  
  
-- Vendor Contact  
  
DECLARE @ContactID int;  
SELECT  @ContactID = co.ContactID FROM  Person.Contact AS co   
WHERE co.EmailAddress='amy@proseware.com';  
DELETE Purchasing.VendorContact WHERE ContactID = @ContactID;  
DELETE Person.Contact WHERE ContactID = @ContactID;  
GO  
  
-- Employee Contact  
  
DECLARE @ContactID int;  
DECLARE @EmployeeID int;  
DECLARE @AddressID int;  
SELECT  @ContactID = co.ContactID   
FROM  Person.Contact AS co   
WHERE co.EmailAddress='ramona@proseware.com';  
SELECT @EmployeeID = e.EmployeeID  
FROM HumanResources.Employee AS e  
WHERE ContactID = @ContactID;   
SELECT @AddressID = ea.AddressID  
FROM HumanResources.EmployeeAddress AS ea  
WHERE EmployeeID = @EmployeeID;  
DELETE HumanResources.EmployeeAddress   
WHERE EmployeeID = @EmployeeID AND AddressID = @AddressID;  
DELETE Person.Address  
WHERE AddressID = @AddressID;  
DELETE HumanResources.EmployeeDepartmentHistory  
WHERE EmployeeID = @EmployeeID;  
DISABLE TRIGGER [HumanResources].[dEmployee] ON [HumanResources].[Employee];  
DELETE HumanResources.Employee WHERE ContactID = @ContactID;  
ENABLE TRIGGER [HumanResources].[dEmployee] ON [HumanResources].[Employee];  
DELETE Person.Contact WHERE ContactID = @ContactID;  
GO  
  
IF EXISTS (SELECT * FROM sys.xml_schema_collections WHERE [name] = N'ContactDataSchemaCollection')  
DROP XML SCHEMA COLLECTION Person.ContactDataSchemaCollection;  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = N'usp_CreateContact')  
  
DROP PROCEDURE [dbo].[usp_CreateContact];  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = N'Contacts')   
DROP ASSEMBLY Contacts;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [공용 언어 런타임 &#40;CLR&#41; 통합에 대한 사용 시나리오 및 예제](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
