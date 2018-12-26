---
title: SQL Server 에이전트에서 자동 관리 태스크 예약 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- scheduling administrative tasks [SMO]
- SQL Server Agent [SMO]
- automatic administrative SMO tasks
ms.assetid: 900242ad-d6a2-48e9-8a1b-f0eea4413c16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cffe92028d392c825616bf8b189508e86fd15077
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074573"
---
# <a name="scheduling-automatic-administrative-tasks-in-sql-server-agent"></a>SQL Server 에이전트에서 자동 관리 태스크 예약
  SMO에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트는 다음 개체로 표시됩니다.  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer> 개체에는 작업, 경고, 운영자의 세 가지 컬렉션이 있습니다.  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCollection> 개체는 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트로부터 자동으로 이벤트 알림을 받을 수 있는 호출기, 전자 메일 주소 및 net send 운영자 목록을 나타냅니다.  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCollection> 개체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 모니터링되는 시스템 이벤트나 성능 조건과 같은 상황 목록을 나타냅니다.  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCollection> 개체는 약간 더 복잡합니다. 이 개체는 지정된 일정에서 실행되는 다단계 태스크 목록을 나타냅니다. 단계 및 일정 정보는 <xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep> 및 <xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule> 개체에 저장됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 개체는 <xref:Microsoft.SqlServer.Management.Smo.Agent> 네임스페이스에 있습니다.  
  
## <a name="examples"></a>예  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 또는 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트를 사용하는 프로그램에 대해 에이전트 네임스페이스를 한정하는 `Imports` 문을 포함해야 합니다. 다음과 같이 응용 프로그램의 선언 앞에, 다른 `Imports` 문 끝에 구문을 삽입하십시오.  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Agent`  
  
## <a name="creating-a-job-with-steps-and-a-schedule-in-visual-basic"></a>Visual Basic에서 단계와 일정이 포함된 작업 만들기  
 이 코드 예제는 단계와 일정이 포함된 작업을 만든 다음 운영자에게 알립니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBAgent1](SMO How to#SMO_VBAgent1)]  -->  
  
## <a name="creating-a-job-with-steps-and-a-schedule-in-visual-c"></a>Visual C#에서 단계와 일정이 포함된 작업 만들기  
 이 코드 예제는 단계와 일정이 포함된 작업을 만든 다음 운영자에게 알립니다.  
  
```  
{  
            //Connect to the local, default instance of SQL Server.  
            Server srv = new Server();  
  
            //Define an Operator object variable by supplying the Agent (parent JobServer object) and the name in the constructor.   
            Operator op = new Operator(srv.JobServer, "Test_Operator");  
  
            //Set the Net send address.   
            op.NetSendAddress = "Network1_PC";  
  
            //Create the operator on the instance of SQL Server Agent.   
            op.Create();  
  
            //Define a Job object variable by supplying the Agent and the name arguments in the constructor and setting properties.   
            Job jb = new Job(srv.JobServer, "Test_Job");  
  
            //Specify which operator to inform and the completion action.   
            jb.OperatorToNetSend = "Test_Operator";  
            jb.NetSendLevel = CompletionAction.Always;  
  
            //Create the job on the instance of SQL Server Agent.   
            jb.Create();  
  
            //Define a JobStep object variable by supplying the parent job and name arguments in the constructor.   
            JobStep jbstp = new JobStep(jb, "Test_Job_Step");  
            jbstp.Command = "Test_StoredProc";  
            jbstp.OnSuccessAction = StepCompletionAction.QuitWithSuccess;  
            jbstp.OnFailAction = StepCompletionAction.QuitWithFailure;  
  
            //Create the job step on the instance of SQL Agent.   
            jbstp.Create();  
  
            //Define a JobSchedule object variable by supplying the parent job and name arguments in the constructor.   
  
            JobSchedule jbsch = new JobSchedule(jb, "Test_Job_Schedule");  
  
            //Set properties to define the schedule frequency, and duration.   
            jbsch.FrequencyTypes = FrequencyTypes.Daily;  
            jbsch.FrequencySubDayTypes = FrequencySubDayTypes.Minute;  
            jbsch.FrequencySubDayInterval = 30;  
            TimeSpan ts1 = new TimeSpan(9, 0, 0);  
            jbsch.ActiveStartTimeOfDay = ts1;  
  
            TimeSpan ts2 = new TimeSpan(17, 0, 0);  
            jbsch.ActiveEndTimeOfDay = ts2;  
            jbsch.FrequencyInterval = 1;  
  
            System.DateTime d = new System.DateTime(2003, 1, 1);  
            jbsch.ActiveStartDate = d;  
  
            //Create the job schedule on the instance of SQL Agent.   
            jbsch.Create();  
        }  
```  
  
## <a name="creating-a-job-with-steps-and-a-schedule-in-powershell"></a>PowerShell에서 단계와 일정이 포함된 작업 만들기  
 이 코드 예제는 단계와 일정이 포함된 작업을 만든 다음 운영자에게 알립니다.  
  
```  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define an Operator object variable by supplying the Agent (parent JobServer object) and the name in the constructor.  
$op = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.Operator -argumentlist $srv.JobServer, "Test_Operator"  
  
#Set the Net send address.  
$op.NetSendAddress = "Network1_PC"  
  
#Create the operator on the instance of SQL Agent.  
$op.Create()  
  
#Define a Job object variable by supplying the Agent and the name arguments in the constructor and setting properties.   
$jb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.Job -argumentlist $srv.JobServer, "Test_Job"   
  
#Specify which operator to inform and the completion action.   
$jb.OperatorToNetSend = "Test_Operator";   
$jb.NetSendLevel = [Microsoft.SqlServer.Management.SMO.Agent.CompletionAction]::Always  
  
#Create the job on the instance of SQL Server Agent.   
$jb.Create()  
  
#Define a JobStep object variable by supplying the parent job and name arguments in the constructor.   
$jbstp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.JobStep -argumentlist $jb, "Test_Job_Step"   
$jbstp.Command = "Test_StoredProc";   
$jbstp.OnSuccessAction = [Microsoft.SqlServer.Management.SMO.Agent.StepCompletionAction]::QuitWithSuccess;   
$jbstp.OnFailAction =[Microsoft.SqlServer.Management.SMO.Agent.StepCompletionAction]::QuitWithFailure;   
  
#Create the job step on the instance of SQL Agent.   
$jbstp.Create();   
  
#Define a JobSchedule object variable by supplying the parent job and name arguments in the constructor.   
$jbsch =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.JobSchedule -argumentlist $jb, "Test_Job_Schedule"   
  
#Set properties to define the schedule frequency, and duration.   
$jbsch.FrequencyTypes =  [Microsoft.SqlServer.Management.SMO.Agent.FrequencyTypes]::Daily  
  
$jbsch.FrequencySubDayTypes = [Microsoft.SqlServer.Management.SMO.Agent.FrequencySubDayTypes]::Minute  
$jbsch.FrequencySubDayInterval = 30  
$ts1 =  New-Object -TypeName TimeSpan -argumentlist 9, 0, 0  
$jbsch.ActiveStartTimeOfDay = $ts1  
$ts2 = New-Object -TypeName TimeSpan -argumentlist 17, 0, 0  
$jbsch.ActiveEndTimeOfDay = $ts2  
$jbsch.FrequencyInterval = 1  
$jbsch.ActiveStartDate = "01/01/2003"  
  
#Create the job schedule on the instance of SQL Agent.   
$jbsch.Create();  
```  
  
## <a name="creating-an-alert-in-visual-basic"></a>Visual Basic에서 경고 만들기  
 이 코드 예제는 성능 조건에 따라 트리거되는 경고를 만듭니다. 다음과 같은 특정 형식으로 조건을 제공해야 합니다.  
  
 **ObjectName | CounterName | 인스턴스 | ComparisionOp | CompValue**  
  
 경고 알림을 위해 운영자가 필요합니다. `operator`가 Visual Basic 키워드이므로 <xref:Microsoft.SqlServer.Management.Smo.Agent.Operator> 형식을 대괄호로 묶어야 합니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBAgent3](SMO How to#SMO_VBAgent3)]  -->  
  
## <a name="creating-an-alert-in-visual-c"></a>Visual C#에서 경고 만들기  
 이 코드 예제는 성능 조건에 따라 트리거되는 경고를 만듭니다. 다음과 같은 특정 형식으로 조건을 제공해야 합니다.  
  
 **ObjectName | CounterName | 인스턴스 | ComparisionOp | CompValue**  
  
 경고 알림을 위해 운영자가 필요합니다. `operator`가 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 키워드이므로 <xref:Microsoft.SqlServer.Management.Smo.Agent.Operator> 형식을 대괄호로 묶어야 합니다.  
  
```  
{  
             //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Define an Alert object variable by supplying the SQL Server Agent and the name arguments in the constructor.   
            Alert al = new Alert(srv.JobServer, "Test_Alert");  
  
            //Specify the performance condition string to define the alert.   
            al.PerformanceCondition = "SQLServer:General Statistics|User Connections||>|3";  
  
            //Create the alert on the SQL Agent.   
            al.Create();  
  
            //Define an Operator object variable by supplying the SQL Server Agent and the name arguments in the constructor.   
  
            Operator op = new Operator(srv.JobServer, "Test_Operator");  
            //Set the net send address.   
            op.NetSendAddress = "NetworkPC";  
            //Create the operator on the SQL Agent.   
            op.Create();  
            //Run the AddNotification method to specify the operator is notified when the alert is raised.   
            al.AddNotification("Test_Operator", NotifyMethods.NetSend);  
        }  
```  
  
## <a name="creating-an-alert-in-powershell"></a>PowerShell에서 경고 만들기  
 이 코드 예제는 성능 조건에 따라 트리거되는 경고를 만듭니다. 다음과 같은 특정 형식으로 조건을 제공해야 합니다.  
  
 **ObjectName | CounterName | 인스턴스 | ComparisionOp | CompValue**  
  
 경고 알림을 위해 운영자가 필요합니다. `operator`가 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 키워드이므로 <xref:Microsoft.SqlServer.Management.Smo.Agent.Operator> 형식을 대괄호로 묶어야 합니다.  
  
```  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define an Alert object variable by supplying the SQL Agent and the name arguments in the constructor.  
$al = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.Alert -argumentlist $srv.JobServer, "Test_Alert"  
  
#Specify the performance condition string to define the alert.  
$al.PerformanceCondition = "SQLServer:General Statistics|User Connections||>|3"  
  
#Create the alert on the SQL Agent.  
$al.Create()  
  
#Define an Operator object variable by supplying the Agent (parent JobServer object) and the name in the constructor.  
$op = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Agent.Operator -argumentlist $srv.JobServer, "Test_Operator"  
  
#Set the Net send address.  
$op.NetSendAddress = "Network1_PC"  
  
#Create the operator on the instance of SQL Agent.  
$op.Create()  
  
#Run the AddNotification method to specify the operator is notified when the alert is raised.  
$ns = [Microsoft.SqlServer.Management.SMO.Agent.NotifyMethods]::NetSend  
$al.AddNotification("Test_Operator", $ns)  
  
#Drop the alert and the operator  
$al.Drop()  
$op.Drop()  
```  
  
## <a name="allowing-user-access-to-subsystem-by-using-a-proxy-account-in-visual-basic"></a>Visual Basic에서 프록시 계정을 사용하여 하위 시스템에 사용자 액세스 허용  
 이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.Agent.ProxyAccount.AddSubSystem%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Agent.ProxyAccount> 메서드를 사용하여 지정된 하위 시스템에 사용자 액세스를 허용하는 방법을 보여 줍니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBAgent2](SMO How to#SMO_VBAgent2)]  -->  
  
## <a name="allowing-user-access-to-subsystem-by-using-a-proxy-account-in-visual-c"></a>Visual C#에서 프록시 계정을 사용하여 하위 시스템에 사용자 액세스 허용  
 이 코드 예제는 <xref:Microsoft.SqlServer.Management.Smo.Agent.ProxyAccount.AddSubSystem%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Agent.ProxyAccount> 메서드를 사용하여 지정된 하위 시스템에 사용자 액세스를 허용하는 방법을 보여 줍니다.  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
//Declare a JobServer object variable and reference the SQL Server Agent.   
JobServer js = default(JobServer);   
js = srv.JobServer;   
//Define a Credential object variable by supplying the parent server and name arguments in the constructor.   
Credential c = default(Credential);   
c = new Credential(srv, "Proxy_accnt");   
//Set the identity to a valid login represented by the vIdentity string variable.   
//The sub system will run under this login.   
c.Identity = vIdentity;   
//Create the credential on the instance of SQL Server.   
c.Create();   
//Define a ProxyAccount object variable by supplying the SQL Server Agent, the name, the credential, the description arguments in the constructor.   
ProxyAccount pa = default(ProxyAccount);   
pa = new ProxyAccount(js, "Test_proxy", "Proxy_accnt", true, "Proxy account for users to run job steps in command shell.");   
//Create the proxy account on the SQL Agent.   
pa.Create();   
//Add the login, represented by the vLogin string variable, to the proxy account.   
pa.AddLogin(vLogin);   
//Add the CmdExec subsytem to the proxy account.   
pa.AddSubSystem(AgentSubSystem.CmdExec);   
}   
//Now users logged on as vLogin can run CmdExec job steps with the specified credentials.   
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트](../../../ssms/agent/sql-server-agent.md)   
 [작업 구현](../../../ssms/agent/implement-jobs.md)  
  
  
