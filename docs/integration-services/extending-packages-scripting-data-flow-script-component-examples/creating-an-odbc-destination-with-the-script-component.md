---
title: "스크립트 구성 요소를 사용 하 여 ODBC 대상 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-data-flow-script-component-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5eb539f0d18f473b10ed8d49bcee9c298292fb41
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>스크립트 구성 요소를 사용하여 ODBC 대상 만들기
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], 일반적으로 데이터를 저장 ODBC 대상을 사용 하 여 프로그램 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 대상 및 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for ODBC 합니다. 그러나 단일 패키지에서 사용할 임시 ODBC 대상을 만들 수도 있습니다. 이 임시 ODBC 대상을 만들려면 다음 예와 같이 스크립트 구성 요소를 사용합니다.  
  
> [!NOTE]  
>  여러 데이터 흐름 태스크 및 여러 패키지에서 쉽게 다시 사용할 수 있는 구성 요소를 만들려면 이 스크립트 구성 요소 예제에 있는 코드를 바탕으로 사용자 지정 데이터 흐름 구성 요소를 만들어 보십시오. 자세한 내용은 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 기존 ODBC를 사용 하는 대상 구성 요소 연결 관리자를 만들려면 데이터 흐름에서 데이터를 저장 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.  
  
 이 예제는 사용자 지정의 수정된 된 버전 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 항목에 설명 된 대상 [스크립트 구성 요소를 사용 하 여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)합니다. 그러나 이 예에서 사용자 지정 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 대상은 ODBC 연결 관리자를 사용하고 데이터를 ODBC 대상에 저장하도록 수정되었습니다. 이러한 수정 내용에는 다음과 같은 변경 내용도 포함됩니다.  
  
-   호출할 수 없습니다는 **AcquireConnection** 에서 ODBC 연결 관리자의 관리 되는 메서드의 코드를 네이티브 개체를 반환 하기 때문에 있습니다. 따라서 이 예제에서는 연결 관리자의 연결 문자열을 사용하여 관리되는 ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 통해 데이터 원본에 직접 연결합니다.  
  
-   **OdbcCommand** 위치 매개 변수가 필요 합니다. 매개 변수의 위치는 명령 텍스트에서 물음표(?)로 표시됩니다. (반대로 **SqlCommand** 명명 된 매개 변수가 필요 합니다.)  
  
 사용 하 여이 예제는 **Person.Address** 테이블에 **AdventureWorks** 예제 데이터베이스. 첫 번째 및 네 번째 열 전달는  **int*AddressID** * 및 **nvarchar (30) 도시** 데이터 흐름을 통해이 테이블의 열입니다. 이 동일한 데이터 원본, 변환 및 대상 예제에는 항목에 사용 됩니다 [개발 특정 Types of Script Components](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)합니다.  
  
#### <a name="to-configure-this-script-component-example"></a>스크립트 구성 요소 예를 구성하려면  
  
1.  관리자에 연결 하는 ODBC 연결을 만듭니다는 **AdventureWorks** 데이터베이스입니다.  
  
2.  다음 TRANSACT-SQL 명령을 실행 하 여 대상 테이블을 만듭니다는 **AdventureWorks** 데이터베이스:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 대상으로 구성합니다.  
  
4.  업스트림 원본 또는 변환의 출력을 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 대상 구성 요소에 연결합니다. 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다. 하는지를 확인 하기 위해이 예제가 작동 하려면 업스트림 구성 요소의 출력에 포함 해야 적어도 **AddressID** 및 **도시** 열을는 **Person.Address** 목차는 **AdventureWorks** 예제 데이터베이스.  
  
5.  열기는 **스크립트 변환 편집기**합니다. 에 **입력 열** 선택 페이지는 **AddressID** 및 **도시** 열입니다.  
  
6.  에 **입 / 출력** 페이지에서 같은 보다 알기 쉬운 이름을 사용 하 여 입력의 이름을 바꿀 **MyAddressInput**합니다.  
  
7.  에 **연결 관리자** 페이지를 추가 하거나 ODBC 연결 관리자 설명적인 이름으로 같은 만들 **MyODBCConnectionManager**합니다.  
  
8.  에 **스크립트** 페이지 **스크립트 편집**, 다음에 아래 표시 된 스크립트를 입력 하 고는 **ScriptMain** 클래스입니다.  
  
9. 스크립트 개발 환경을 닫습니다는 **스크립트 변환 편집기**, 한 다음 샘플을 실행 합니다.  
  
    ```vb  
    Imports System.Data.Odbc  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim odbcConn As OdbcConnection  
        Dim odbcCmd As OdbcCommand  
        Dim odbcParam As OdbcParameter  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connectionString As String  
            connectionString = Me.Connections.MyODBCConnectionManager.ConnectionString  
            odbcConn = New OdbcConnection(connectionString)  
            odbcConn.Open()  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            odbcCmd = New OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
                "VALUES(?, ?)", odbcConn)  
            odbcParam = New OdbcParameter("@addressid", OdbcType.Int)  
            odbcCmd.Parameters.Add(odbcParam)  
            odbcParam = New OdbcParameter("@city", OdbcType.NVarChar, 30)  
            odbcCmd.Parameters.Add(odbcParam)  
  
        End Sub  
  
        Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
            With odbcCmd  
                .Parameters("@addressid").Value = Row.AddressID  
                .Parameters("@city").Value = Row.City  
                .ExecuteNonQuery()  
            End With  
  
        End Sub  
  
        Public Overrides Sub ReleaseConnections()  
  
            odbcConn.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.Data.Odbc;  
    ...  
    public class ScriptMain :  
        UserComponent  
    {  
        OdbcConnection odbcConn;  
        OdbcCommand odbcCmd;  
        OdbcParameter odbcParam;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            string connectionString;  
            connectionString = this.Connections.MyODBCConnectionManager.ConnectionString;  
            odbcConn = new OdbcConnection(connectionString);  
            odbcConn.Open();  
  
        }  
  
        public override void PreExecute()  
        {  
  
            odbcCmd = new OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " +  
                "VALUES(?, ?)", odbcConn);  
            odbcParam = new OdbcParameter("@addressid", OdbcType.Int);  
            odbcCmd.Parameters.Add(odbcParam);  
            odbcParam = new OdbcParameter("@city", OdbcType.NVarChar, 30);  
            odbcCmd.Parameters.Add(odbcParam);  
  
        }  
  
        public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
        {  
  
            {  
                odbcCmd.Parameters["@addressid"].Value = Row.AddressID;  
                odbcCmd.Parameters["@city"].Value = Row.City;  
                odbcCmd.ExecuteNonQuery();  
            }  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            odbcConn.Close();  
  
        }  
    }  
    ```  
  
## <a name="see-also"></a>관련 항목:  
 [스크립트 구성 요소를 사용하여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  

