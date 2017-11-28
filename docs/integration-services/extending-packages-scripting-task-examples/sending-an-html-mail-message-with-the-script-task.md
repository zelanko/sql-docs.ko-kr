---
title: "스크립트 태스크와 HTML 메일 메시지 보내기 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-task-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b5f50a79ca83243ea130c77a0d95ab402ba2d31a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>스크립트 태스크를 사용하여 HTML 메일 메시지 보내기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] SendMail 태스크에서는 일반 텍스트 형식의 메일 메시지만 지원합니다. 그러나 스크립트 태스크와 .NET Framework의 메일 기능을 사용하여 HTML 메일 메시지를 쉽게 보낼 수도 있습니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="description"></a>Description  
 다음 예제에서는 **System.Net.Mail** 네임 스페이스를 구성 하 고 HTML 메일 메시지를 보냅니다. 스크립트에서 제목과 패키지 변수에서 전자 메일의 본문을 가져오고, 사용 하 여 새 **MailMessag**설정 해당 **IsBodyHtml** 속성을 **True**합니다. 인스턴스를 초기화 합니다. 다른 패키지 변수에서 SMTP 서버 이름을 가져온 다음 **대신**, 호출 하 고 해당 **보낼** HTML 메시지를 보내는 방법을 합니다. 이 예제에서는 다른 스크립트에서 다시 사용할 수 있도록 메시지 보내기 기능을 서브루틴에 캡슐화합니다.  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>이 스크립트 태스크 예에서 SMTP 연결 관리자를 사용하지 않도록 구성하려면  
  
1.  `HtmlEmailTo`, `HtmlEmailFrom` 및 `HtmlEmailSubject`라는 문자열 변수를 만들고 이 변수에 올바른 테스트 메시지에 대한 적절한 값을 할당합니다.  
  
2.  `HtmlEmailBody`라는 문자열 변수를 만들고 이 변수에 HTML 태그의 문자열을 할당합니다. 예를 들어  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  `HtmlEmailServer`라는 문자열 변수를 만들고 보내는 익명의 보내는 메시지를 허용하는 사용 가능한 SMTP 서버의 이름을 할당합니다.  
  
4.  5 이러한 변수를 모두 할당 된 **ReadOnlyVariables** 새 스크립트 태스크의 속성입니다.  
  
5.  가져오기는 **System.Net** 및 **System.Net.Mail** 코드에 대 한 네임 스페이스입니다.  
  
 이 항목의 예제 코드는 패키지 변수에서 SMTP 서버 이름을 가져옵니다. 그러나 SMTP 연결 관리자를 사용하여 연결 정보를 캡슐화하고 코드를 통해 연결 관리자에서 서버 이름을 추출할 수도 있습니다. SMTP 연결 관리자의 <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> 메서드는 문자열을 다음과 같은 형식으로 반환합니다.  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 사용할 수는 **String.Split** 메서드를이 인수 목록을 각 세미콜론 (;)에서 개별 문자열의 배열에 구분 또는 값이 등호 (=) 및 서버 이름으로 배열에서 두 번째 인수 (subscript 1)을 추출 합니다.  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>이 스크립트 태스크 예에서 SMTP 연결 관리자를 사용하도록 구성하려면  
  
1.  제거 하 여 이전에 구성한 스크립트 태스크를 수정 된 `HtmlEmailServer` 목록에서 변수 **ReadOnlyVariables**합니다.  
  
2.  서버 이름을 가져오는 다음 코드 줄을  
  
    ```  
    Dim smtpServer As String = _  
      Dts.Variables("HtmlEmailServer").Value.ToString  
    ```  
  
     다음 줄로 바꿉니다.  
  
    ```  
    Dim smtpConnectionString As String = _  
      DirectCast(Dts.Connections("SMTP Connection Manager").AcquireConnection(Dts.Transaction), String)  
    Dim smtpServer As String = _  
      smtpConnectionString.Split(New Char() {"="c, ";"c})(1)  
    ```  
  
## <a name="code"></a>코드  
  
```vb  
Public Sub Main()  
  
  Dim htmlMessageFrom As String = _  
    Dts.Variables("HtmlEmailFrom").Value.ToString  
  Dim htmlMessageTo As String = _  
    Dts.Variables("HtmlEmailTo").Value.ToString  
  Dim htmlMessageSubject As String = _  
    Dts.Variables("HtmlEmailSubject").Value.ToString  
  Dim htmlMessageBody As String = _  
    Dts.Variables("HtmlEmailBody").Value.ToString  
  Dim smtpServer As String = _  
    Dts.Variables("HtmlEmailServer").Value.ToString  
  
  SendMailMessage( _  
      htmlMessageFrom, htmlMessageTo, _  
      htmlMessageSubject, htmlMessageBody, _  
      True, smtpServer)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Sub SendMailMessage( _  
    ByVal From As String, ByVal SendTo As String,  _  
    ByVal Subject As String, ByVal Body As String, _  
    ByVal IsBodyHtml As Boolean, ByVal Server As String)  
  
  Dim htmlMessage As MailMessage  
  Dim mySmtpClient As SmtpClient  
  
  htmlMessage = New MailMessage( _  
    From, SendTo, Subject, Body)  
  htmlMessage.IsBodyHtml = IsBodyHtml  
  
  mySmtpClient = New SmtpClient(Server)  
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials  
  mySmtpClient.Send(htmlMessage)  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();  
            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();  
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();  
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();  
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();  
  
            SendMailMessage(htmlMessageFrom, htmlMessageTo, htmlMessageSubject, htmlMessageBody, true, smtpServer);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private void SendMailMessage(string From, string SendTo, string Subject, string Body, bool IsBodyHtml, string Server)  
        {  
  
            MailMessage htmlMessage;  
            SmtpClient mySmtpClient;  
  
            htmlMessage = new MailMessage(From, SendTo, Subject, Body);  
            htmlMessage.IsBodyHtml = IsBodyHtml;  
  
            mySmtpClient = new SmtpClient(Server);  
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;  
            mySmtpClient.Send(htmlMessage);  
  
        }  
```  
  
## <a name="see-also"></a>관련 항목:  
 [메일 보내기 태스크](../../integration-services/control-flow/send-mail-task.md)  
  
  

