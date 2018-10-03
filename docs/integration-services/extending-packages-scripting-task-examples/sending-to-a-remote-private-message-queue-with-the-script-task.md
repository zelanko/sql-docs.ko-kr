---
title: 스크립트 태스크를 사용하여 원격 개인 메시지 큐에 메시지 보내기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0f25998bdbbe2cc32027b2fcb54bf7ef32bc716e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832591"
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>스크립트 태스크를 사용하여 원격 개인 메시지 큐에 메시지 보내기
  개발자는 메시지 큐(MSMQ)를 통해 메시지를 주고 받는 방법으로 신속하고 안전하게 응용 프로그램과 통신할 수 있습니다. 메시지 큐는 로컬 컴퓨터나 원격 컴퓨터에 있을 수 있으며 공개 큐이거나 개인 큐일 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 MSMQ 연결 관리자와 메시지 큐 태스크에서 원격 컴퓨터의 개인 큐로 메시지를 보낼 수 없습니다. 그러나 스크립트 태스크를 사용하면 원격 개인 메시지 큐에 메시지를 쉽게 보낼 수 있습니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="description"></a>설명  
 다음 예에서는 기존 MSMQ 연결 관리자와 System.Messaging 네임스페이스의 개체 및 메서드를 사용하여 패키지 변수에 들어 있는 텍스트를 원격 개인 메시지 큐에 보냅니다. MSMQ 연결 관리자의 M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) 메서드에 대한 호출은 **Send** 메서드가 이 작업을 수행하는 **MessageQueue** 개체를 반환합니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  기본 이름을 사용하여 MSMQ 연결 관리자를 만듭니다. 다음과 같은 형식으로 올바른 원격 개인 큐의 경로를 설정합니다.  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  **MessageText**라는 **String** 형식의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 변수를 만들어 메시지 텍스트를 스크립트에 전달합니다. 변수의 값으로 기본 메시지를 입력합니다.  
  
3.  디자인 화면에 스크립트 태스크를 추가하고 편집합니다. **스크립트 태스크 편집기**의 **스크립트** 탭에서 **ReadOnlyVariables** 속성에 `MessageText` 변수를 추가하여 해당 변수를 스크립트 내에서 사용할 수 있게 합니다.  
  
4.  **스크립트 편집**을 클릭하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA(Tools for Applications) 스크립트 편집기를 엽니다.  
  
5.  **System.Messaging** 네임스페이스에 대한 참조를 스크립트 프로젝트에 추가합니다.  
  
6.  스크립트 창의 내용을 다음 섹션의 코드로 바꿉니다.  
  
## <a name="code"></a>코드  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Messaging  
  
Public Class ScriptMain  
  
    Public Sub Main()  
  
        Dim remotePrivateQueue As MessageQueue  
        Dim messageText As String  
  
        remotePrivateQueue = _  
            DirectCast(Dts.Connections("Message Queue Connection Manager").AcquireConnection(Dts.Transaction), _  
            MessageQueue)  
        messageText = DirectCast(Dts.Variables("MessageText").Value, String)  
        remotePrivateQueue.Send(messageText)  
  
        Dts.TaskResult = ScriptResults.Success  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Messaging;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
  
            MessageQueue remotePrivateQueue = new MessageQueue();  
            string messageText;  
  
            remotePrivateQueue = (MessageQueue)(Dts.Connections["Message Queue Connection Manager"].AcquireConnection(Dts.Transaction) as MessageQueue);  
            messageText = (string)(Dts.Variables["MessageText"].Value);  
            remotePrivateQueue.Send(messageText);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [메시지 큐 태스크](../../integration-services/control-flow/message-queue-task.md)  
  
  
