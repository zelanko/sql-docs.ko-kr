---
title: "중앙 관리에서 SharePoint 웹 응용 프로그램에 파워 피벗 서비스 응용 프로그램 연결 | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 중앙 관리에서 SharePoint 웹 응용 프로그램에 파워 피벗 서비스 응용 프로그램 연결
  팜의 여러 SharePoint 웹 응용 프로그램에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 사용할 수 있습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 사용할 수 있도록 하려면 서비스 연결 목록에 해당 응용 프로그램을 추가합니다.  
  
> [!IMPORTANT]  
>  기본 그룹에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램이 하나 있어야 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 관리 대시보드가 제대로 작동합니다. 기본 그룹에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 둘 이상 추가하지 마세요. 같은 서비스 응용 프로그램 유형의 여러 항목을 추가하는 구성은 지원되지 않으며 오류가 발생할 수 있습니다. 추가 서비스 응용 프로그램을 만들 경우 사용자 지정 목록에 추가하십시오.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [기본 그룹에 파워 피벗 서비스 응용 프로그램 추가](#default)  
  
 [사용자 지정 서비스 연결 목록에 파워 피벗 서비스 응용 프로그램 추가](#custom)  
  
##  <a name="default"></a> 기본 그룹에 서비스 응용 프로그램 추가  
 서비스 연결 목록은 팜의 다른 SharePoint 웹 응용 프로그램에 리소스를 제공하는 공유 서비스의 목록입니다. 팜에는 하나의 기본 서비스 연결 그룹이 있습니다.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 목록에 추가하려면 응용 프로그램을 만들 때나 나중에 다음 단계를 사용하여 추가할 수 있습니다.  
  
1.  중앙 관리의 **응용 프로그램 관리**에서 **서비스 응용 프로그램 연결 구성**을 클릭합니다.  
  
2.  응용 프로그램 프록시 그룹에서 **기본값**을 클릭합니다.  
  
3.  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램(형식 이름 **파워 피벗 서비스 응용 프로그램 프록시**로 표시) 옆에 있는 확인란을 선택합니다. 둘 이상의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램이 있는 경우 하나만 선택합니다.  
  
4.  **확인**을 클릭합니다.  
  
##  <a name="custom"></a> 사용자 지정 서비스 연결 목록에 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램 추가  
 기본 그룹을 사용자 지정 목록으로 바꿀 수 있습니다. 특히 하나의 SharePoint 웹 응용 프로그램에 대해 사용자 지정 목록이 작성됩니다. 기본 그룹이 무시되고 팜 또는 서비스 관리자가 지정한 서비스 연결만으로 기본 그룹이 대체됩니다. 여러 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 만든 경우 사용자 지정 목록을 사용하여 사용할 응용 프로그램을 지정해야 합니다. 사용자 지정 목록을 다른 웹 응용 프로그램에서 다시 사용할 수 없습니다. 이는 작성된 웹 응용 프로그램에만 적용됩니다.  
  
1.  중앙 관리의 **응용 프로그램 관리**에서 **웹 응용 프로그램 관리**를 클릭합니다.  
  
2.  응용 프로그램(예: SharePoint -80)을 선택합니다.  
  
3.  웹 응용 프로그램의 관리에서 **서비스 연결**을 클릭합니다.  
  
4.  **다음 연결 그룹 편집**에서 **[사용자 지정]**을 선택합니다.  
  
5.  사용할 각 서비스 응용 프로그램 연결 옆에 있는 확인란을 선택합니다. 여러 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램(**파워 피벗 서비스 응용 프로그램 프록시**로 설정된 형식으로 표시)이 있는 경우 하나만 선택해야 합니다.  
  
6.  **확인**을 클릭합니다.  
  
## 관련 항목:  
 [중앙 관리에서 PowerPivot 서비스 응용 프로그램 만들기 및 구성](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [초기 구성(SharePoint용 파워 피벗)](http://msdn.microsoft.com/ko-kr/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)  
  
  