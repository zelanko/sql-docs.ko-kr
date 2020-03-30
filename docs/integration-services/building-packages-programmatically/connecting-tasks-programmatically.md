---
title: 프로그래밍 방식으로 태스크 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- tasks [Integration Services], precedence constraints
- precedence constraints [Integration Services], connecting tasks
- constraints [Integration Services]
ms.assetid: 23668e88-cef4-4009-a9cf-38e607eab7a2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 51cce76a41cfcc513e633a20b16ca5e861fa492a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71299035"
---
# <a name="connecting-tasks-programmatically"></a>프로그래밍 방식으로 태스크 연결

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  개체 모델에서 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 클래스가 나타내는 선행 제약 조건은 패키지에서 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 개체가 실행되는 순서를 설정합니다. 선행 제약 조건을 사용하면 패키지의 컨테이너 및 태스크 실행이 이전 태스크 또는 컨테이너의 실행 결과에 따라 결정되도록 할 수 있습니다. 선행 제약 조건은 컨테이너 개체에서 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 컬렉션의 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints.Add%2A> 메서드를 호출하여 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraints> 개체 쌍 간에 설정됩니다. 두 개의 실행 개체 사이에 제약 조건을 만든 후 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A> 속성을 설정하여 제약 조건에 정의된 두 번째 실행 파일을 실행하기 위한 조건을 지정합니다.  
  
 다음 표에서 설명하는 것처럼 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.EvalOp%2A> 속성에 지정하는 값에 따라 단일 선행 제약 조건에 제약 조건과 식을 모두 사용할 수 있습니다.  
  
|EvalOp 속성 값|Description|  
|----------------------------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Constraint>|실행 결과에 따라 제약 조건이 지정된 컨테이너 또는 태스크의 실행 여부가 결정되도록 지정합니다. <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 속성을 <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 열거형에서 원하는 값으로 설정합니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.Expression>|식의 값에 따라 제약 조건이 지정된 컨테이너 또는 태스크의 실행 여부가 결정되도록 지정합니다. <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 속성을 설정합니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionAndConstraint>|제약 조건 결과가 발생해야 하며 식에서 제약 조건이 지정된 컨테이너 또는 태스크의 실행을 평가해야 하도록 지정합니다. <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> 속성과 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 속성을 모두 설정하고 해당 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> 속성을 **true**로 설정합니다.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.DTSPrecedenceEvalOp.ExpressionOrConstraint>|제약 조건 결과가 발생해야 하거나 식에서 제약 조건이 지정된 컨테이너 또는 태스크의 실행을 평가해야 하도록 지정합니다. <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Value%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.Expression%2A> 속성과 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 속성을 모두 설정하고 해당 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint.LogicalAnd%2A> 속성을 **false**로 설정합니다.|  
  
 다음 코드 예제에서는 패키지에 두 개의 태스크를 추가하는 방법을 보여 줍니다. 두 태스크 사이에는 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint>가 만들어지므로 첫 번째 태스크가 완료될 때까지 두 번째 태스크는 실행되지 않습니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      // Add a File System task.  
      Executable eFileTask1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost1 = eFileTask1 as TaskHost;  
  
      // Add a second File System task.  
      Executable eFileTask2 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileHost2 = eFileTask2 as TaskHost;  
  
      // Put a precedence constraint between the tasks.  
      // Set the constraint to specify that the second File System task cannot run  
      // until the first File System task finishes.  
      PrecedenceConstraint pcFileTasks =   
        p.PrecedenceConstraints.Add((Executable)thFileHost1, (Executable)thFileHost2);  
      pcFileTasks.Value = DTSExecResult.Completion;  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task.  
    Dim eFileTask1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost1 As TaskHost = CType(eFileTask1, TaskHost)  
  
    ' Add a second File System task.  
    Dim eFileTask2 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileHost2 As TaskHost = CType(eFileTask2, TaskHost)  
  
    ' Put a precedence constraint between the tasks.  
    ' Set the constraint to specify that the second File System task cannot run  
    ' until the first File System task finishes.  
    Dim pcFileTasks As PrecedenceConstraint = _  
      p.PrecedenceConstraints.Add(CType(thFileHost1, Executable), CType(thFileHost2, Executable))  
    pcFileTasks.Value = DTSExecResult.Completion  
  
  End Sub  
  
End Module  
```
  
## <a name="see-also"></a>참고 항목  
 [프로그래밍 방식으로 데이터 흐름 태스크 추가](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)  
  
  
