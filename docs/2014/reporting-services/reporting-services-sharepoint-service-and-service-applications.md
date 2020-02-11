---
title: Reporting Services SharePoint 서비스 및 서비스 응용 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 501aa9ee-8c13-458c-bf6f-24e00c82681b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93a8092dc9ed731349a1948a74e3950eb32f4f47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783155"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Reporting Services SharePoint Service 및 서비스 애플리케이션
  
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드는 SharePoint 서비스 아키텍처에 맞게 구축되었으며 SharePoint 서비스와 일대다 서비스 애플리케이션을 활용합니다. 서비스 애플리케이션을 만들면 서비스를 사용할 수 있게 되며 서비스 애플리케이션 데이터베이스가 생성됩니다. Reporting Services 서비스 애플리케이션은 여러 개 만들 수 있지만 대부분의 배포 시나리오에서 서비스 애플리케이션은 하나면 충분합니다.  
  
 이 항목에는 다음과 같은 정보가 포함되어 있습니다.  
  
-   [Reporting Services 서비스 응용 프로그램 만들기](#bkmk_createapp)  
  
-   [프록시 그룹과 서비스 응용 프로그램의 연결 수정](#bkmk_associations)  
  
-   [서비스 응용 프로그램 속성 편집](#bkmk_editserviceapplication)  
  
-   [PowerShell을 사용 하 여 Reporting Services 서비스 응용 프로그램을 만들려면](#bkmk_powershell_create_ssrs_serviceapp)  
  
-   [관련 작업](#bkmk_related)  
  
##  <a name="bkmk_createapp"></a>Reporting Services 서비스 응용 프로그램 만들기  
 SharePoint 중앙 관리 또는 PowerShell 스크립트를 사용하여 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션을 만들 수 있습니다. SharePoint 중앙 관리를 사용 하는 방법에 대 한 자세한 내용은 sharepoint [2010에 대 한 Reporting Services Sharepoint 모드 설치](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)에서 "Reporting Services 서비스 응용 프로그램 만들기" 섹션을 참조 하세요. 서비스 애플리케이션을 만들기 위한 예제 PowerShell 스크립트는 이 항목의 뒷부분에 나오는 PowerShell 섹션을 참조하세요.  
  
##  <a name="bkmk_associations"></a>프록시 그룹과 서비스 응용 프로그램의 연결 수정  
 서비스 애플리케이션을 만들기 위한 새 페이지에는 **웹 애플리케이션 연결**섹션이 있습니다. 이 섹션에서 만들어지는 서비스 애플리케이션에 연결할 수 있습니다. 다음 단계를 사용하여 연결을 변경하고 사용자 구성을 서비스 애플리케이션에 할당합니다. 사용자 지정 그룹에 대한 서비스 애플리케이션의 연결을 변경하지 않고 동일한 일반 프로세스를 사용하여 기본 그룹에 프록시를 추가할 수도 있습니다.  
  
1.  SharePoint 중앙 관리의 애플리케이션 관리에서 **서비스 애플리케이션 연결 구성**을 클릭합니다.  
  
2.  서비스 애플리케이션 연결 페이지에서 보기를 **서비스 애플리케이션**으로 변경합니다.  
  
3.  새 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 서비스 애플리케이션의 이름을 찾아서 클릭합니다. 또한 애플리케이션 프록시 그룹 이름인 **기본값** 을 클릭하여 다음 단계를 완료하는 대신 기본 그룹에 프록시를 추가할 수도 있습니다.  
  
4.  
  **다음 연결 그룹 편집** 선택 상자에서 **사용자 지정**을 선택합니다.  
  
5.  해당 프록시의 상자를 선택하고 **확인**클릭합니다.  
  
##  <a name="bkmk_editserviceapplication"></a>서비스 응용 프로그램 속성 편집  
 서비스 애플리케이션의 속성 페이지를 다시 열어서 속성을 수정할 수 있습니다.  
  
1.  SharePoint 중앙 관리의 응용 프로그램 관리 그룹에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  전체 행을 선택하려면 유형 열을 클릭하여 서비스 애플리케이션을 선택합니다. 애플리케이션 이름을 클릭하면 서비스 애플리케이션의 속성을 여는 대신 서비스에 대한 관리 옵션 페이지가 열립니다.  
  
3.  서비스 애플리케이션 리본에서 **속성**을 클릭합니다.  
  
##  <a name="bkmk_powershell_create_ssrs_serviceapp"></a>PowerShell을 사용 하 여 Reporting Services 서비스 응용 프로그램을 만들려면  
 PowerShell을 사용하여 서비스 애플리케이션과 프록시를 만들 수 있습니다. 아래 예제에서는 서비스 애플리케이션에서 사용하도록 구성할 애플리케이션 풀을 알고 있다고 가정합니다.  
  
1.  애플리케이션 풀 이름의 애플리케이션 풀 개체를 새 동작으로 전달되는 변수에 추가합니다.  
  
    ```powershell
    $appPoolName = Get-SPServiceApplicationPool "<application pool name>"  
    ```  
  
2.  제공한 이름 및 애플리케이션 풀 이름을 사용하여 서비스 애플리케이션을 만듭니다.  
  
    ```powershell
    New-SPRSServiceApplication -Name 'MyServiceApplication' -ApplicationPool $appPoolName -DatabaseName 'MyServiceApplicationDatabase' -DatabaseServer '<Server Name>'  
    ```  
  
3.  새 서비스 애플리케이션 개체를 가져오고 개체를 새 프록시 파이프 지정 cmdlet으로 파이프합니다.  
  
    ```powershell
    Get-SPRSServiceApplication -name MyServiceApplication | New-SPRSServiceApplicationProxy "MyServiceApplicationProxy"  
    ```  
  
##  <a name="bkmk_related"></a> 관련 작업  
  
|Task|링크|  
|----------|----------|  
|서비스 애플리케이션의 설정 관리|[Reporting Services SharePoint 서비스 응용 프로그램 관리](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)|  
|서비스 애플리케이션과 관련 구성 요소(예: 암호화 키 및 프록시) 백업 및 복원|[Reporting Services SharePoint 서비스 애플리케이션 백업 및 복원](../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  
