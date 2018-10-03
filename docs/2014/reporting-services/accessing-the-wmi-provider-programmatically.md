---
title: WMI 공급자에 프로그래밍 방식으로 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
ms.assetid: 67bd266b-1484-4863-8152-060a993420a9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8eeb349c91dd87175f8baaabad75acccc8a622d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094999"
---
# <a name="accessing-the-wmi-provider-programmatically"></a>WMI공급자에 프로그래밍 방식으로 액세스
  [항목 작성 중]  
  
## <a name="wmi-provider-overview"></a>WMI 공급자 개요  
 이 항목에 표시된 코드 예제의 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에 대한 정보를 얻는 데 사용되는 네임스페이스는 **System.Management** 네임스페이스이며 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]에서 찾을 수 있습니다. **System.Management** 네임스페이스는 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 응용 프로그램에서 관리 정보를 액세스하고 조작하는 데 사용할 수 있는 관리 코드 클래스 집합을 제공합니다. **System.Management** 네임스페이스를 사용하여 Reporting Services WMI 클래스를 사용하는 방법은 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK의 "System.Management를 사용하여 관리 정보 액세스"를 참조하십시오.  
  
## <a name="finding-a-report-server-instance"></a>보고서 서버 인스턴스 찾기  
 보고서 서버 설치에 대한 정보를 찾을 때는 WMI 인스턴스 컬렉션을 열거하는 것이 좋습니다. 아래 예는 컬렉션을 만들고 이 컬렉션을 반복하여 속성을 표시하는 방법으로 모든 보고서 서버 인스턴스에 대한 속성을 찾는 방법을 보여 줍니다.  
  
```vb  
Imports System  
Imports System.Management  
Imports System.IO  
  
Module Module1  
    Sub Main()  
        Const WmiNamespace As String = "\\<ServerName>\root\Microsoft\SqlServer\ReportServer\<InstanceName>\v10\Admin"  
        Const WmiRSClass As String = _  
           "\\<ServerName>\root\Microsoft\SqlServer\ReportServer\<InstanceName>\v10\admin:MSReportServer_ConfigurationSetting"  
  
        Dim serverClass As ManagementClass  
        Dim scope As ManagementScope  
        scope = New ManagementScope(WmiNamespace)  
        'Connect to the Reporting Services namespace.  
        scope.Connect()  
  
        'Create the server class.  
        serverClass = New ManagementClass(WmiRSClass)  
        'Connect to the management object.  
        serverClass.Get()  
        If serverClass Is Nothing Then Throw New Exception("No class found")  
  
        'Loop through the instances of the server class.  
        Dim instances As ManagementObjectCollection = serverClass.GetInstances()  
        Dim instance As ManagementObject  
        For Each instance In instances  
            Console.Out.WriteLine("Instance Detected")  
            Dim instProps As PropertyDataCollection = instance.Properties  
            Dim prop As PropertyData  
            For Each prop In instProps  
                Dim name As String = prop.Name  
                Dim val As Object = prop.Value  
                Console.Out.Write("Property Name: " + name)  
                If val Is Nothing Then  
                    Console.Out.WriteLine("     Value: <null>")  
                Else  
                    Console.Out.WriteLine("     Value: " + val.ToString())  
                End If  
            Next  
        Next  
  
        Console.WriteLine("--- Press any key ---")  
        Console.ReadKey()  
  
    End Sub  
End Module  
```  
  
```csharp  
using System;  
using System.Management;  
using System.IO;  
[assembly: CLSCompliant(true)]  
  
class Class1  
{  
    [STAThread]  
    static void Main(string[] args)  
    {  
        const string WmiNamespace = @"\\<ServerName>\root\Microsoft\SqlServer\ReportServer\<InstanceName>\v10\Admin";  
        const string WmiRSClass =  
          @"\\<ServerName>\root\Microsoft\SqlServer\ReportServer\<InstanceName>\v10\admin:MSReportServer_ConfigurationSetting";  
        ManagementClass serverClass;  
        ManagementScope scope;  
        scope = new ManagementScope(WmiNamespace);  
  
        // Connect to the Reporting Services namespace.  
        scope.Connect();  
        // Create the server class.  
        serverClass = new ManagementClass(WmiRSClass);  
        // Connect to the management object.  
        serverClass.Get();  
        if (serverClass == null)  
            throw new Exception("No class found");  
  
        // Loop through the instances of the server class.  
        ManagementObjectCollection instances = serverClass.GetInstances();  
  
        foreach (ManagementObject instance in instances)  
        {  
            Console.Out.WriteLine("Instance Detected");  
            PropertyDataCollection instProps = instance.Properties;  
            foreach (PropertyData prop in instProps)  
            {  
                string name = prop.Name;  
                object val = prop.Value;  
                Console.Out.Write("Property Name: " + name);  
                if (val != null)  
                    Console.Out.WriteLine("     Value: " + val.ToString());  
                else  
                    Console.Out.WriteLine("     Value: <null>");  
            }  
        }  
        Console.WriteLine("\n--- Press any key ---");  
        Console.ReadKey();  
    }  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services WMI 공급자 액세스](tools/access-the-reporting-services-wmi-provider.md)   
 [RSReportServer 구성 파일](report-server/rsreportserver-config-configuration-file.md)  
  
  
