---
title: 메시지를 사용 하 여 | Microsoft Docs
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
topic_type:
- apiref
helpviewer_keywords:
- messages [SMO]
ms.assetid: 4037a866-4826-4c1f-890c-e7e3658adf13
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 868af8443b01b44b79642b6c7f2ef321b9513203
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37164234"
---
# <a name="using-messages"></a>메시지 사용
  SMO에서 시스템 메시지는 `Server` 개체에 속하는 <xref:Microsoft.SqlServer.Management.Smo.SystemMessageCollection> 개체로 표시됩니다. 시스템 메시지는 수정할 수 없으므로 `SystemMessage` 개체 속성은 읽기 전용입니다.  
  
 사용자 정의 메시지는 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedMessageCollection> 개체를 통해 SMO에서 프로그래밍 방식으로 표시됩니다. 전체 컬렉션을 반복하여 기존 사용자 정의 메시지를 검색할 수 있습니다. 새 사용자 정의 메시지는 새 `UserDefinedMessage` 개체를 인스턴스화하고 적절한 속성을 설정하여 만들 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 코드 예제를 사용하려면 응용 프로그램을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 및 [Visual C 만들기&#35; Visual Studio.NET에서 SMO 프로젝트](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)합니다.  
  
## <a name="finding-a-particular-system-message-in-visual-basic"></a>Visual Basic에서 특정 시스템 메시지 찾기  
 코드 예제는 ID 번호로 시스템 메시지를 식별하고 메시지를 표시하는 방법을 보여 줍니다.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMessages1](SMO How to#SMO_VBMessages1)]  -->  
  
## <a name="finding-a-particular-system-message-in-visual-c"></a>Visual C#에서 특정 시스템 메시지 찾기  
 코드 예제는 ID 번호로 시스템 메시지를 식별하고 메시지를 표시하는 방법을 보여 줍니다.  
  
```  
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
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get the message 14126 in US English and display it  
$msg = $srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")  
$msg.ID.ToString() + " "+ $msg.Text  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-basic"></a>Visual Basic에서 새 사용자 정의 메시지 추가  
 코드 예제는 ID가 5000보다 큰 사용자 정의 메시지를 만드는 방법을 보여 줍니다.  
  
```  
Dim mysrv As Server  
mysrv = New Server  
Dim udm As UserDefinedMessage  
udm = New UserDefinedMessage(mysrv, 50003, "us_english", 16, "Test message")  
udm.Create()  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-c"></a>Visual C#에서 새 사용자 정의 메시지 추가  
 코드 예제는 ID가 5000보다 큰 사용자 정의 메시지를 만드는 방법을 보여 줍니다.  
  
```  
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
  
```  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a new message  
  
$udm = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedMessage -argumentlist `  
$srv, 50030, "us_english", 16, "Test message"  
$udm.Create()  
$msg = $srv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
$msg  
```  
  
  
