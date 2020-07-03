---
title: 데이터베이스 메일 | 사용 Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dc909acc1cf5fa2a229cdf3c7477f291685c1bf0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894353"
---
# <a name="using-database-mail"></a>데이터베이스 메일 사용
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]

  SMO에서 데이터베이스 메일 하위 시스템은 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 속성에서 참조되는 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 개체로 표시됩니다. SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 개체를 사용하여 데이터베이스 메일 하위 시스템을 구성하고 프로필 및 메일 계정을 관리할 수 있습니다. SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 개체는 **서버** 개체에 속하며,이는 메일 계정의 범위가 서버 수준에 있음을 의미 합니다.  
  
## <a name="examples"></a>예  
 제공된 코드 예제를 사용하려면 애플리케이션을 만들 프로그래밍 환경, 프로그래밍 템플릿 및 프로그래밍 언어를 선택해야 합니다. 자세한 내용은 [Visual Studio .net에서 Visual C&#35; SMO 프로젝트 만들기](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)를 참조 하세요.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 메일을 사용하는 프로그램에 대해 메일 네임스페이스를 한정하는 **Imports** 문을 포함해야 합니다. 다음과 같이 애플리케이션의 선언 앞에, 다른 **Imports** 문 끝에 구문을 삽입하십시오.  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Visual Basic을 사용하여 데이터베이스 메일 계정 만들기  
 이 코드 예제는 SMO에서 전자 메일 계정을 만드는 방법을 보여 줍니다. 데이터베이스 메일은 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 개체로 표시되며 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 개체의 <xref:Microsoft.SqlServer.Management.Smo.Server> 속성에서 참조됩니다. SMO에서는 데이터베이스 메일을 프로그래밍 방식으로 구성할 수 있지만 수신된 전자 메일을 보내거나 처리할 수는 없습니다.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Define the Database Mail service with a SqlMail object variable and reference it using the Server Mail property.
Dim sm As SqlMail
sm = srv.Mail
'Define and create a mail account by supplying the Database Mail service, name, description, display name, and email address arguments in the constructor.
Dim a As MailAccount
a = New MailAccount(sm, "AdventureWorks Administrator", "AdventureWorks Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com")
a.Create()
```
  
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
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  
