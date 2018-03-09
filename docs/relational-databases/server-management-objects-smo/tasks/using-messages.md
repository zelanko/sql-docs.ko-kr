---
title: "메시지를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: messages [SMO]
ms.assetid: 4037a866-4826-4c1f-890c-e7e3658adf13
caps.latest.revision: "40"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ed18e9b9b7f91613a23d0146b79e0da2b056618
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/12/2018
---
# <a name="using-messages"></a>메시지 사용
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO에서 시스템 메시지 표시 됩니다는 <xref:Microsoft.SqlServer.Management.Smo.SystemMessageCollection> 에 속하는 개체는 **서버** 개체입니다. 시스템 메시지는 수정할 수 없으므로 **SystemMessage** 개체 속성은 읽기 전용입니다.  
  
 사용자 정의 메시지는 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedMessageCollection> 개체를 통해 SMO에서 프로그래밍 방식으로 표시됩니다. 전체 컬렉션을 반복하여 기존 사용자 정의 메시지를 검색할 수 있습니다. 새 사용자 정의 메시지는 새 **UserDefinedMessage** 개체를 인스턴스화하고 적절한 속성을 설정하여 만들 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 참조 [만들기 Visual C & #35; Visual Studio.NET에서에서 SMO 프로젝트](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="finding-a-particular-system-message-in-visual-basic"></a>Visual Basic에서 특정 시스템 메시지 찾기  
 코드 예제는 ID 번호로 시스템 메시지를 식별하고 메시지를 표시하는 방법을 보여 줍니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference an existing system message using the ItemByIdAndLanguage method.
Dim msg As SystemMessage
msg = srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")
'Display the message ID and  text.
Console.WriteLine(msg.ID.ToString + " " + msg.Text)
```
  
## <a name="finding-a-particular-system-message-in-visual-c"></a>Visual C#에서 특정 시스템 메시지 찾기  
 코드 예제는 ID 번호로 시스템 메시지를 식별하고 메시지를 표시하는 방법을 보여 줍니다.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference an existing system message using the   
            //ItemByIdAndLanguage method.   
            SystemMessage msg = default(SystemMessage);  
            msg = srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
        }  
```  
  
## <a name="finding-a-particular-system-message-in-powershell"></a>PowerShell에서 특정 시스템 메시지 찾기  
 코드 예제는 ID 번호로 시스템 메시지를 식별하고 메시지를 표시하는 방법을 보여 줍니다.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get the message 14126 in US English and display it  
$msg = $srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")  
$msg.ID.ToString() + " "+ $msg.Text  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-basic"></a>Visual Basic에서 새 사용자 정의 메시지 추가  
 코드 예제는 ID가 5000보다 큰 사용자 정의 메시지를 만드는 방법을 보여 줍니다.  
  
```VBNET  
Dim mysrv As Server  
mysrv = New Server  
Dim udm As UserDefinedMessage  
udm = New UserDefinedMessage(mysrv, 50003, "us_english", 16, "Test message")  
udm.Create()  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-c"></a>Visual C#에서 새 사용자 정의 메시지 추가  
 코드 예제는 ID가 5000보다 큰 사용자 정의 메시지를 만드는 방법을 보여 줍니다.  
  
```csharp  
{  
  
            Server mysrv = new Server();  
  
            UserDefinedMessage udm = new UserDefinedMessage(mysrv, 50030, "us_english",16, "Test message");  
            udm.Create();  
             UserDefinedMessage  msg = mysrv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
  
        }  
```  
  
## <a name="adding-a-new-user-defined-message-in-powershell"></a>PowerShell에서 새 사용자 정의 메시지 추가  
 코드 예제는 ID가 5000보다 큰 사용자 정의 메시지를 만드는 방법을 보여 줍니다.  
  
```powershell  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a new message  
  
$udm = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedMessage -argumentlist `  
$srv, 50030, "us_english", 16, "Test message"  
$udm.Create()  
$msg = $srv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
$msg  
```  
  
  
