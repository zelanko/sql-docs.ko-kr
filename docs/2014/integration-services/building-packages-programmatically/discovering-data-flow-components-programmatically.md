---
title: 프로그래밍 방식으로 데이터 흐름 구성 요소 검색 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- PipelineComponentInfos collection
- data flow task [Integration Services], components
- discovering data flow components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: ff92a96a-8af6-4532-82cc-c0bbff92401b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 92cd83935ef4cb76c40aae0964100c7b88d847e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771801"
---
# <a name="discovering-data-flow-components-programmatically"></a>프로그래밍 방식으로 데이터 흐름 구성 요소 검색
  패키지에 데이터 흐름 태스크를 추가한 후 사용할 수 있는 데이터 흐름 구성 요소를 확인할 수 있습니다. 로컬 컴퓨터에 설치되어 있고 사용 가능한 데이터 흐름 원본, 변환 및 대상을 프로그래밍 방식으로 검색할 수 있습니다. 패키지에 데이터 흐름 태스크 추가에 대한 자세한 내용은 [프로그래밍 방식으로 데이터 흐름 태스크 추가](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)를 참조하세요.  
  
## <a name="discovering-components"></a>구성 요소 검색  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스에서는 로컬 컴퓨터에 올바르게 설치된 각 구성 요소에 대한 <xref:Microsoft.SqlServer.Dts.Runtime.Application.PipelineComponentInfos%2A> 개체가 들어 있는 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 컬렉션을 제공합니다. 각 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo>에는 구성 요소 이름, 설명 및 생성 이름과 같이 구성 요소에 대한 정보가 들어 있습니다. 패키지에 구성 요소를 추가할 때 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> 속성에서 반환된 값을 사용하여 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A>의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 속성을 설정할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
 사용 가능한 구성 요소를 검색한 후에는 다음의 [프로그래밍 방식으로 데이터 흐름 구성 요소 추가](../building-packages-programmatically/adding-data-flow-components-programmatically.md) 항목에 설명된 대로 구성 요소를 추가하고 구성합니다.  
  
## <a name="sample"></a>예제  
 다음 코드 예제에서는 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfos> 개체의 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 컬렉션을 열거하여 로컬 컴퓨터에서 사용할 수 있는 데이터 흐름 구성 요소를 프로그래밍 방식으로 검색하는 방법을 보여 줍니다. 이 샘플에는 Microsoft.SqlServer.ManagedDTS 어셈블리에 대한 참조가 필요합니다.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application application = new Application();  
      PipelineComponentInfos componentInfos = application.PipelineComponentInfos;  
  
      foreach (PipelineComponentInfo componentInfo in componentInfos)  
      {  
        Console.WriteLine("Name: " + componentInfo.Name + "\n" +  
          " CreationName: " + componentInfo.CreationName + "\n");  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim application As Application = New Application()  
  
    Dim componentInfos As PipelineComponentInfos = application.PipelineComponentInfos  
  
    For Each componentInfo As PipelineComponentInfo In componentInfos  
      Console.WriteLine("Name: " & componentInfo.Name & vbCrLf & _  
        " CreationName: " & componentInfo.CreationName & vbCrLf)  
    Next  
  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [프로그래밍 방식으로 데이터 흐름 구성 요소 추가](../building-packages-programmatically/adding-data-flow-components-programmatically.md)  
  
  
