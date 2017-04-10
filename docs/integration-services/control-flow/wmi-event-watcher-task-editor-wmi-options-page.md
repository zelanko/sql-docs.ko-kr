---
title: "WMI 이벤트 감시자 태스크 편집기(WMI 옵션 페이지) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.wmieventwatcher.wmiquery.f1"
helpviewer_keywords: 
  - "WMI 이벤트 감시자 태스크 편집기"
ms.assetid: 525f3de7-a021-4e52-9939-3a83c88f131a
caps.latest.revision: 38
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# WMI 이벤트 감시자 태스크 편집기(WMI 옵션 페이지)
  **WMI 이벤트 감시자 태스크 편집기** 대화 상자의 **WMI 옵션** 페이지를 사용하여 WQL(Windows Management Instrumentation Query Language) 쿼리의 원본 및 WMI 이벤트 감시자 태스크가 Microsoft Windows Instrumentation(WMI) 이벤트에 응답하는 방식을 지정할 수 있습니다.  
  
 이 태스크에 대한 자세한 내용은 [WMI Event Watcher Task](../../integration-services/control-flow/wmi-event-watcher-task.md)를 참조하십시오. WQL(WMI Query Language)에 대한 자세한 내용은 MSDN 라이브러리의 WMI(Windows Management Instrumentation) 항목인 [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)(WQL을 사용하여 쿼리)을 참조하세요.  
  
## 정적 옵션  
 **WMIConnectionName**  
 목록에서 WMI 연결 관리자를 선택하거나 \<**새 WMI 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [WMI 연결 관리자](../../integration-services/connection-manager/wmi-connection-manager.md), [WMI 연결 관리자 편집기](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 태스크에서 실행하는 WQL 쿼리의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**직접 입력**|WQL 쿼리에 대한 원본을 설정합니다. 이 값을 선택하면 동적 옵션 **WQLQuerySource**가 표시됩니다.|  
|**파일 연결**|WQL 쿼리가 포함된 파일을 선택합니다. 이 값을 선택하면 동적 옵션 **WQLQuerySource**가 표시됩니다.|  
|**변수**|WQL 쿼리를 정의하는 변수에 대한 원본을 설정합니다. 이 값을 선택하면 동적 옵션 **WQLQuerySource**가 표시됩니다.|  
  
 **ActionAtEvent**  
 WMI 이벤트가 이벤트를 기록하고 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 동작을 시작할지, 아니면 이벤트만 기록할지를 지정합니다.  
  
 **AfterEvent**  
 WMI 이벤트를 수신한 후 태스크가 성공 또는 실패하도록 지정하거나 태스크가 이벤트가 다시 발생하는지 여부를 계속 감시하도록 지정합니다.  
  
 **ActionAtTimeout**  
 태스크가 WMI 쿼리에 대한 제한 시간 초과 발생을 기록하고 이에 대한 응답으로 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 이벤트를 시작할지, 아니면 제한 시간 초과 발생만 기록할지를 지정합니다.  
  
 **AfterTimeout**  
 제한 시간 초과에 대한 응답으로 태스크가 성공 또는 실패하도록 지정하거나 태스크가 제한 시간 초과가 다시 발생하는지 여부를 계속 감시하도록 지정합니다.  
  
 **NumberOfEvents**  
 감시할 이벤트의 수를 지정합니다.  
  
 **Timeout**  
 이벤트가 발생할 때까지 대기할 시간(초)을 지정합니다. 값 0은 제한 시간이 적용되지 않음을 의미합니다.  
  
## WQLQuerySource 동적 옵션  
  
### WQLQuerySource = 직접 입력  
 **WQLQuerySource**  
 쿼리를 제공하거나, 줄임표 단추(...)를 클릭하고 **WQL 쿼리** 대화 상자를 사용하여 쿼리를 입력합니다.  
  
### WQLQuerySource = 파일 연결  
 **WQLQuerySource**  
 목록에서 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### WQLQuerySource = 변수  
 **WQLQuerySource**  
 목록에서 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](../Topic/Add%20Variable.md)  
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [WMI 이벤트 감시자 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-general-page.md)   
 [식 페이지](../../integration-services/expressions/expressions-page.md)   
 [WMI 데이터 판독기 태스크](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
  