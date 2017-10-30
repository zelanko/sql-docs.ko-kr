---
title: "스크립트 태스크에서 이벤트를 발생 시키는 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- events [Integration Services], scripts
- warnings [Integration Services]
- SSIS events, scripts
- errors [Integration Services], events
- SSIS Script task, events
- Events property
- Script task [Integration Services], events
ms.assetid: 21ea07d1-e267-4fb1-a6cc-82c95a39beae
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 80f16c8d4fa5d4eb27eefe76b2dcf811e21cfaab
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="raising-events-in-the-script-task"></a>스크립트 태스크에서 이벤트 발생
  이벤트를 사용하면 포함하는 패키지에 오류 및 경고와 태스크 진행률 또는 상태 같은 기타 정보를 보고할 수 있습니다. 패키지에서는 이벤트 알림을 관리하기 위한 이벤트 처리기를 제공합니다. 스크립트 태스크에서 메서드를 호출 하 여 이벤트를 발생 시킬 수는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 의 속성은 **Dts** 개체입니다. 방법에 대 한 자세한 내용은 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 이벤트를 처리 하는 패키지를 참조 [Integration services&#40; Ssis&#41; 이벤트 처리기](../../../integration-services/integration-services-ssis-event-handlers.md)합니다.  
  
 이벤트는 패키지에서 사용할 수 있도록 설정된 모든 로그 공급자에 로깅될 수 있습니다. 로그 공급자는 이벤트에 대한 정보를 데이터 원본에 저장합니다. 스크립트 태스크에서는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 메서드를 사용하여 이벤트를 발생시키지 않고 로그 공급자에 정보를 로깅할 수도 있습니다. 사용 하는 방법에 대 한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 메서드를 참조 [스크립트 태스크에서 로깅](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)합니다.  
  
 이벤트를 발생시키기 위해 스크립트 태스크에서는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 속성에 의해 제공된 메서드 중 하나를 호출합니다. 다음 표에서는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 속성에 의해 제공된 메서드를 보여 줍니다.  
  
|이벤트|Description|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireCustomEvent%2A>|패키지에서 사용자가 정의한 사용자 지정 이벤트를 발생시킵니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A>|패키지에 오류 조건을 알립니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireInformation%2A>|사용자에게 정보를 제공합니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A>|패키지에 태스크 진행률을 알립니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireQueryCancel%2A>|패키지에서 태스크를 중간에 종료해야 하는지 여부를 나타내는 값을 반환합니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A>|태스크가 사용자 알림이 발생할 수 있지만 오류 조건은 아닌 상태에 있음을 패키지에 알립니다.|  
  
## <a name="events-example"></a>이벤트 예  
 다음 예에서는 스크립트 태스크 내에서 이벤트를 발생시키는 방법을 보여 줍니다. 이 예에서는 네이티브 Windows API 함수를 사용하여 인터넷 연결을 사용할 수 있는지 확인합니다. 연결을 사용할 수 없으면 오류가 발생합니다. 불안정할 수 있는 모뎀 연결이 사용 중인 경우에는 경고가 발생합니다. 그렇지 않은 경우 인터넷 연결이 검색되었다는 정보 메시지가 반환됩니다.  
  
```vb  
Private Declare Function InternetGetConnectedState Lib "wininet" _  
    (ByRef dwFlags As Long, ByVal dwReserved As Long) As Long  
  
Private Enum ConnectedStates  
    LAN = &H2  
    Modem = &H1  
    Proxy = &H4  
    Offline = &H20  
    Configured = &H40  
    RasInstalled = &H10  
End Enum  
  
Public Sub Main()  
  
    Dim dwFlags As Long  
    Dim connectedState As Long  
    Dim fireAgain as Boolean  
  
    connectedState = InternetGetConnectedState(dwFlags, 0)  
  
    If connectedState <> 0 Then  
        If (dwFlags And ConnectedStates.Modem) = ConnectedStates.Modem Then  
            Dts.Events.FireWarning(0, "Script Task Example", _  
                "Volatile Internet connection detected.", String.Empty, 0)  
        Else  
            Dts.Events.FireInformation(0, "Script Task Example", _  
                "Internet connection detected.", String.Empty, 0, fireAgain)  
        End If  
    Else  
        ' If not connected to the Internet, raise an error.  
        Dts.Events.FireError(0, "Script Task Example", _  
            "Internet connection not available.", String.Empty, 0)  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
using System.Runtime.InteropServices;  
  
public class ScriptMain  
{  
  
[DllImport("wininet")]  
        private extern static long InternetGetConnectedState(ref long dwFlags, long dwReserved);  
  
        private enum ConnectedStates  
        {  
            LAN = 0x2,  
            Modem = 0x1,  
            Proxy = 0x4,  
            Offline = 0x20,  
            Configured = 0x40,  
            RasInstalled = 0x10  
        };  
  
        public void Main()  
        {  
            //  
            long dwFlags = 0;  
            long connectedState;  
            bool fireAgain = true;  
            int state;  
  
            connectedState = InternetGetConnectedState(ref dwFlags, 0);  
            state = (int)ConnectedStates.Modem;  
            if (connectedState != 0)  
            {  
                if ((dwFlags & state) == state)  
                {  
                    Dts.Events.FireWarning(0, "Script Task Example", "Volatile Internet connection detected.", String.Empty, 0);  
                }  
                else  
                {  
                    Dts.Events.FireInformation(0, "Script Task Example", "Internet connection detected.", String.Empty, 0, ref fireAgain);  
                }  
            }  
            else  
            {  
                // If not connected to the Internet, raise an error.  
                Dts.Events.FireError(0, "Script Task Example", "Internet connection not available.", String.Empty, 0);  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services &#40; Ssis&#41; 이벤트 처리기](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [패키지에 이벤트 처리기를 추가 합니다.](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  

