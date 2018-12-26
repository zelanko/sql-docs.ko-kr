---
title: SMO에서 SQL Server 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0d54fd966594fc8219623e566f68edf65023546
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052183"
---
# <a name="configuring-sql-server-in-smo"></a>SMO에서 SQL Server 구성
  Smo에서 합니다 <xref:Microsoft.SqlServer.Management.Smo.Information> 개체를 <xref:Microsoft.SqlServer.Management.Smo.Settings> 개체를 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 설정 및 인스턴스에 대 한 정보를 포함 하는 개체 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에는 설치된 인스턴스의 동작을 설명하는 다양한 속성이 있습니다. 이러한 속성은 시작 옵션, 서버 기본값, 파일 및 디렉터리, 시스템 및 프로세서 정보, 제품 및 버전, 연결 정보, 메모리 옵션, 언어 및 데이터 정렬 선택, 인증 모드에 대해 설명합니다.  
  
## <a name="sql-server-configuration"></a>SQL Server 구성  
 합니다 <xref:Microsoft.SqlServer.Management.Smo.Information> 인스턴스에 대 한 정보를 포함 하는 개체 속성 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]프로세서 및 플랫폼과 같은 합니다.  
  
 합니다 <xref:Microsoft.SqlServer.Management.Smo.Settings> 인스턴스에 대 한 정보를 포함 하는 개체 속성 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 기본 데이터베이스 파일 및 디렉터리를 메일 프로필 및 서버 계정과 더불어 수정할 수 있습니다. 이러한 속성은 연결 기간 동안 유지됩니다.  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 개체 속성은 산술 연산, ANSI 표준 및 트랜잭션과 관련된 현재 연결 동작에 대한 정보를 포함합니다.  
  
 일련의 구성 옵션으로 표시 되는 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 개체입니다. 이 개체는 `sp_configure` 저장 프로시저로 수정할 수 있는 옵션을 나타내는 일련의 속성을 포함합니다. 와 같은 옵션 **우선 순위 높임**, **복구 간격** 하 고 **Network Packet Size**인스턴스의 성능을 제어 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 이러한 옵션은 대부분 동적으로 변경할 수 있지만, 먼저 값이 구성된 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스가 다시 시작될 때 변경되는 경우도 있습니다.  
  
 한 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 모든 구성 옵션에 대 한 속성 개체입니다. <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 개체를 사용하여 전역 구성 설정을 수정할 수 있습니다. 대부분의 속성에는 최대값 및 최소값이 있으며 이것 역시 <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> 속성으로 저장됩니다. 이러한 속성에는 필요 합니다 <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A> 인스턴스의 변경 내용을 커밋하려면 메서드 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
 모든 구성 옵션을 <xref:Microsoft.SqlServer.Management.Smo.Configuration> 시스템 관리자가 개체를 변경 해야 합니다.  
  
## <a name="examples"></a>예  
 다음 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 및 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>Visual Basic에서 SQL Server 구성 옵션 수정  
 코드 예제는 Visual Basic .NET에서 구성 옵션을 업데이트하는 방법을 보여 줍니다. 또한 지정된 구성 옵션에 대한 최대값 및 최소값 정보를 검색하고 표시합니다. 마지막으로 프로그램 사용자에 게 알려 변경 내용을 동적으로 수행 된 경우 또는 인스턴스의까지 저장 되어 있는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다시 시작 됩니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure2](SMO How to#SMO_VBConfigure2)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>Visual Basic에서 SQL Server 설정 수정  
 인스턴스에 대 한 정보를 표시 하는 코드 예제 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 <xref:Microsoft.SqlServer.Management.Smo.Information> 하 고 <xref:Microsoft.SqlServer.Management.Smo.Settings>에서 설정을 수정 <xref:Microsoft.SqlServer.Management.Smo.Settings> 및 <xref:Microsoft.SqlServer.Management.Smo.UserOptions>개체 속성입니다.  
  
 이 예에서 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.Settings> 개체에는 모두 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 메서드가 있습니다. 실행할 수 있습니다는 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 이러한 메서드에 개별적으로 합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure1](SMO How to#SMO_VBConfigure1)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>Visual C#에서 SQL Server 설정 수정  
 인스턴스에 대 한 정보를 표시 하는 코드 예제 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 <xref:Microsoft.SqlServer.Management.Smo.Information> 하 고 <xref:Microsoft.SqlServer.Management.Smo.Settings>에서 설정을 수정 <xref:Microsoft.SqlServer.Management.Smo.Settings> 및 <xref:Microsoft.SqlServer.Management.Smo.UserOptions>개체 속성입니다.  
  
 이 예에서 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.Settings> 개체에는 모두 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 메서드가 있습니다. 실행할 수 있습니다는 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 이러한 메서드에 개별적으로 합니다.  
  
 `//Connect to the local, default instance of SQL Server.`  
  
```  
{  
            Server srv = new Server();  
            //Display all the configuration options.   
  
            foreach (ConfigProperty p in srv.Configuration.Properties)  
            {  
                Console.WriteLine(p.DisplayName);  
            }  
            Console.WriteLine("There are " + srv.Configuration.Properties.Count.ToString() + " configuration options.");  
            //Display the maximum and minimum values for ShowAdvancedOptions.   
            int min = 0;  
            int max = 0;  
            min = srv.Configuration.ShowAdvancedOptions.Minimum;  
            max = srv.Configuration.ShowAdvancedOptions.Maximum;  
            Console.WriteLine("Minimum and Maximum values are " + min + " and " + max + ".");  
            //Modify the value of ShowAdvancedOptions and run the Alter method.   
            srv.Configuration.ShowAdvancedOptions.ConfigValue = 0;  
            srv.Configuration.Alter();  
            //Display when the change takes place according to the IsDynamic property.   
            if (srv.Configuration.ShowAdvancedOptions.IsDynamic == true)  
            {  
                Console.WriteLine("Configuration option has been updated.");  
            }  
            else  
            {  
                Console.WriteLine("Configuration option will be updated when SQL Server is restarted.");  
            }  
        }  
```  
  
## <a name="modifying-sql-server-settings-in-powershell"></a>PowerShell에서 SQL Server 설정 수정  
 인스턴스에 대 한 정보를 표시 하는 코드 예제 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 <xref:Microsoft.SqlServer.Management.Smo.Information> 하 고 <xref:Microsoft.SqlServer.Management.Smo.Settings>에서 설정을 수정 <xref:Microsoft.SqlServer.Management.Smo.Settings> 및 <xref:Microsoft.SqlServer.Management.Smo.UserOptions>개체 속성입니다.  
  
 이 예에서 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> 개체 및 <xref:Microsoft.SqlServer.Management.Smo.Settings> 개체에는 모두 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 메서드가 있습니다. 실행할 수 있습니다는 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> 이러한 메서드에 개별적으로 합니다.  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Display information about the instance of SQL Server in Information and Settings.  
"OS Version = " + $srv.Information.OSVersion  
"State = "+ $srv.Settings.State.ToString()  
  
#Display information specific to the current user in UserOptions.  
"Quoted Identifier support = " + $srv.UserOptions.QuotedIdentifier  
  
#Modify server settings in Settings.  
$srv.Settings.LoginMode = [Microsoft.SqlServer.Management.SMO.ServerLoginMode]::Integrated  
  
#Modify settings specific to the current connection in UserOptions.  
$srv.UserOptions.AbortOnArithmeticErrors = $true  
  
#Run the Alter method to make the changes on the instance of SQL Server.  
$srv.Alter()  
```  
  
## <a name="modifying-sql-server-configuration-options-in-powershell"></a>PowerShell에서 SQL Server 구성 옵션 수정  
 코드 예제는 Visual Basic .NET에서 구성 옵션을 업데이트하는 방법을 보여 줍니다. 또한 지정된 구성 옵션에 대한 최대값 및 최소값 정보를 검색하고 표시합니다. 마지막으로 프로그램 사용자에 게 알려 변경 내용을 동적으로 수행 된 경우 또는 인스턴스의까지 저장 되어 있는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다시 시작 됩니다.  
  
```  
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = get-item default  
  
#enumerate its properties  
foreach ($Item in $Svr.Configuration.Properties)   
{  
 $Item.DisplayName  
}  
  
"There are " + $svr.Configuration.Properties.Count.ToString() + " configuration options."  
  
#Display the maximum and minimum values for ShowAdvancedOptions.  
$min = $svr.Configuration.ShowAdvancedOptions.Minimum  
$max = $svr.Configuration.ShowAdvancedOptions.Maximum  
"Minimum and Maximum values are " + $min.ToString() + " and " + $max.ToString() + "."  
  
#Modify the value of ShowAdvancedOptions and run the Alter method.  
$svr.Configuration.ShowAdvancedOptions.ConfigValue = 0  
$svr.Configuration.Alter()  
  
#Display when the change takes place according to the IsDynamic property.  
If ($svr.Configuration.ShowAdvancedOptions.IsDynamic -eq $true)  
 {    
   "Configuration option has been updated."  
 }  
Else  
{  
    "Configuration option will be updated when SQL Server is restarted."  
}  
```  
  
  
