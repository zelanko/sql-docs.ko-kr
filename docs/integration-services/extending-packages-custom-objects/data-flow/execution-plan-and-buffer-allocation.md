---
title: 실행 계획 및 버퍼 할당 | Microsoft Docs
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
- custom data flow components [Integration Services], buffer allocations
- custom data flow components [Integration Services], execution plans
- buffer allocations [Integration Services]
- data flow components [Integration Services], buffer allocations
- data flow components [Integration Services], execution plans
- execution plans [Integration Services]
ms.assetid: 679d9ff0-641e-47c3-abb8-d1a7dcb279dd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7219499b05a3e0229d685fdf518eea41a734daba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724689"
---
# <a name="execution-plan-and-buffer-allocation"></a>실행 계획 및 버퍼 할당

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  실행 전에 데이터 흐름 태스크에서는 구성 요소를 검사하고 각 구성 요소 시퀀스에 대한 실행 계획을 생성합니다. 이 섹션에서는 실행 계획, 실행 계획을 보는 방법 및 실행 계획에 따라 입력 및 출력 버퍼가 할당되는 방식에 대해 자세히 설명합니다.  
  
## <a name="understanding-the-execution-plan"></a>실행 계획 이해  
 실행 계획에는 원본 스레드와 작업 스레드가 포함되며 각 스레드에는 원본 스레드에 대한 출력 작업 목록이나 작업 스레드에 대한 입력 및 출력 작업 목록이 포함됩니다. 실행 계획의 원본 스레드는 데이터 흐름의 원본 구성 요소를 나타내며 실행 계획에서 *SourceThreadn*으로 식별됩니다. 여기서 *n*은 0부터 시작하는 원본 스레드 번호입니다.  
  
 각 원본 스레드에서는 버퍼를 만들고, 수신기를 설정하고, 원본 구성 요소에 대해 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드를 호출합니다. 이 지점에서 원본 구성 요소는 데이터 흐름 태스크에서 해당 구성 요소에 제공한 출력 버퍼에 행을 추가하기 시작하므로 이 지점이 실행이 시작되고 데이터가 시작되는 지점입니다. 원본 스레드가 실행된 후 잔여 작업은 여러 작업 스레드 간에 분산됩니다.  
  
 작업 스레드는 입력 및 출력 작업 목록을 모두 포함할 수 있으며 실행 계획에서 *WorkThreadn*으로 식별됩니다. 여기서 *n*은 0부터 시작하는 작업 스레드 번호입니다. 그래프에 비동기 출력을 사용하는 구성 요소가 포함된 경우 이러한 스레드에는 출력 작업 목록이 포함됩니다.  
  
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
>  실행 계획은 패키지가 실행될 때마다 생성되며, 패키지에 로그 공급자를 추가하고 로깅을 사용하도록 설정한 다음 **PipelineExecutionPlan** 이벤트를 선택하면 실행 계획을 캡처할 수 있습니다.  
  
## <a name="understanding-buffer-allocation"></a>버퍼 할당 이해  
 실행 계획에 따라 데이터 흐름 태스크에서는 데이터 흐름 구성 요소의 출력에 정의된 열을 포함하는 버퍼를 만듭니다. 이 버퍼는 비동기 출력을 사용하는 구성 요소가 나타날 때까지 구성 요소의 시퀀스를 통해 데이터 흐름으로 재사용됩니다. 그런 다음 비동기 출력의 출력 열과 다운 스트림 구성 요소의 출력 열을 포함하는 새 버퍼가 만들어집니다.  
  
 실행 중 구성 요소에서는 현재 원본 또는 작업 스레드의 버퍼에 액세스할 수 있습니다. 이 버퍼는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드에 의해 제공된 입력 버퍼이거나 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드에 의해 제공된 출력 버퍼입니다. <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.Mode%2A>의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 속성도 각 버퍼를 입력 또는 출력 버퍼로 식별합니다.  
  
 비동기 출력을 사용하는 변환은 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 메서드에서 기존 입력 버퍼를 받고 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 메서드에서 새 출력 버퍼를 받습니다. 비동기 출력을 사용하는 구성 요소는 데이터 흐름에서 입력 버퍼와 출력 버퍼를 모두 받는 유일한 유형의 구성 요소입니다.  
  
 구성 요소에 제공된 버퍼에는 구성 요소의 입력 또는 출력 열 컬렉션에 있는 것보다 많은 열이 포함될 수 있으므로 구성 요소 개발자는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> 메서드를 호출하고 **LineageID**를 지정하여 버퍼에서 열을 찾을 수 있습니다.  
  
