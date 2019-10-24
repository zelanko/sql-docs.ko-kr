---
title: 데이터베이스 메일 | 사용 Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2db385919c30037612f00e53b2b990c1a7df0429
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781862"
---
# <a name="using-database-mail"></a>데이터베이스 메일 사용
  SMO에서 데이터베이스 메일 하위 시스템은 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 속성에서 참조되는 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 개체로 표시됩니다. SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 개체를 사용하여 데이터베이스 메일 하위 시스템을 구성하고 프로필 및 메일 계정을 관리할 수 있습니다. SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 개체는 `Server` 개체에 속하는데, 이는 메일 계정의 범위가 서버 수준임을 의미합니다.  
  
## <a name="examples"></a>예  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 visual [studio .net에서 VISUAL BASIC SMO 프로젝트 만들기](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) 또는 [visual Studio .Net에서 Visual C&#35; smo 프로젝트 만들기](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
 @No__t_0 데이터베이스 메일를 사용 하는 프로그램의 경우 메일 네임 스페이스를 한 정하는 `Imports` 문을 포함 해야 합니다. 다음과 같이 애플리케이션의 선언 앞에, 다른 `Imports` 문 끝에 구문을 삽입하십시오.  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Visual Basic을 사용하여 데이터베이스 메일 계정 만들기  
 이 코드 예제는 SMO에서 전자 메일 계정을 만드는 방법을 보여 줍니다. 데이터베이스 메일은 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 개체로 표시되며 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Server> 속성에서 참조됩니다. SMO에서는 데이터베이스 메일을 프로그래밍 방식으로 구성할 수 있지만 수신된 전자 메일을 보내거나 처리할 수는 없습니다.  
  
 VB.NET  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMail1](SMO How to#SMO_VBMail1)]  -->  
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>Visual C#을 사용하여 데이터베이스 메일 계정 만들기  
 이 코드 예제는 SMO에서 전자 메일 계정을 만드는 방법을 보여 줍니다. 데이터베이스 메일은 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 개체로 표시되며 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Server> 속성에서 참조됩니다. SMO에서는 데이터베이스 메일을 프로그래밍 방식으로 구성할 수 있지만 수신된 전자 메일을 보내거나 처리할 수는 없습니다.  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>PowerShell을 사용하여 데이터베이스 메일 계정 만들기  
 이 코드 예제는 SMO에서 전자 메일 계정을 만드는 방법을 보여 줍니다. 데이터베이스 메일은 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 개체로 표시되며 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Server> 속성에서 참조됩니다. SMO에서는 데이터베이스 메일을 프로그래밍 방식으로 구성할 수 있지만 수신된 전자 메일을 보내거나 처리할 수는 없습니다.
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -ArgumentList $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
