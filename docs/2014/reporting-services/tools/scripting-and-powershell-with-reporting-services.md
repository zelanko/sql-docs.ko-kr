---
title: Reporting Services를 사용한 스크립팅 및 PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services]
- Reporting Services, scripting
- scripting [Reporting Services]
ms.assetid: 1ac2646d-ed5a-4436-b18f-2150c33f3d87
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7ea45b2b785666253405c579930d1f89417d4c58
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024524"
---
# <a name="scripting-and-powershell-with-reporting-services"></a>Reporting Services를 사용한 스크립팅 및 PowerShell
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 는 rs.exe 명령줄 유틸리티, SharePoint 모드 보고서 서버용 PowerShell cmdlet을 비롯한 스크립트를 통해 기본 모드 및 SharePoint 모드에서 PowerShell의 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 개체 모델을 활용하여 다양한 개발 및 관리 시나리오를 지원합니다.  
  
-   관리자는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 에서 스크립트를 작성하여 보고서 서버 설치를 배포 및 관리하는 방법을 자동화하며 보고서 서버 데이터베이스를 생성, 구성 및 업데이트하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 생성하고 실행할 수 있습니다. 또한 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 의 기록 및 재생 스크립트 기능을 사용하여 일상적인 유지 관리 태스크를 자동화할 수 있습니다.  
  
-   개발자는 스크립트를 포함하는 사용자 지정 애플리케이션을 만들 수 있습니다. 보고서 서버 웹 서비스를 호출하는 스크립트를 실행할 수 있습니다. 관리 코드로 작성할 수 있는 거의 모든 작업을 스크립트로도 작성할 수 있습니다.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET 스크립트를 보고서 서버에서 실행되는 스크립트 호스트인 RS.exe 유틸리티에서 처리할 수 있는 스크립트 언어로 지원합니다.  
  
## <a name="reporting-services-sharepoint-mode-powershell-cmdlets-and-samples"></a>Reporting Services SharePoint 모드 PowerShell cmdlet 및 샘플  
 ![PowerShell 관련 콘텐츠](../media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠")  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 모드에는 보고서 서버 관리를 위한 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] cmdlet이 포함되어 있습니다.  
  
-   [PowerShell cmdlets for Reporting Services SharePoint Mode](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md) 에서는 다음 예를 제공합니다.  
  
    -   서비스 애플리케이션 및 프록시 만들기  
  
    -   배달 확장 검토 및 업데이트  
  
    -   보고 서비스 애플리케이션 데이터베이스의 속성 가져오기 및 설정(예: 데이터베이스 시간 제한)  
  
    -   데이터 확장 나열  
  
## <a name="reporting-services-object-model-and-powershell-samples"></a>Reporting Services 개체 모델 및 Powershell 샘플  
 ![PowerShell 관련 콘텐츠](../media/rs-powershellicon.jpg "PowerShell 관련 콘텐츠")  
  
 대부분 SharePoint 및 기본 모드에 유효하며 핵심 개체 모델을 호출하는 PowerShell(예: 마이그레이션 작업, 구독 작업)과 관련 샘플은 SQL15에서 작동합니다.  
  
-   [PowerShell을 사용하여 Reporting Services 구독 소유자 변경, 나열 및 구독 실행](../subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
-   [PowerShell을 사용하여 기본 모드 보고서 서버로 Azure VM 만들기](https://msdn.microsoft.com/library/azure/dn449661.aspx)  
  
-   [Reporting Services WMI 공급자 액세스](access-the-reporting-services-wmi-provider.md)에서 "PowerShell을 사용하여 WMI 클래스 액세스" 섹션을 참조하세요.  
  
-   [PowerShell을 사용하여 SSRS를 관리하는 방법](http://curah.microsoft.com/13107/how-to-administer-ssrs-using-powershell).scriptin  
  
## <a name="rsexe-scripting-samples"></a>RS.exe 스크립팅 샘플  
  
-   [보고서 서버 간 콘텐츠 마이그레이션을 위한 예제 Reporting Services rs.exe](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md)  
  
-   추가 스크립트, 애플리케이션 및 확장 예에 대해서는 [SQL Server Reporting Services 제품 샘플](https://go.microsoft.com/fwlink/?LinkId=177889)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [RS.exe 유틸리티&#40;SSRS&#41;](rs-exe-utility-ssrs.md)   
 [배포 및 관리 태스크 스크립팅](script-deployment-and-administrative-tasks.md)   
 [rs.exe 유틸리티 및 웹 서비스를 사용한 스크립트](script-with-the-rs-exe-utility-and-the-web-service.md)  
  
  
