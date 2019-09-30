---
title: 스크립트 태스크를 사용하여 성능 카운터 모니터링 | Microsoft Docs
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
- performance counters [Integration Services]
- SSIS Script task, performance counters
- custom performance counters [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], performance counters
- counters [Integration Services]
ms.assetid: 86609bf1-cae6-435e-a58d-41bdfc521e94
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ed4bca496d48e5fe268c1a425223fe03c8fcc6e7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297034"
---
# <a name="monitoring-performance-counters-with-the-script-task"></a>스크립트 태스크를 사용하여 성능 카운터 모니터링

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  관리자는 대량의 데이터에 대해 복잡한 변환을 수행하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 성능을 모니터링하는 경우가 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]의 **System.Diagnostics** 네임스페이스에서는 기존 성능 카운터를 사용하고 개발자 고유의 성능 카운터를 만들기 위한 클래스를 제공합니다.  
  
 성능 카운터는 시간 경과에 따른 소프트웨어 성능을 분석하는 데 사용할 수 있는 애플리케이션 성능 정보를 저장합니다. **성능 모니터** 도구를 사용하여 로컬 또는 원격으로 성능 카운터를 모니터링할 수 있습니다. 나중에 패키지에서 제어 흐름을 분기할 수 있도록 성능 카운터의 값을 변수에 저장할 수 있습니다.  
  
 성능 카운터를 사용하는 대신 **Dts** 개체의 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> 속성을 통해 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> 이벤트를 발생시킬 수도 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A> 이벤트는 진행률 및 완료율 정보를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에 반환합니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="description"></a>설명  
 다음 예에서는 사용자 지정 성능 카운터를 만들고 해당 카운터를 증가시킵니다. 이 예에서는 먼저 성능 카운터가 이미 있는지 여부를 확인합니다. 성능 카운터가 만들어지지 않은 경우 스크립트에서는 **PerformanceCounterCategory** 개체의 **Create** 메서드를 호출하여 성능 카운터를 만듭니다. 성능 카운터를 만든 후에는 스크립트에서 해당 카운터를 증가시킵니다. 마지막으로, 성능 카운터가 더 이상 필요하지 않은 경우 성능 카운터에서 **Close** 메서드를 호출하는 모범 사례를 따릅니다.  
  
> [!NOTE]  
>  성능 카운터 범주와 성능 카운터를 새로 만들려면 관리자 권한이 필요합니다. 또한 새 범주 및 카운터는 만든 후에도 해당 컴퓨터에 유지됩니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
-   코드에 **Imports** 문을 사용하여 **System.Diagnostics** 네임스페이스를 가져옵니다.  
  
### <a name="example-code"></a>코드 예  
  
```vb  
Public Sub Main()  
  
    Dim myCounter As PerformanceCounter  
  
    Try  
        'Create the performance counter if it does not already exist.  
        If Not _  
        PerformanceCounterCategory.Exists("TaskExample") Then  
            PerformanceCounterCategory.Create("TaskExample", _  
                "Task Performance Counter Example", "Iterations", _  
                "Number of times this task has been called.")  
        End If  
  
        'Initialize the performance counter.  
        myCounter = New PerformanceCounter("TaskExample", _  
            "Iterations", String.Empty, False)  
  
        'Increment the performance counter.  
        myCounter.Increment()  
  
         myCounter.Close()  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Task Performance Counter Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
  
public class ScriptMain  
{  
  
public void Main()  
        {  
  
            PerformanceCounter myCounter;  
  
            try  
            {  
                //Create the performance counter if it does not already exist.  
                if (!PerformanceCounterCategory.Exists("TaskExample"))  
                {  
                    PerformanceCounterCategory.Create("TaskExample", "Task Performance Counter Example", "Iterations", "Number of times this task has been called.");  
                }  
  
                //Initialize the performance counter.  
                myCounter = new PerformanceCounter("TaskExample", "Iterations", String.Empty, false);  
  
                //Increment the performance counter.  
                myCounter.Increment();  
  
                myCounter.Close();  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Task Performance Counter Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
  
```  
