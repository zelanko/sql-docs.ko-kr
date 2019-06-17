---
title: WMI 데이터 판독기 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 12340ae2ba13bf6219cf9940a56eeaa8b995f3e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829496"
---
# <a name="wmi-data-reader-task"></a>WMI 데이터 판독기 태스크
  WMI 데이터 판독기 태스크는 WMI(Windows Management Instrumentation) 쿼리 언어를 사용하여 WMI로부터 컴퓨터 시스템에 대한 정보를 반환하는 쿼리를 실행합니다. WMI 데이터 판독기 태스크는 다음 용도로 사용할 수 있습니다.  
  
-   로컬 또는 원격 컴퓨터의 Windows 이벤트 로그를 쿼리하고 정보를 파일이나 변수에 기록합니다.  
  
-   하드웨어 구성 요소의 설치 여부, 상태 또는 속성에 대한 정보를 가져온 후 이 정보를 사용하여 제어 흐름에서 다른 태스크를 실행할지 여부를 결정합니다.  
  
-   애플리케이션 목록을 가져오고 설치된 각 애플리케이션의 버전을 확인합니다.  
  
 다음과 같은 방법으로 WMI 데이터 판독기 태스크를 구성할 수 있습니다.  
  
-   사용할 WMI 연결 관리자를 지정합니다.  
  
-   WQL 쿼리의 원본을 지정합니다. 쿼리는 태스크 속성에 저장하거나 변수 또는 파일과 같은 태스크 외부에 저장할 수 있습니다.  
  
-   WQL 쿼리 결과의 형식을 정의합니다. 태스크에는 테이블, 속성 이름/값의 쌍 또는 속성 값 형식이 지원됩니다.  
  
-   쿼리 대상을 지정합니다. 대상은 변수 또는 파일일 수 있습니다.  
  
-   쿼리 대상을 덮어쓰거나, 유지하거나, 추가할지 여부를 나타냅니다.  
  
 원본 또는 대상이 파일인 경우 WMI 데이터 판독기 태스크는 파일 연결 관리자를 사용하여 파일에 연결합니다. 자세한 내용은 [Flat File Connection Manager](../connection-manager/file-connection-manager.md)을 참조하세요.  
  
 WMI 데이터 판독기 태스크는 WMI 연결 관리자를 사용하여 WMI 정보를 읽어 온 서버에 연결합니다. 자세한 내용은 [WMI Connection Manager](../connection-manager/wmi-connection-manager.md)을 참조하세요.  
  
## <a name="wql-query"></a>WQL 쿼리  
 WQL은 WMI 이벤트 알림 및 기타 WMI 관련 기능을 지원하기 위한 확장 기능이 포함된 SQL의 언어입니다. WQL에 대한 자세한 내용은 [MSDN Library](https://go.microsoft.com/fwlink/?linkid=7022)에서 WMI(Windows Management Instrumentation) 설명서를 참조하십시오.  
  
> [!NOTE]  
>  WMI 클래스는 Windows 버전마다 다릅니다.  
  
 다음 WQL 쿼리는 애플리케이션 로그 이벤트의 항목을 반환합니다.  
  
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
 다음 표에서는 WMI 데이터 판독기 태스크에 대한 사용자 지정 로그 항목을 나열합니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 로깅](../performance/integration-services-ssis-logging.md) 및 [로깅할 메시지 사용자 지정](../custom-messages-for-logging.md)을 참조하세요.  
  
|로그 항목|Description|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|태스크에서 WMI 데이터 읽기를 시작했음을 나타냅니다.|  
|`WMIDataReaderOperation`|태스크에서 실행한 WQL 쿼리를 보고합니다.|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>WMI 데이터 판독기 태스크 구성  
 프로그래밍 방식을 통해 또는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [WMI 데이터 판독기 태스크 편집기&#40;WMI 옵션 페이지&#41;](../wmi-data-reader-task-editor-wmi-options-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 태스크](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  
