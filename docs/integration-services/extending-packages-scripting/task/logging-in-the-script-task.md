---
title: "스크립트 태스크에서 로깅 | Microsoft Docs"
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
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- logs [Integration Services], scripts
- Integration Services packages, logs
- Log method
- SSIS Script task, logs
- Script task [Integration Services], logs
- packages [Integration Services], logs
ms.assetid: 2e11fc15-df18-4309-bd2d-fc58aa4b9b7a
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 98859dafe0b023954f10239fe11e8b76f36ab28b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-task"></a>스크립트 태스크에서 로깅
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 패키지의 로깅 기능을 사용하면 나중에 분석할 수 있도록 미리 정의된 이벤트나 사용자 정의 메시지를 기록하여 실행 진행률, 결과 및 문제에 대한 세부 정보를 기록할 수 있습니다. 스크립트 태스크에서 사용할 수는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 의 메서드는 **Dts** 사용자 정의 데이터를 기록 하는 개체입니다. 로깅이 설정 된 경우와 **ScriptTaskLogEntry** 이벤트가 로깅 대상으로 선택 되어는 **세부 정보** 탭은 **SSIS 로그 구성** 대화 상자, 한 번 호출 하는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> 메서드 작업에 대해 구성 된 모든 로그 공급자에 이벤트 정보를 저장 합니다.  
  
> [!NOTE]  
>  스크립트 태스크에서 직접 로깅을 수행할 수도 있지만 로깅보다는 이벤트를 구현하는 것이 좋습니다. 이벤트를 사용하면 이벤트 메시지의 로깅 기능을 사용할 수 있을 뿐 아니라 기본 또는 사용자 정의 이벤트 처리기를 사용하여 이벤트에 응답할 수도 있습니다.  
  
 로깅에 대 한 자세한 내용은 참조 [Integration services&#40; Ssis&#41; 로깅](../../../integration-services/performance/integration-services-ssis-logging.md)합니다.  
  
## <a name="logging-example"></a>로깅 예  
 다음 예에서는 처리된 행 수를 나타내는 값을 로깅하여 스크립트 태스크에서의 로깅을 보여 줍니다.  
  
```vb  
Public Sub Main()  
  
    Dim rowsProcessed As Integer = 100  
    Dim emptyBytes(0) As Byte  
  
    Try  
        Dts.Log("Rows processed: " & rowsProcessed.ToString, _  
            0, _  
            emptyBytes)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
            //  
            int rowsProcessed = 100;  
            byte[] emptyBytes = new byte[0];  
  
            try  
            {  
                Dts.Log("Rows processed: " + rowsProcessed.ToString(), 0, emptyBytes);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                //An error occurred.  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
```  
  
 }  
  
## <a name="external-resources"></a>외부 리소스  
  
-   블로그 항목- [Integration Services 태스크에 대 한 사용자 지정 이벤트 로깅](http://go.microsoft.com/fwlink/?LinkId=165644), dougbert.com  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services &#40; Ssis&#41; 로깅](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
