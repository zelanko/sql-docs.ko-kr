---
title: "SharePoint용 파워 피벗 서버 시작 또는 중지 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e38e6366-9f20-4db0-b2a8-da7d5adf00eb
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# SharePoint용 파워 피벗 서버 시작 또는 중지
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 및 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 인스턴스는 SharePoint 팜에서 요청 및 데이터 처리를 조정할 수 있도록 동일한 로컬 응용 프로그램 서버에서 함께 작동합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [서비스 종속성](#dependencies)  
  
 [서비스 시작 또는 중지](#startstop)  
  
 [파워 피벗 서버 중지의 영향](#effects)  
  
##  <a name="dependencies"></a> 서비스 종속성  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스는 동일한 실제 서버에 함께 설치되어 있는 로컬 Analysis Services 서버 인스턴스를 사용합니다. 즉, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스를 중지하는 경우 로컬 Analysis Services 서버 인스턴스도 수동으로 중지해야 합니다. 두 서비스 중 하나만 실행하는 경우에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 처리에 대해 요청 할당 오류가 발생합니다.  
  
 Analysis Services 서버는 문제를 진단하거나 문제를 해결할 경우에만 자체적으로 실행되어야 합니다. 다른 모든 경우에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스가 동일한 서버에서 로컬로 실행되어야 합니다.  
  
##  <a name="startstop"></a> 서비스 시작 또는 중지  
 항상 중앙 관리를 사용하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 또는 Analysis Services 서버 인스턴스를 시작하거나 중지합니다. 중앙 관리를 사용하면 같은 페이지에서 서비스를 함께 시작하거나 중지할 수 있습니다. 또한 중앙 관리에서는 **하나 이상의 서비스가 시작했거나 중지했습니다.** 타이머 작업을 사용하여 실행 중이어야 하는 서비스를 다시 시작합니다. SharePoint 이외의 도구를 사용하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 또는 Analysis Services를 중지하면 타이머 작업 실행 시 서비스가 다시 시작됩니다.  
  
 서비스 시작 및 중지는 물리적 서비스 인스턴스에 적용되는 동작입니다. 팜에 추가 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버가 있는 경우 팜 내의 다른 서버는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 요청을 계속 수락합니다.  
  
 팜에서 모든 물리적 서비스를 동시에 시작하거나 중지할 수 없습니다. 각 서버를 선택한 다음 특정 서비스를 시작하거나 중지해야 합니다.  
  
 특정 웹 응용 프로그램에 대해 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스를 시작, 일시 중지 또는 중지할 수는 없지만 서비스를 사용하지 못하도록 기본 연결 목록에서 제거할 수는 있습니다. 자세한 내용은 [중앙 관리에서 SharePoint 웹 응용 프로그램에 파워 피벗 서비스 응용 프로그램 연결](../../analysis-services/power-pivot-sharepoint/connect power pivot service app to sharepoint web app in ca.md)을 참조하세요.  
  
1.  중앙 관리의 **시스템 설정**에서 **서버의 서비스 관리**를 클릭합니다.  
  
2.  페이지 맨 위의 서버에서 아래쪽 화살표를 클릭한 다음 **서버 변경**을 클릭합니다.  
  
3.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스가 있는 SharePoint 서버를 선택하거나 시작 또는 중지하려는 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 인스턴스를 선택합니다.  
  
4.  서비스를 선택한 다음 동작을 클릭합니다. 서비스를 쌍으로 시작 또는 중지해야 합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스를 시작 또는 중지하는 경우 동일한 컴퓨터에서 실행되는 Analysis Services 서버 인스턴스도 시작 또는 중지해야 합니다.  
  
##  <a name="effects"></a> 파워 피벗 서버 중지의 영향  
 다음 표에서는 SharePoint 서버에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 및 Analysis Services 서비스를 중지할 때의 영향에 대해 설명합니다.  
  
|영향|Description|  
|---------------|-----------------|  
|기존 쿼리|Analysis Services 서버에서 진행 중인 쿼리가 즉시 중지됩니다. 사용자에게 데이터를 찾을 수 없거나 데이터 원본 연결을 찾을 수 없다는 오류가 표시됩니다.|  
|현재 처리 중인 기존 데이터 새로 고침 작업|현재 Analysis Services 서버에서 진행 중인 작업이 즉시 중지됩니다. 데이터 새로 고침 작업에 실패하고 데이터 새로 고침 기록에 오류가 기록됩니다.<br /><br /> SharePoint 중앙 관리의 작업 상태 확인 페이지를 사용하여 서비스를 중지하기 전에 현재 작업의 상태를 볼 수 있습니다.<br /><br /> 현재 처리 중인 작업이 무엇인지 알 수 있지만 시작하려는 다른 작업이 있는지 확인하기 위해 큐 자체를 볼 수는 없습니다.|  
|큐의 기존 데이터 새로 고침 요청|예약된 데이터 새로 고침 요청이 일정의 전체 주기를 완료하기 위해 처리 큐에 남습니다. 즉, 다음 시작 시까지 큐에 유지됩니다. 그때까지 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스가 다시 시작되지 않을 경우 데이터 새로 고침 요청이 삭제되고 오류가 기록됩니다.|  
|쿼리나 데이터 새로 고침에 대한 새로운 요청|팜에서 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버만 중지하는 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 새 요청이 처리되지 않으며 데이터를 요청하면 데이터를 찾을 수 없다는 오류가 발생합니다.<br /><br /> SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버가 더 있는 경우 요청이 사용 가능한 서버 중 하나로 전달됩니다.|  
|사용 데이터|서비스가 중지된 동안에는 사용 데이터가 수집되지 않습니다.|  
  
## 관련 항목:  
 [Power Pivot 서비스 계정 구성](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)  
  
  