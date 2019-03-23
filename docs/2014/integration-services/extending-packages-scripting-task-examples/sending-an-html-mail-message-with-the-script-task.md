---
title: 스크립트 태스크를 사용하여 HTML 메일 메시지 보내기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 254f1fcb701fd11b22e35def915b09b537c4b33a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392211"
---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>스크립트 태스크를 사용하여 HTML 메일 메시지 보내기
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] SendMail 태스크에서는 일반 텍스트 형식의 메일 메시지만 지원합니다. 그러나 스크립트 태스크와 .NET Framework의 메일 기능을 사용하여 HTML 메일 메시지를 쉽게 보낼 수도 있습니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="description"></a>Description  
 다음 예에서는 `System.Net.Mail` 네임스페이스를 사용하여 HTML 메일 메시지를 구성하고 보냅니다. 스크립트는 패키지 변수에서 전자 메일의 받는 사람, 보내는 사람, 제목 및 본문을 가져오고 이를 사용하여 새 `MailMessag`를 만든 다음 해당 `IsBodyHtml` 속성을 `True`로 설정합니다. 그런 다음 다른 패키지 변수에서 SMTP 서버 이름을 가져오고 `System.Net.Mail.SmtpClient`의 인스턴스를 초기화한 다음 `Send` 메서드를 호출하여 HTML 메시지를 보냅니다. 이 예제에서는 다른 스크립트에서 다시 사용할 수 있도록 메시지 보내기 기능을 서브루틴에 캡슐화합니다.  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>이 스크립트 태스크 예에서 SMTP 연결 관리자를 사용하지 않도록 구성하려면  
  
1.  `HtmlEmailTo`, `HtmlEmailFrom` 및 `HtmlEmailSubject`라는 문자열 변수를 만들고 이 변수에 올바른 테스트 메시지에 대한 적절한 값을 할당합니다.  
  
2.  `HtmlEmailBody`라는 문자열 변수를 만들고 이 변수에 HTML 태그의 문자열을 할당합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  `HtmlEmailServer`라는 문자열 변수를 만들고 보내는 익명의 보내는 메시지를 허용하는 사용 가능한 SMTP 서버의 이름을 할당합니다.  
  
4.  이러한 다섯 개의 변수를 모두 새 스크립트 태스크의 **ReadOnlyVariables** 속성에 할당합니다.  
  
5.  `System.Net` 및 `System.Net.Mail` 네임스페이스를 코드로 가져옵니다.  
  
 이 항목의 예제 코드는 패키지 변수에서 SMTP 서버 이름을 가져옵니다. 그러나 SMTP 연결 관리자를 사용하여 연결 정보를 캡슐화하고 코드를 통해 연결 관리자에서 서버 이름을 추출할 수도 있습니다. SMTP 연결 관리자의 <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> 메서드는 문자열을 다음과 같은 형식으로 반환합니다.  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 `String.Split` 메서드를 사용하여 이 인수 목록을 각 세미콜론(;) 또는 등호(=) 위치에서 구분하여 개별 문자열의 배열로 만든 다음 해당 배열에서 두 번째 인수(subscript 1)를 서버 이름으로 추출할 수 있습니다.  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>이 스크립트 태스크 예에서 SMTP 연결 관리자를 사용하도록 구성하려면  
  
1.  **ReadOnlyVariables** 목록에서 `HtmlEmailServer` 변수를 제거하여 이전에 구성한 스크립트 태스크를 수정합니다.  
  
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
  
  Dim htmlMessageTo As String = _  
    Dts.Variables("HtmlEmailTo").Value.ToString  
  Dim htmlMessageFrom As String = _  
    Dts.Variables("HtmlEmailFrom").Value.ToString  
  Dim htmlMessageSubject As String = _  
    Dts.Variables("HtmlEmailSubject").Value.ToString  
  Dim htmlMessageBody As String = _  
    Dts.Variables("HtmlEmailBody").Value.ToString  
  Dim smtpServer As String = _  
    Dts.Variables("HtmlEmailServer").Value.ToString  
  
  SendMailMessage( _  
      htmlMessageTo, htmlMessageFrom, _  
      htmlMessageSubject, htmlMessageBody, _  
      True, smtpServer)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Sub SendMailMessage( _  
    ByVal SendTo As String, ByVal From As String, _  
    ByVal Subject As String, ByVal Body As String, _  
    ByVal IsBodyHtml As Boolean, ByVal Server As String)  
  
  Dim htmlMessage As MailMessage  
  Dim mySmtpClient As SmtpClient  
  
  htmlMessage = New MailMessage( _  
    SendTo, From, Subject, Body)  
  htmlMessage.IsBodyHtml = IsBodyHtml  
  
  mySmtpClient = New SmtpClient(Server)  
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials  
  mySmtpClient.Send(htmlMessage)  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();  
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();  
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();  
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();  
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();  
  
            SendMailMessage(htmlMessageTo, htmlMessageFrom, htmlMessageSubject, htmlMessageBody, true, smtpServer);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private void SendMailMessage(string SendTo, string From, string Subject, string Body, bool IsBodyHtml, string Server)  
        {  
  
            MailMessage htmlMessage;  
            SmtpClient mySmtpClient;  
  
            htmlMessage = new MailMessage(SendTo, From, Subject, Body);  
            htmlMessage.IsBodyHtml = IsBodyHtml;  
  
            mySmtpClient = new SmtpClient(Server);  
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;  
            mySmtpClient.Send(htmlMessage);  
  
        }  
```  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메일 보내기 태스크](../control-flow/send-mail-task.md)  
  
  
