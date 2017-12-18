---
title: "스크립트 태스크에서 데이터 원본에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs: VB
helpviewer_keywords:
- connections [Integration Services], scripts
- Integration Services packages, connections
- connection managers [Integration Services], scripts
- scripts [Integration Services], connections
- SSIS packages, connections
- packages [Integration Services], connections
- Script task [Integration Services], connections
- Connections property
- SQL Server Integration Services packages, connections
- SSIS Script task, connections
ms.assetid: 9c008380-715b-455b-9da7-22572d67c388
caps.latest.revision: "59"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 052113c5e6f18381a26d9a3a7f1703659a40a88e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="connecting-to-data-sources-in-the-script-task"></a>스크립트 태스크에서 데이터 원본에 연결
  연결 관리자를 사용하면 패키지에 구성된 데이터 원본에 액세스할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 연결](../../../integration-services/connection-manager/integration-services-ssis-connections.md)을 참조하세요.  
  
 스크립트 태스크에서는 **Dts** 개체의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 속성을 통해 이러한 연결 관리자에 액세스합니다. <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 컬렉션의 각 연결 관리자는 기본 데이터 원본에 연결하는 방법에 대한 정보를 저장합니다.  
  
 연결 관리자의 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> 메서드를 호출하면 해당 연결 관리자는 데이터 원본이 아직 연결되어 있지 않은 경우 데이터 원본에 연결하고 개발자가 스크립트 태스크 코드에서 사용할 수 있는 적절한 연결 및 연결 정보를 반환합니다.  
  
> [!NOTE]  
>  **AcquireConnection**을 호출하려면 먼저 연결 관리자에서 반환하는 연결 형식을 알고 있어야 합니다. 스크립트 태스크에는 **Option Strict**가 설정되어 있으므로 **개체** 형식으로 반환된 연결을 사용하려면 먼저 이 연결을 적절한 연결 형식으로 캐스팅해야 합니다.  
  
 코드에서 연결을 사용하기 전에 <xref:Microsoft.SqlServer.Dts.Runtime.Connections.Contains%2A> 속성에서 반환된 <xref:Microsoft.SqlServer.Dts.Runtime.Connections> 컬렉션의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> 메서드를 사용하여 기존 연결을 찾을 수 있습니다.  
  
> [!IMPORTANT]  
>  스크립트 태스크의 관리 코드에서는 OLE DB 연결 관리자 및 Excel 연결 관리자와 같이 관리되지 않는 개체를 반환하는 연결 관리자의 AcquireConnection 메서드를 호출할 수 없습니다. 그러나 이러한 연결 관리자의 ConnectionString 속성을 읽고 **System.Data.OleDb** 네임스페이스에서 OLEDB **OledbConnection**의 연결 문자열을 사용하여 코드에서 직접 데이터 원본에 연결할 수 있습니다.  
>   
>  관리되지 않는 개체를 반환하는 연결 관리자의 AcquireConnection 메서드를 호출해야 하는 경우에는 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 연결 관리자를 사용합니다. [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 연결 관리자에서 OLE DB 공급자를 사용하도록 구성할 경우 이 연결 관리자는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Data Provider for OLE DB를 사용하여 연결합니다. 이 경우 AcquireConnection 메서드는 관리되지 않는 개체 대신 **System.Data.OleDb.OleDbConnection**을 반환합니다. [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 연결 관리자를 Excel 데이터 원본에 사용할 수 있도록 구성하려면 **연결 관리자** 대화 상자의 **모두** 페이지에서 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB Provider for Jet를 선택하고 Excel 파일을 지정한 다음 **확장 속성** 값으로 `Excel 8.0`(Excel 97 이상의 경우)을 입력합니다.  
  
## <a name="connections-example"></a>연결 예  
 다음 예에서는 스크립트 태스크 내에서 연결 관리자에 액세스하는 방법을 보여 줍니다. 이 예제에서는 **Test ADO.NET Connection**이라는 [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 연결 관리자와 **플랫 파일 연결 관리자**라는 플랫 파일 연결 관리자를 만들고 구성했다고 가정합니다. [!INCLUDE[vstecado](../../../includes/vstecado-md.md)] 연결 관리자는 데이터 원본에 즉시 연결하는 데 사용할 수 있는 **SqlConnection** 개체를 반환합니다. 반면에 플랫 파일 연결 관리자는 경로와 파일 이름이 들어 있는 문자열만 반환합니다. 플랫 파일을 열어 작업하려면 **System.IO** 네임스페이스의 메서드를 사용해야 합니다.  
  
```vb  
Public Sub Main()  
  
    Dim myADONETConnection As SqlClient.SqlConnection  
    myADONETConnection = _  
        DirectCast(Dts.Connections("Test ADO.NET Connection").AcquireConnection(Dts.Transaction), _  
        SqlClient.SqlConnection)  
    MsgBox(myADONETConnection.ConnectionString, _  
        MsgBoxStyle.Information, "ADO.NET Connection")  
  
    Dim myFlatFileConnection As String  
    myFlatFileConnection = _  
        DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _  
        String)  
    MsgBox(myFlatFileConnection, MsgBoxStyle.Information, "Flat File Connection")  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
  
public class ScriptMain  
{  
  
        public void Main()  
        {  
            SqlConnection myADONETConnection = new SqlConnection();  
            myADONETConnection = (SqlConnection)(Dts.Connections["Test ADO.NET Connection"].AcquireConnection(Dts.Transaction)as SqlConnection);  
            MessageBox.Show(myADONETConnection.ConnectionString, "ADO.NET Connection");  
  
            string myFlatFileConnection;  
            myFlatFileConnection = (string)(Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);  
            MessageBox.Show(myFlatFileConnection, "Flat File Connection");  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services&#40;SSIS&#41; 연결](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [연결 관리자 만들기](http://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
