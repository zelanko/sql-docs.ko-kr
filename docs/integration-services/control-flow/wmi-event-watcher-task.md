---
title: "WMI 이벤트 감시자 태스크 | Microsoft Docs"
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
  - "sql13.dts.designer.wmieventwatchertask.f1"
helpviewer_keywords: 
  - "WQL [Integration Services]"
  - "WMI 이벤트 감시자 태스크 [Integration Services]"
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
caps.latest.revision: 53
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 53
---
# WMI 이벤트 감시자 태스크
  WMI 이벤트 감시자 태스크는 WQL(WMI Query Language) 이벤트 쿼리를 사용하여 특정 이벤트를 지정하기 위해 WMI(Windows Management Instrumentation) 이벤트를 감시합니다. WMI 이벤트 감시자 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   파일이 폴더에 추가되었다는 알림을 기다린 후 파일 처리를 시작합니다.  
  
-   서버에서 사용 가능한 메모리가 지정된 백분율 아래로 떨어지면 파일을 삭제하는 패키지를 실행합니다.  
  
-   응용 프로그램 설치를 감시한 후 응용 프로그램을 사용하는 패키지를 실행합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 WMI 정보를 읽는 태스크가 포함됩니다.  
  
 이 태스크에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [WMI 데이터 판독기 태스크](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
## WQL 쿼리  
 WQL은 WMI 이벤트 알림 및 기타 WMI 관련 기능을 지원하기 위한 확장 기능이 포함된 SQL의 언어입니다. WQL에 대한 자세한 내용은 [MSDN Library](http://go.microsoft.com/fwlink/?linkid=62553)에서 WMI(Windows Management Instrumentation) 설명서를 참조하십시오.  
  
> [!NOTE]  
>  WMI 클래스는 Windows 버전마다 다릅니다.  
  
 다음 쿼리는 CPU 사용이 40%를 넘는 알림을 감시합니다.  
  
```  
SELECT * from __InstanceModificationEvent WITHIN 2 WHERE TargetInstance ISA 'Win32_Processor' and TargetInstance.LoadPercentage > 40  
```  
  
 다음 쿼리는 폴더에 추가된 파일 알림을 감시합니다.  
  
```  
SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "CIM_DirectoryContainsFile" and TargetInstance.GroupComponent= "Win32_Directory.Name=\"c:\\\\WMIFileWatcher\""   
```  
  
## WMI 이벤트 감시자 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 WMI 이벤트 감시자 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../../integration-services/performance/custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|태스크에서 모니터링하고 있는 이벤트가 발생했음을 나타냅니다.|  
|**WMIEventWatcherTimedout**|태스크 시간이 초과되었음을 나타냅니다.|  
|**WMIEventWatcherWatchingForWMIEvents**|태스크에서 WQL 쿼리 실행을 시작했음을 나타냅니다. 이 항목은 해당 쿼리를 포함합니다.|  
  
## WMI 이벤트 감시자 태스크 구성  
 다음과 같은 방법으로 WMI 데이터 판독기 태스크를 구성할 수 있습니다.  
  
-   사용할 WMI 연결 관리자를 지정합니다.  
  
-   WQL 쿼리의 원본을 지정합니다. 원본은 태스크, 변수 또는 파일의 외부에 있을 수 있으며 쿼리는 태스크 속성에 저장될 수 있습니다.  
  
-   WMI 이벤트가 발생할 때 태스크에서 취할 동작을 지정합니다. 이벤트 알림과 이벤트 이후의 상태를 로깅하거나 WMI 이벤트와 관련된 정보, 알림 및 이벤트 이후의 상태를 제공하는 사용자 지정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 이벤트를 발생시킬 수 있습니다.  
  
-   태스크가 이벤트에 대응하는 방법을 정의합니다. 이벤트에 따라 태스크가 성공 또는 실패하도록 구성하거나 단지 태스크에서 이벤트를 다시 감시하도록 할 수 있습니다.  
  
-   WMI 쿼리 시간이 종료될 때 태스크에서 취할 동작을 지정합니다. 시간 제한 및 시간 제한 이후의 상태를 로깅하거나 WMI 이벤트 시간이 종료되었고 해당 제한 시간과 제한 시간 상태를 로깅하도록 나타내는 사용자 지정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 이벤트를 발생시킬 수 있습니다.  
  
-   태스크가 시간 종료에 대응하는 방법을 정의합니다. 태스크가 성공 또는 실패하도록 구성하거나 단지 태스크에서 이벤트를 다시 감시하도록 할 수 있습니다.  
  
-   태스크가 이벤트를 감시하는 횟수를 지정합니다.  
  
-   제한 시간을 지정합니다.  
  
 원본이 파일인 경우 WMI 이벤트 감시자 태스크는 파일 연결 관리자를 사용하여 파일에 연결합니다. 자세한 내용은 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)을 참조하세요.  
  
 WMI 이벤트 감시자 태스크는 WMI 연결 관리자를 사용하여 WMI 정보를 읽어 온 서버에 연결합니다. 자세한 내용은 [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [WMI 이벤트 감시자 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-general-page.md)  
  
-   [WMI 이벤트 감시자 태스크 편집기&#40;WMI 옵션 페이지&#41;](../../integration-services/control-flow/wmi-event-watcher-task-editor-wmi-options-page.md)  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## WMI 이벤트 감시자 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
  