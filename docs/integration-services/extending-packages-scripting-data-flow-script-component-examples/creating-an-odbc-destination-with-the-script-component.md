---
title: 스크립트 구성 요소를 사용하여 ODBC 대상 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bb28965af992a19864ccf2e6959decd778468403
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296497"
---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>스크립트 구성 요소를 사용하여 ODBC 대상 만들기

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 일반적으로 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 대상 및 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for ODBC를 사용하여 ODBC 대상에 데이터를 저장합니다. 그러나 단일 패키지에서 사용할 임시 ODBC 대상을 만들 수도 있습니다. 이 임시 ODBC 대상을 만들려면 다음 예와 같이 스크립트 구성 요소를 사용합니다.  
  
> [!NOTE]  
>  여러 데이터 흐름 태스크 및 여러 패키지에서 쉽게 다시 사용할 수 있는 구성 요소를 만들려면 이 스크립트 구성 요소 예제에 있는 코드를 바탕으로 사용자 지정 데이터 흐름 구성 요소를 만들어 보십시오. 자세한 내용은 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서는 기존 ODBC 연결 관리자를 사용하여 데이터 흐름에서 받은 데이터를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장하는 대상 구성 요소를 만드는 방법을 보여 줍니다.  
  
 이 예는 [스크립트 구성 요소를 사용하여 대상 만들기](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md) 항목에서 예로 보여 준 사용자 지정 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 대상의 수정된 버전입니다. 그러나 이 예에서 사용자 지정 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 대상은 ODBC 연결 관리자를 사용하고 데이터를 ODBC 대상에 저장하도록 수정되었습니다. 이러한 수정 내용에는 다음과 같은 변경 내용도 포함됩니다.  
  
-   ODBC 연결 관리자의 **AcquireConnection** 메서드는 네이티브 개체를 반환하므로 관리 코드에서 이 메서드를 호출할 수 없습니다. 따라서 이 예제에서는 연결 관리자의 연결 문자열을 사용하여 관리되는 ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 통해 데이터 원본에 직접 연결합니다.  
  
-   **OdbcCommand**에는 위치 매개 변수가 필요합니다. 매개 변수의 위치는 명령 텍스트에서 물음표(?)로 표시됩니다. (반면 **SqlCommand**에는 명명된 매개 변수가 필요합니다.)  
  
 이 예에서는 **AdventureWorks** 예제 데이터베이스의 **Person.Address** 테이블을 사용하고, 이 테이블의 첫 번째 열인 **int _AddressID_** 와 네 번째 열인 **nvarchar(30) _City_** 열을 데이터 흐름을 통해 전달합니다. 동일한 데이터가 [특정 유형의 스크립트 구성 요소 개발](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md) 항목의 원본, 변환 및 대상 예제에도 사용됩니다.  
  
#### <a name="to-configure-this-script-component-example"></a>스크립트 구성 요소 예를 구성하려면  
  
1.  **AdventureWorks** 데이터베이스에 연결하는 ODBC 연결 관리자를 만듭니다.  
  
2.  **AdventureWorks** 데이터베이스에서 다음 Transact-SQL 명령을 실행하여 대상 테이블을 만듭니다.  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  데이터 흐름 디자이너 화면에 새 스크립트 구성 요소를 추가하고 이 구성 요소를 대상으로 구성합니다.  
  
4.  업스트림 원본 또는 변환의 출력을 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 대상 구성 요소에 연결합니다. 변환하지 않고 원본을 대상에 직접 연결할 수 있습니다. 이 예제가 작동하려면 업스트림 구성 요소의 출력에는 **AdventureWorks** 예제 데이터베이스의 **Person.Address** 테이블에서 적어도 **AddressID** 및 **City** 열이 포함되어야 합니다.  
  
5.  **스크립트 변환 편집기**를 엽니다. **입력 열** 페이지에서 **AddressID** 및 **City** 열을 선택합니다.  
  
6.  **입/출력** 페이지에서 입력의 이름을 **MyAddressInput**과 같이 더 알기 쉬운 이름으로 바꿉니다.  
  
7.  **연결 관리자** 페이지에서 **MyODBCConnectionManager**와 같이 알기 쉬운 이름으로 ODBC 연결 관리자를 추가하거나 만듭니다.  
  
8.  **스크립트** 페이지에서 **스크립트 편집**을 클릭한 다음 아래의 **ScriptMain** 클래스에 표시된 스크립트를 입력합니다.  
  
9. 스크립트 개발 환경을 닫고 **스크립트 변환 편집기**를 닫은 다음 예제를 실행합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [스크립트 구성 요소를 사용하여 대상 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  
