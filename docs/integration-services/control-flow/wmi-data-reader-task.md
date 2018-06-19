---
title: WMI 데이터 판독기 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmidatareadertask.f1
- sql13.dts.designer.wmidatareadertask.general.f1
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 881118c9747dca1a328bd091bf1bfee017e2bbb5
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35405865"
---
# <a name="wmi-data-reader-task"></a>WMI 데이터 판독기 태스크
  WMI 데이터 판독기 태스크는 WMI(Windows Management Instrumentation) 쿼리 언어를 사용하여 WMI로부터 컴퓨터 시스템에 대한 정보를 반환하는 쿼리를 실행합니다. WMI 데이터 판독기 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   로컬 또는 원격 컴퓨터의 Windows 이벤트 로그를 쿼리하고 정보를 파일이나 변수에 기록합니다.  
  
-   하드웨어 구성 요소의 설치 여부, 상태 또는 속성에 대한 정보를 가져온 후 이 정보를 사용하여 제어 흐름에서 다른 태스크를 실행할지 여부를 결정합니다.  
  
-   응용 프로그램 목록을 가져오고 설치된 각 응용 프로그램의 버전을 확인합니다.  
  
 다음과 같은 방법으로 WMI 데이터 판독기 태스크를 구성할 수 있습니다.  
  
-   사용할 WMI 연결 관리자를 지정합니다.  
  
-   WQL 쿼리의 원본을 지정합니다. 쿼리는 태스크 속성에 저장하거나 변수 또는 파일과 같은 태스크 외부에 저장할 수 있습니다.  
  
-   WQL 쿼리 결과의 형식을 정의합니다. 태스크에는 테이블, 속성 이름/값의 쌍 또는 속성 값 형식이 지원됩니다.  
  
-   쿼리 대상을 지정합니다. 대상은 변수 또는 파일일 수 있습니다.  
  
-   쿼리 대상을 덮어쓰거나, 유지하거나, 추가할지 여부를 나타냅니다.  
  
 원본 또는 대상이 파일인 경우 WMI 데이터 판독기 태스크는 파일 연결 관리자를 사용하여 파일에 연결합니다. 자세한 내용은 [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md)을 참조하세요.  
  
 WMI 데이터 판독기 태스크는 WMI 연결 관리자를 사용하여 WMI 정보를 읽어 온 서버에 연결합니다. 자세한 내용은 [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md)을 참조하세요.  
  
## <a name="wql-query"></a>WQL 쿼리  
 WQL은 WMI 이벤트 알림 및 기타 WMI 관련 기능을 지원하기 위한 확장 기능이 포함된 SQL의 언어입니다. WQL에 대한 자세한 내용은 [MSDN Library](http://go.microsoft.com/fwlink/?linkid=7022)에서 WMI(Windows Management Instrumentation) 설명서를 참조하십시오.  
  
> [!NOTE]  
>  WMI 클래스는 Windows 버전마다 다릅니다.  
  
 다음 WQL 쿼리는 응용 프로그램 로그 이벤트의 항목을 반환합니다.  
  
```  
SELECT * FROM Win32_NTLogEvent WHERE LogFile = 'Application' AND (SourceName='SQLISService' OR SourceName='SQLISPackage') AND TimeGenerated > '20050117'  
```  
  
 다음 WQL 쿼리는 논리적 디스크 정보를 반환합니다.  
  
```  
SELECT FreeSpace, DeviceId, Size, SystemName, Description FROM Win32_LlogicalDisk  
```  
  
 다음 WQL 쿼리는 운영 체제에 대한 QFE(Quick Fix Engineering) 업데이트 목록을 반환합니다.  
  
```  
Select * FROM Win32_QuickFixEngineering  
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-data-reader-task"></a>WMI 데이터 판독기 태스크에 사용할 수 있는 사용자 지정 로깅 메시지  
 다음 표에서는 WMI 데이터 판독기 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)을 참조하세요.  
  
|로그 항목|설명|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|태스크에서 WMI 데이터 읽기를 시작했음을 나타냅니다.|  
|**WMIDataReaderOperation**|태스크에서 실행한 WQL 쿼리를 보고합니다.|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>WMI 데이터 판독기 태스크 구성  
 프로그래밍 방식을 통해 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="wmi-data-reader-task-editor-general-page"></a>WMI 데이터 판독기 태스크 편집기(일반 페이지)
  **WMI 데이터 판독기 태스크 편집기** 대화 상자의 **일반** 페이지를 사용하여 WMI 데이터 판독기 태스크를 명명 및 설명할 수 있습니다.  
  
  WQL(WMI Query Language)에 대한 자세한 내용은 MSDN 라이브러리의 WMI(Windows Management Instrumentation) 항목인 [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)(WQL을 사용하여 쿼리)을 참조하세요.  
  
### <a name="options"></a>변수  
 **이름**  
 WMI 데이터 판독기 태스크에 사용할 고유 이름을 제공합니다. 이 이름은 태스크 아이콘에서 레이블로 사용됩니다.  
  
> [!NOTE]  
>  태스크 이름은 패키지 내에서 고유해야 합니다.  
  
 **설명**  
 WMI 데이터 판독기 태스크에 대한 설명을 입력합니다.  
  
## <a name="wmi-data-reader-task-editor-wmi-options-page"></a>WMI 데이터 판독기 태스크 편집기(WMI 옵션 페이지)
  **WMI 데이터 판독기 태스크 편집기** 대화 상자의 **WMI 옵션** 페이지를 사용하여 WQL(WMI Query Language) 쿼리의 원본 및 쿼리 결과의 대상을 지정할 수 있습니다.  
  
 WQL(WMI Query Language)에 대한 자세한 내용은 MSDN 라이브러리의 WMI(Windows Management Instrumentation) 항목인 [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)(WQL을 사용하여 쿼리)을 참조하세요.  
  
### <a name="static-options"></a>정적 옵션  
 **WMIConnectionName**  
 목록에서 WMI 연결 관리자를 선택하거나 \<**새 WMI 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [WMI 연결 관리자](../../integration-services/connection-manager/wmi-connection-manager.md), [WMI 연결 관리자 편집기](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 태스크에서 실행하는 WQL 쿼리의 원본 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**직접 입력**|WQL 쿼리에 대한 원본을 설정합니다. 이 값을 선택하면 동적 옵션 **WQLQuerySourceType**이 표시됩니다.|  
|**파일 연결**|WQL 쿼리가 포함된 파일을 선택합니다. 이 값을 선택하면 동적 옵션 **WQLQuerySourceType**이 표시됩니다.|  
|**변수**|원본을 WQL 쿼리를 정의하는 변수로 설정합니다. 이 값을 선택하면 동적 옵션 **WQLQuerySourceType**이 표시됩니다.|  
  
 **OutputType**  
 출력 유형을 데이터 테이블, 속성 값 또는 속성 이름 및 값으로 지정합니다.  
  
 **OverwriteDestination**  
 대상 파일 또는 변수의 원본 데이터에 대한 유지, 덮어쓰기 또는 추가 여부를 지정합니다.  
  
 **DestinationType**  
 태스크에서 실행하는 WQL 쿼리의 대상 유형을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**파일 연결**|WQL 쿼리 결과를 저장할 파일을 선택합니다. 이 값을 선택하면 동적 옵션인 **DestinationType**이 표시됩니다.|  
|**변수**|WQL 쿼리 결과를 저장할 변수를 설정합니다. 이 값을 선택하면 동적 옵션인 **DestinationType**이 표시됩니다.|  
  
### <a name="wqlquerysourcetype-dynamic-options"></a>WQLQuerySourceType 동적 옵션  
  
#### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = 직접 입력  
 **WQLQuerySource**  
 쿼리를 제공하거나, 줄임표(...)를 클릭하고 **WQL 쿼리** 대화 상자를 사용하여 쿼리를 입력합니다.  
  
#### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = 파일 연결  
 **WQLQuerySource**  
 목록에서 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = 변수  
 **WQLQuerySource**  
 목록에서 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
### <a name="destinationtype-dynamic-options"></a>DestinationType 동적 옵션  
  
#### <a name="destinationtype--file-connection"></a>DestinationType = 파일 연결  
 **대상**  
 목록에서 파일 연결 관리자를 선택하거나 \<**새 연결...**>을 클릭하여 새 연결 관리자를 만듭니다.  
  
 **관련 항목:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="destinationtype--variable"></a>DestinationType = 변수  
 **대상**  
 목록에서 변수를 선택하거나 \<**새 변수...**>를 클릭하여 새 변수를 만듭니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md), [변수 추가](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  
