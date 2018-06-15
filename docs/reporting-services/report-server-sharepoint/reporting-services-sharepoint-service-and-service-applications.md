---
title: Reporting Services SharePoint Service 및 서비스 응용 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server-sharepoint
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d1db1758c979ae3582d562c47690e12af72171cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025140"
---
# <a name="reporting-services-sharepoint-service-and-service-applications"></a>Reporting Services SharePoint Service 및 서비스 응용 프로그램

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Reporting Services SharePoint 모드는 SharePoint 서비스 아키텍처에 맞게 구축되었으며 SharePoint 서비스와 일대다 서비스 응용 프로그램을 활용합니다. 서비스 응용 프로그램을 만들면 서비스를 사용할 수 있게 되며 서비스 응용 프로그램 데이터베이스가 생성됩니다. Reporting Services 서비스 응용 프로그램은 여러 개 만들 수 있지만 대부분의 배포 시나리오에서 서비스 응용 프로그램은 하나면 충분합니다.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.
  
## <a name="creating-a-reporting-services-service-application"></a>Reporting Services 서비스 응용 프로그램 만들기

 SharePoint 중앙 관리 또는 PowerShell 스크립트를 사용하여 Reporting Services 서비스 응용 프로그램을 만들 수 있습니다. SharePoint 중앙 관리를 사용하는 방법은 [SharePoint 2010용 Reporting Services SharePoint 모드 설치](http://msdn.microsoft.com/47efa72e-1735-4387-8485-f8994fb08c8c)에서 "Reporting Services 서비스 응용 프로그램 만들기" 섹션을 참조하세요. 서비스 응용 프로그램을 만들기 위한 예제 PowerShell 스크립트는 이 항목의 뒷부분에 나오는 PowerShell 섹션을 참조하세요.  
  
## <a name="modify-the-associations-of-the-service-application-with-a-proxy-group"></a>프록시 그룹과 서비스 응용 프로그램의 연결 수정

 서비스 응용 프로그램을 만들기 위한 새 페이지에는 **웹 응용 프로그램 연결**섹션이 있습니다. 이 섹션에서 만들어지는 서비스 응용 프로그램에 연결할 수 있습니다. 다음 단계를 사용하여 연결을 변경하고 사용자 구성을 서비스 응용 프로그램에 할당합니다. 사용자 지정 그룹에 대한 서비스 응용 프로그램의 연결을 변경하지 않고 동일한 일반 프로세스를 사용하여 기본 그룹에 프록시를 추가할 수도 있습니다.  
  
1.  SharePoint 중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 연결 구성**을 클릭합니다.  
  
2.  서비스 응용 프로그램 연결 페이지에서 보기를 **서비스 응용 프로그램**으로 변경합니다.  
  
3.  새 Reporting Services 서비스 응용 프로그램의 이름을 찾아서 클릭합니다. 또한 응용 프로그램 프록시 그룹 이름인 **기본값** 을 클릭하여 다음 단계를 완료하는 대신 기본 그룹에 프록시를 추가할 수도 있습니다.  
  
4.  **다음 연결 그룹 편집** 선택 상자에서 **사용자 지정**을 선택합니다.  
  
5.  해당 프록시의 상자를 선택하고 **확인**클릭합니다.  
  
## <a name="edit-service-application-properties"></a>서비스 응용 프로그램 속성 편집

 서비스 응용 프로그램의 속성 페이지를 다시 열어서 속성을 수정할 수 있습니다.  
  
1.  SharePoint 중앙 관리의 응용 프로그램 관리 그룹에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
2.  전체 행을 선택하려면 유형 열을 클릭하여 서비스 응용 프로그램을 선택합니다. 응용 프로그램 이름을 클릭하면 서비스 응용 프로그램의 속성을 여는 대신 서비스에 대한 관리 옵션 페이지가 열립니다.  
  
3.  서비스 응용 프로그램 리본에서 **속성**을 클릭합니다.  
  
## <a name="create-a-reporting-services-service-application-using-powershell"></a>PowerShell을 사용하여 Reporting Services 서비스 응용 프로그램 만들기

 PowerShell을 사용하여 서비스 응용 프로그램과 프록시를 만들 수 있습니다. 아래 예제에서는 서비스 응용 프로그램에서 사용하도록 구성할 응용 프로그램 풀을 알고 있다고 가정합니다.  
  
1.  응용 프로그램 풀 이름의 응용 프로그램 풀 개체를 새 동작으로 전달되는 변수에 추가합니다.  
  
    ```  
    $appPoolName = get-spserviceapplicationpool “<application pool name>”  
    ```  
  
2.  제공한 이름 및 응용 프로그램 풀 이름을 사용하여 서비스 응용 프로그램을 만듭니다.  
  
    ```  
    New-SPRSServiceApplication –Name ‘MyServiceApplication’ –ApplicationPool $appPoolName –DatabaseName ‘MyServiceApplicationDatabase’ –DatabaseServer ‘<Server Name>’  
    ```  
  
3.  새 서비스 응용 프로그램 개체를 가져오고 개체를 새 프록시 파이프 지정 cmdlet으로 파이프합니다.  
  
    ```  
    Get-SPRSServiceApplication –name MyServiceApplication | New-SPRSServiceApplicationProxy “MyServiceApplicationProxy”  
    ```  
  
## <a name="related-tasks"></a>관련 작업
  
|태스크|링크|  
|----------|----------|  
|서비스 응용 프로그램의 설정 관리|[Reporting Services SharePoint 서비스 응용 프로그램 관리](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)|  
|서비스 응용 프로그램과 관련 구성 요소(예: 암호화 키 및 프록시) 백업 및 복원|[Reporting Services SharePoint 서비스 응용 프로그램 백업 및 복원](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)|  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
