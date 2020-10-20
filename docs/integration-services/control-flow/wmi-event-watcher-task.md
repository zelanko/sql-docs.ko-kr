---
description: WMI 이벤트 감시자 태스크
title: WMI 이벤트 감시자 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmieventwatchertask.f1
- sql13.dts.designer.wmieventwatcher.general.f1
- sql13.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d40281b9c233b55b41cfc8fc18040fb3e6c4d927
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195979"
---
# <a name="wmi-event-watcher-task"></a>WMI 이벤트 감시자 태스크

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  WMI 이벤트 감시자 태스크는 WQL(WMI Query Language) 이벤트 쿼리를 사용하여 특정 이벤트를 지정하기 위해 WMI(Windows Management Instrumentation) 이벤트를 감시합니다. WMI 이벤트 감시자 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   파일이 폴더에 추가되었다는 알림을 기다린 후 파일 처리를 시작합니다.  
  
-   서버에서 사용 가능한 메모리가 지정된 백분율 아래로 떨어지면 파일을 삭제하는 패키지를 실행합니다.  
  
-   애플리케이션 설치를 감시한 후 애플리케이션을 사용하는 패키지를 실행합니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 WMI 정보를 읽는 태스크가 포함됩니다.  
  
 이 태스크에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [WMI 데이터 판독기 태스크](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
## <a name="wql-queries"></a>WQL 쿼리  
 WQL은 WMI 이벤트 알림 및 기타 WMI 관련 기능을 지원하기 위한 확장 기능이 포함된 SQL의 언어입니다. WQL에 대한 자세한 내용은 [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553)에서 WMI(Windows Management Instrumentation) 설명서를 참조하십시오.  
  
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
  
## <a name="custom-logging-messages-available-on-the-wmi-event-watcher-task"></a>WMI 이벤트 감시자 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 WMI 이벤트 감시자 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|태스크에서 모니터링하고 있는 이벤트가 발생했음을 나타냅니다.|  
|**WMIEventWatcherTimedout**|태스크 시간이 초과되었음을 나타냅니다.|  
|**WMIEventWatcherWatchingForWMIEvents**|태스크에서 WQL 쿼리 실행을 시작했음을 나타냅니다. 이 항목은 해당 쿼리를 포함합니다.|  
  
## <a name="configuration-of-the-wmi-event-watcher-task"></a>WMI 이벤트 감시자 태스크 구성  
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
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>WMI 이벤트 감시자 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
## <a name="wmi-event-watcher-task-editor-general-page"></a>WMI 이벤트 감시자 태스크 편집기(일반 페이지)
  **WMI 이벤트 감시자 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 WMI 이벤트 감시자 태스크의 이름을 지정하고 설명할 수 있습니다.  
  
 WQL(WMI Query Language)에 대한 자세한 내용은 MSDN 라이브러리의 WMI(Windows Management Instrumentation) 항목인 [Querying with WQL](/windows/win32/wmisdk/querying-with-wql)(WQL을 사용하여 쿼리)을 참조하세요.  
  
### <a name="options"></a>옵션  
 **이름**  
 WMI 이벤트 감시자 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 WMI 이벤트 감시자 태스크에 대한 설명을 입력합니다.  
  
## <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>WMI 이벤트 감시자 태스크 편집기(WMI 옵션 페이지)
  **WMI 이벤트 감시자 태스크 편집기** 대화 상자의 **WMI 옵션** 페이지를 사용하여 WQL(Windows Management Instrumentation Query Language) 쿼리의 원본 및 WMI 이벤트 감시자 태스크가 Microsoft Windows Instrumentation(WMI) 이벤트에 응답하는 방식을 지정할 수 있습니다.  
  
 WQL(WMI Query Language)에 대한 자세한 내용은 MSDN 라이브러리의 WMI(Windows Management Instrumentation) 항목인 [Querying with WQL](/windows/win32/wmisdk/querying-with-wql)(WQL을 사용하여 쿼리)을 참조하세요.  
  
### <a name="static-options"></a>정적 옵션  
 **WMIConnectionName**  
 목록에서 WMI 연결 관리자를 선택하거나 \<**New WMI Connection...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [WMI 연결 관리자](../../integration-services/connection-manager/wmi-connection-manager.md), [WMI 연결 관리자 편집기](../connection-manager/wmi-connection-manager.md)  
  
 **WQLQuerySourceType**  
 태스크에서 실행하는 WQL 쿼리의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
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
  
### <a name="wqlquerysource-dynamic-options"></a>WQLQuerySource 동적 옵션  
  
#### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = 직접 입력  
 **WQLQuerySource**  
 쿼리를 입력하거나, 줄임표 단추(...)를 클릭하고 **WQL 쿼리** 대화 상자를 사용하여 쿼리를 입력합니다.  
  
#### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = 파일 연결  
 **WQLQuerySource**  
 목록에서 파일 연결 관리자를 선택하거나 \<**New connection...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [파일 연결 관리자](../../integration-services/connection-manager/file-connection-manager.md), [파일 연결 관리자 편집기](../connection-manager/file-connection-manager.md)  
  
#### <a name="wqlquerysource--variable"></a>WQLQuerySource = 변수  
 **WQLQuerySource**  
 목록에서 변수를 선택하거나 \<**New variable...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](../integration-services-ssis-variables.md)  
