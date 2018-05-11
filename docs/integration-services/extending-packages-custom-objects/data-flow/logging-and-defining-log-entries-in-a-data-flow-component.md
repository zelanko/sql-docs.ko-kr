---
title: 데이터 흐름 구성 요소에서 로그 항목 로깅 및 정의 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-custom-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- logs [Integration Services], custom
- custom log entries [Integration Services]
- custom data flow components [Integration Services], logging
- data flow components [Integration Services], logging
ms.assetid: 2190dba9-59b5-480b-b8e9-21d5a54c5917
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c73ada1f927496cc9758a1e43ba9577c727d1dd0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="logging-and-defining-log-entries-in-a-data-flow-component"></a>데이터 흐름 구성 요소에서 로그 항목 로깅 및 정의
  사용자 지정 데이터 흐름 구성 요소에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.PostLogMessage%2A> 인터페이스의 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 메서드를 사용하여 기존 로그 항목에 메시지를 게시할 수 있습니다. 또한 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A> 메서드나 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스의 유사한 메서드를 사용하여 사용자에게 정보를 제공할 수도 있습니다. 그러나 이 방법을 사용할 경우 추가 이벤트를 발생시키고 처리하는 오버헤드가 발생하며 사용자가 직접 관심 있는 메시지에 대한 자세한 정보 메시지를 조사해야 합니다. 아래에서 설명하는 대로 사용자 지정 로그 항목을 사용하면 구성 요소 사용자에게 고유한 레이블이 지정된 사용자 지정 로그 정보를 제공할 수 있습니다.  
  
## <a name="registering-and-using-a-custom-log-entry"></a>사용자 지정 로그 항목 등록 및 사용  
  
### <a name="registering-a-custom-log-entry"></a>사용자 지정 로그 항목 등록  
 구성 요소에서 사용할 사용자 지정 로그 항목을 등록하려면 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterLogEntries%2A> 기본 클래스의 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 메서드를 재정의합니다. 다음 예에서는 사용자 지정 로그 항목을 등록하고 이름과 설명을 지정합니다.  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime;  
...  
private const string MyLogEntryName = "My Custom Component Log Entry";  
private const string MyLogEntryDescription = "Log entry from My Custom Component ";  
...  
    public override void RegisterLogEntries()  
    {  
      this.LogEntryInfos.Add(MyLogEntryName,  
        MyLogEntryDescription,  
        Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT);  
    }  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
...  
Private Const MyLogEntryName As String = "My Custom Component Log Entry"   
Private Const MyLogEntryDescription As String = "Log entry from My Custom Component "  
...  
Public  Overrides Sub RegisterLogEntries()   
  Me.LogEntryInfos.Add(MyLogEntryName, _  
    MyLogEntryDescription, _  
    Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT)   
End Sub  
```  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency> 열거형은 이벤트가 기록되는 빈도에 대한 힌트를 런타임에 제공합니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_OCCASIONAL>: 이벤트가 실행 시마다 로깅되는 것이 아니라 가끔씩만 로깅됩니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>: 이벤트가 실행 시마다 일정 횟수만큼 로깅됩니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_PROPORTIONAL>: 이벤트가 완료된 작업 양에 비례하여 여러 번 로깅됩니다.  
  
 위의 예에서는 구성 요소가 실행 시마다 한 번씩 로그 항목을 로깅해야 하므로 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>를 사용합니다.  
  
 사용자 지정 로그 항목을 등록하고 데이터 흐름 디자이너 화면에 사용자 지정 구성 요소의 인스턴스를 추가한 후에는 디자이너의 **로깅** 대화 상자에 있는 사용 가능한 로그 항목 목록에 "My Custom Component Log Entry"라는 이름의 새 로그 항목이 표시됩니다.  
  
### <a name="logging-to-a-custom-log-entry"></a>사용자 지정 로그 항목에 로깅  
 사용자 지정 로그 항목을 등록한 후에는 구성 요소에서 사용자 지정 메시지를 로깅할 수 있습니다. 다음 예에서는 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 메서드 실행 중에 구성 요소에서 사용되는 SQL 문의 텍스트를 포함하는 사용자 지정 로그 항목을 작성합니다.  
  
```csharp  
public override void PreExecute()  
{  
  DateTime now = DateTime.Now;  
  byte[] additionalData = null;  
  this.ComponentMetaData.PostLogMessage(MyLogEntryName,  
    this.ComponentMetaData.Name,  
    "Command Sent was: " + myCommand.CommandText,  
    now, now, 0, ref additionalData);  
}  
```  
  
```vb  
Public  Overrides Sub PreExecute()   
  Dim now As DateTime = DateTime.Now   
  Dim additionalData As Byte() = Nothing   
  Me.ComponentMetaData.PostLogMessage(MyLogEntryName, _  
    Me.ComponentMetaData.Name, _  
    "Command Sent was: " + myCommand.CommandText, _  
    now, now, 0, additionalData)   
End Sub  
```  
  
 이제 사용자가 패키지를 실행하고 **로깅** 대화 상자에서 "My Custom Component Log Entry"를 선택하면 "User::My Custom Component Log Entry"라는 레이블이 지정된 항목이 로그에 포함됩니다. 이 새 로그 항목에는 SQL 문, 타임스탬프 및 개발자가 로깅한 추가 데이터의 텍스트가 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 로깅](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
