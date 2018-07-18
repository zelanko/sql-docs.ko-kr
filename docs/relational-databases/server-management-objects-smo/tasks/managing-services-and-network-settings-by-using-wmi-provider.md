---
title: WMI 공급자를 사용 하 여 서비스 및 네트워크 설정 관리 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- WMI provider [SMO]
- services [SQL Server], SMO
- network settings [SMO]
- monitoring [SMO]
ms.assetid: ef8c3986-1098-4f21-b03a-f1f6bdb51c26
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 77eef3609246b60c7a49adcde9ee72498bb6f215
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031631"
---
# <a name="managing-services-and-network-settings-by-using-wmi-provider"></a>WMI 공급자를 사용하여 서비스 및 네트워크 설정 관리
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  WMI 공급자가 사용 되는 게시 된 인터페이스 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Management Console (MMC)를 관리 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 및 네트워크 프로토콜입니다. Smo에서 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체가 WMI 공급자를 나타냅니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체와 설정 된 연결과 독립적으로 작동 합니다 <xref:Microsoft.SqlServer.Management.Smo.Server> 개체의 인스턴스를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Windows 자격 증명을 사용 하 여 WMI 서비스에 연결 하 고 합니다.  
  
## <a name="example"></a>예제  
제공된 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  

  
 사용 하는 프로그램에 대해 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 포함 해야 WMI 공급자는 **가져오기** WMI 네임 스페이스를 정규화 하는 문. 다음과 같이 응용 프로그램의 선언 앞에, 다른 **Imports** 문 끝에 구문을 삽입하십시오.  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Wmi`  
  
## <a name="stopping-and-restarting-the-microsoft-sql-server-service-to-the-instance-of-sql-server-in-visual-basic"></a>Visual Basic에서 SQL Server 인스턴스에 대한 Microsoft SQL Server 서비스 중지 및 다시 시작  
 이 코드 예제는 SMO <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체를 사용하여 서비스를 중지하고 시작하는 방법을 보여 줍니다. 이를 통해 구성 관리용 WMI 공급자에 대한 인터페이스를 제공합니다.  
  
```VBNET
'Declare and create an instance of the ManagedComputer object that represents the WMI Provider services.
Dim mc As ManagedComputer
mc = New ManagedComputer()
'Iterate through each service registered with the WMI Provider.
Dim svc As Service
For Each svc In mc.Services
    Console.WriteLine(svc.Name)
Next
'Reference the Microsoft SQL Server service.
svc = mc.Services("MSSQLSERVER")
'Stop the service if it is running and report on the status continuously until it has stopped.
If svc.ServiceState = ServiceState.Running Then
    svc.Stop()

    Console.WriteLine(String.Format("{0} service state is {1}", svc.Name, svc.ServiceState))
    Do Until String.Format("{0}", svc.ServiceState) = "Stopped"
        Console.WriteLine(String.Format("{0}", svc.ServiceState))
        svc.Refresh()
    Loop
    Console.WriteLine(String.Format("{0} service state is {1}", svc.Name, svc.ServiceState))
    'Start the service and report on the status continuously until it has started.
    svc.Start()
    Do Until String.Format("{0}", svc.ServiceState) = "Running"
        Console.WriteLine(String.Format("{0}", svc.ServiceState))
        svc.Refresh()
    Loop
    Console.WriteLine(String.Format("{0} service state is {1}", svc.Name, svc.ServiceState))

Else
    Console.WriteLine("SQL Server service is not running.")
End If
```
  
## <a name="enabling-a-server-protocol-using-a-urn-string-in-visual-basic"></a>Visual Basic에서 URN 문자열을 사용하여 서버 프로토콜 활성화  
 코드 예제는 URN 개체를 사용하여 서버 프로토콜을 식별한 다음 프로토콜을 활성화하는 방법을 보여 줍니다.  
  
```VBNET  
'This program must run with administrator privileges.  
        'Declare the ManagedComputer WMI interface.  
        Dim mc As New ManagedComputer()  
  
        'Create a URN object that represents the TCP server protocol.  
        Dim u As New Urn("ManagedComputer[@Name='V-ROBMA3']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']")  
  
        'Declare the serverProtocol variable and return the ServerProtocol object.  
        Dim sp As ServerProtocol  
        sp = mc.GetSmoObject(u)  
  
        'Enable the protocol.  
        sp.IsEnabled = True  
  
        'propagate back to the service  
        sp.Alter()  
```  
  
## <a name="enabling-a-server-protocol-using-a-urn-string-in-powershell"></a>PowerShell에서 URN 문자열을 사용하여 서버 프로토콜 활성화  
 코드 예제는 URN 개체를 사용하여 서버 프로토콜을 식별한 다음 프로토콜을 활성화하는 방법을 보여 줍니다.  
  
```powershell  
#This example shows how to identify a server protocol using a URN object, and then enable the protocol  
#This program must run with administrator privileges.  
  
#Load the assembly containing the classes used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlWmiManagement")  
  
#Get a managed computer instance  
$mc = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer  
  
#Create a URN object that represents the TCP server protocol  
#Change 'MyPC' to the name of the your computer   
$urn = New-Object -TypeName Microsoft.SqlServer.Management.Sdk.Sfc.Urn -argumentlist "ManagedComputer[@Name='MyPC']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
  
#Get the protocol object  
$sp = $mc.GetSmoObject($urn)  
  
#enable the protocol on the object  
$sp.IsEnabled = $true  
  
#propagate back to actual service  
$sp.Alter()  
```  
  
## <a name="starting-and-stopping-a-service-in-visual-c"></a>Visual C#에서 서비스 시작 및 중지  
 이 코드 예제는 SQL Server 인스턴스를 중지 및 시작하는 방법을 보여 줍니다.  
  
```csharp  
{   
   //Declare and create an instance of the ManagedComputer   
   //object that represents the WMI Provider services.   
   ManagedComputer mc;   
   mc = new ManagedComputer();   
   //Iterate through each service registered with the WMI Provider.   
  
   foreach (Service svc in mc.Services)  
   {   
      Console.WriteLine(svc.Name);   
   }   
//Reference the Microsoft SQL Server service.   
  Service Mysvc = mc.Services["MSSQLSERVER"];   
//Stop the service if it is running and report on the status  
// continuously until it has stopped.   
   if (Mysvc.ServiceState == ServiceState.Running) {   
      Mysvc.Stop();   
      Console.WriteLine(string.Format("{0} service state is {1}", Mysvc.Name, Mysvc.ServiceState));   
      while (!(string.Format("{0}", Mysvc.ServiceState) == "Stopped")) {   
         Console.WriteLine(string.Format("{0}", Mysvc.ServiceState));   
          Mysvc.Refresh();   
      }   
      Console.WriteLine(string.Format("{0} service state is {1}", Mysvc.Name, Mysvc.ServiceState));   
//Start the service and report on the status continuously   
//until it has started.   
      Mysvc.Start();   
      while (!(string.Format("{0}", Mysvc.ServiceState) == "Running")) {   
         Console.WriteLine(string.Format("{0}", Mysvc.ServiceState));   
         Mysvc.Refresh();   
      }   
      Console.WriteLine(string.Format("{0} service state is {1}", Mysvc.Name, Mysvc.ServiceState));  
      Console.ReadLine();  
   }   
   else {   
      Console.WriteLine("SQL Server service is not running.");  
      Console.ReadLine();  
   }   
}  
```  
  
## <a name="starting-and-stopping-a-service-in-powershell"></a>PowerShell에서 서비스 시작 및 중지  
 이 코드 예제는 SQL Server 인스턴스를 중지 및 시작하는 방법을 보여 줍니다.  
  
```powershell  
#Load the assembly containing the objects used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlWmiManagement")  
  
#Get a managed computer instance  
$mc = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer  
  
#List out all sql server instnces running on this mc  
foreach ($Item in $mc.Services){$Item.Name}  
  
#Get the default sql server datbase engine service  
$svc = $mc.Services["MSSQLSERVER"]  
  
# for stopping and starting services PowerShell must run as administrator  
  
#Stop this service  
$svc.Stop()  
$svc.Refresh()  
while ($svc.ServiceState -ne "Stopped")  
{  
$svc.Refresh()  
$svc.ServiceState  
}  
"Service" + $svc.Name + " is now stopped"  
"Starting " + $svc.Name  
$svc.Start()  
$svc.Refresh()  
while ($svc.ServiceState -ne "Running")  
{  
$svc.Refresh()  
$svc.ServiceState  
}  
$svc.ServiceState  
"Service" + $svc.Name + "is now started"  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [구성 관리용 WMI 공급자 개념](../../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  
