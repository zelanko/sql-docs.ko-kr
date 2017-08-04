---
title: "실행 계획 및 버퍼 할당 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom data flow components [Integration Services], buffer allocations
- custom data flow components [Integration Services], execution plans
- buffer allocations [Integration Services]
- data flow components [Integration Services], buffer allocations
- data flow components [Integration Services], execution plans
- execution plans [Integration Services]
ms.assetid: 679d9ff0-641e-47c3-abb8-d1a7dcb279dd
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 931196de739980cb889f120b977b82bfb313ddd9
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="execution-plan-and-buffer-allocation"></a>실행 계획 및 버퍼 할당
  실행 전에 데이터 흐름 태스크에서는 구성 요소를 검사하고 각 구성 요소 시퀀스에 대한 실행 계획을 생성합니다. 이 섹션에서는 실행 계획, 실행 계획을 보는 방법 및 실행 계획에 따라 입력 및 출력 버퍼가 할당되는 방식에 대해 자세히 설명합니다.  
  
## <a name="understanding-the-execution-plan"></a>실행 계획 이해  
 실행 계획에는 원본 스레드와 작업 스레드가 포함되며 각 스레드에는 원본 스레드에 대한 출력 작업 목록이나 작업 스레드에 대한 입력 및 출력 작업 목록이 포함됩니다. 실행 계획의 원본 스레드 데이터 흐름에서 원본 구성 요소를 나타내고 하 여 실행 계획에서 확인 *SourceThread**n*여기서  *n*  소스 스레드 수가 0부터 시작 합니다.  
  
 각 원본 스레드에서는 버퍼를 만들고, 수신기를 설정하고, 원본 구성 요소에 대해 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드를 호출합니다. 이 지점에서 원본 구성 요소는 데이터 흐름 태스크에서 해당 구성 요소에 제공한 출력 버퍼에 행을 추가하기 시작하므로 이 지점이 실행이 시작되고 데이터가 시작되는 지점입니다. 원본 스레드가 실행된 후 잔여 작업은 여러 작업 스레드 간에 분산됩니다.  
  
 작업 스레드 입력 및 출력 작업 목록 모두 포함 하 고 실행 계획으로 식별 되 *WorkThread**n*여기서  *n*  0부터 시작 스레드에 있는 작업 수입니다. 그래프에 비동기 출력을 사용하는 구성 요소가 포함된 경우 이러한 스레드에는 출력 작업 목록이 포함됩니다.  
  
 다음 예제 실행 계획이 나타내는 데이터 흐름에서는 원본 구성 요소가 비동기 출력을 사용하는 변환에 연결되어 있고 이 변환은 대상 구성 요소에 연결되어 있습니다. 이 예에서 변환 구성 요소에는 비동기 출력이 있으므로 WorkThread0에는 출력 작업 목록이 포함됩니다.  
  
```  
SourceThread0   
    Influences: 72 158   
    Output Work List   
        CreatePrimeBuffer of type 1 for output id 10   
        SetBufferListener: "WorkThread0" for input ID 73   
        CallPrimeOutput on component "OLE DB Source" (1)   
    End Output Work List   
    This thread drives 0 distributors   
End SourceThread0   
WorkThread0   
    Influences: 72 158   
    Input Work list, input ID 73   
        CallProcessInput on input ID 73 on component "Sort" (72) for view type 2   
    End Input Work list for input 73   
    Output Work List   
        CreatePrimeBuffer of type 3 for output id 74   
        SetBufferListener: "WorkThread1" for input ID 171with internal handoff   
        CallPrimeOutput on component "Sort" (72)   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread0   
WorkThread1   
    Influences: 158   
    Input Work list, input ID 171  
        CallProcessInput on input ID 171 on component "OLE DB Destination" (158) for view type 4  
    End Input Work list for input 171   
    Output Work List   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread1  
```  
  
> [!NOTE]  
>  실행 계획이 생성 될 때마다 패키지 실행 되 고 로그 공급자를 선택 하 고 로깅을 사용 하도록 설정 하 고 패키지를 추가 하 여 캡처할 수 있습니다는 **PipelineExecutionPlan** 이벤트입니다.  
  
## <a name="understanding-buffer-allocation"></a>버퍼 할당 이해  
 실행 계획에 따라 데이터 흐름 태스크에서는 데이터 흐름 구성 요소의 출력에 정의된 열을 포함하는 버퍼를 만듭니다. 이 버퍼는 비동기 출력을 사용하는 구성 요소가 나타날 때까지 구성 요소의 시퀀스를 통해 데이터 흐름으로 재사용됩니다. 그런 다음 비동기 출력의 출력 열과 다운 스트림 구성 요소의 출력 열을 포함하는 새 버퍼가 만들어집니다.  
  
 실행 중 구성 요소에서는 현재 원본 또는 작업 스레드의 버퍼에 액세스할 수 있습니다. 이 버퍼는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드에 의해 제공된 입력 버퍼이거나 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드에 의해 제공된 출력 버퍼입니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.Mode%2A>의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 속성도 각 버퍼를 입력 또는 출력 버퍼로 식별합니다.  
  
 비동기 출력을 사용하는 변환은 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드에서 기존 입력 버퍼를 받고 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드에서 새 출력 버퍼를 받습니다. 비동기 출력을 사용하는 구성 요소는 데이터 흐름에서 입력 버퍼와 출력 버퍼를 모두 받는 유일한 유형의 구성 요소입니다.  
  
 구성 요소에 제공 된 버퍼가 포함 될 가능성이 있기 때문에 해당 입력 또는 출력 열 컬렉션에 구성 요소 보다 더 많은 열에, 구성 요소 개발자가 호출할 수는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> 지정 하 여 버퍼에서 열을 찾을 방법의 **LineageID**합니다.  
  
