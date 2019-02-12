---
title: 기본 모드에서 SharePoint 모드로 마이그레이션(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c5b15bec-6fde-4174-bcde-d043307244dd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5aa1492942e76011eac784bbea90e41b7a3a2484
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011174"
---
# <a name="native-to-sharepoint-migration-ssrs"></a>기본 모드에서 SharePoint 모드로의 마이그레이션(SSRS)
  한 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서버 모드에서 다른 서버 모드로 업그레이드하거나 변환할 수 없습니다. 예를 들어 기본 모드 보고서 서버를 SharePoint 모드로 업그레이드하거나 변환할 수 없습니다. 사용되는 데이터베이스 스키마가 다르기 때문에 모드 간에 보고서 서버 데이터베이스를 복사할 수 없습니다. 한 보고서 서버에서 다른 보고서 서버로 콘텐츠를 마이그레이션할 수 있습니다. 사용하는 도구는 원본 서버 및 대상 서버에 맞게 구성된 보고서 서버 모드의 유형에 따라 달라집니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Native mode | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint mode  
  
##  <a name="bkmk_native_to_sharepoint"></a> Reporting Services 마이그레이션 도구  
 이 도구는 기본 모드 배포에서 SharePoint 모드 배포로의 콘텐츠 마이그레이션을 지원합니다. 이 도구는 SharePoint 모드에서 SharePoint 모드로 또는 SharePoint 모드에서 기본 모드로의 마이그레이션을 지원하지 않습니다.  
  
 자세한 내용은 [Reporting Services 마이그레이션 도구](https://www.microsoft.com/download/details.aspx?id=29560)(https://www.microsoft.com/download/details.aspx?id=29560)를 참조하세요.  
  
## <a name="use-script-to-migrate-content"></a>스크립트를 사용하여 콘텐츠 마이그레이션  
 마이그레이션 도구가 사용자 요구에 맞지 않는 경우 수동으로 보고서 서버 데이터를 마이그레이션할 수 있습니다. 다음은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 배포 간에 보고서 항목을 마이그레이션하는 데 필요한 단계를 요약한 내용입니다. 이 방법은 기본 또는 SharePoint 모드를 원본 또는 대상 서버로 지원하지 않습니다.  
  
1.  암호화 키 백업 및 복원. 데이터를 암호화하는 데 사용되는 키입니다. 암호화 키는 암호(예: 데이터 원본 연결을 위해 저장된 암호)를 암호화하는 데도 사용됩니다. 그러나 암호는 마이그레이션할 수 없으며 대화 환경에서 암호를 다시 입력해야 합니다.  
  
2.  **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] RSS 스크립트:** 보고서 서버 웹 서비스 SOAP 메서드를 호출하여 데이터베이스 간에 데이터를 복사하는 Visual Basic 스크립트를 작성합니다. **RS.exe** 유틸리티를 사용하여 이 스크립트를 실행합니다. Rs.exe는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]와 함께 설치됩니다.  
  
    -   [보고서 서버 간 콘텐츠 마이그레이션을 위한 예제 Reporting Services rs.exe](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md) 이 항목에서는 CodePlex에서 다운로드할 수 있는 예제 스크립트를 사용하는 방법에 대해 설명합니다.  
  
    -   CodePlex의 예제 rss 스크립트, [한 보고서 서버에서 다른 보고서 서버로 콘텐츠를 마이그레이션하는 Reporting Services RS.exe 스크립트](http://azuresql.codeplex.com/releases/view/115207)  
  
    -   [Reporting Services를 사용한 스크립팅 및 PowerShell](../tools/scripting-and-powershell-with-reporting-services.md)  
  
 다음 표에는 스크립트를 사용하여 마이그레이션할 수 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 개체가 요약되어 있습니다.  
  
|Object|스크립팅 가능|주석|  
|------------|---------------------|--------------|  
|보고서|사용자 계정 컨트롤|마이그레이션 후 데이터 원본에 대한 암호를 다시 입력합니다.|  
|데이터 원본|사용자 계정 컨트롤|마이그레이션 후 보고서를 데이터 원본에 다시 연결 합니다.|  
|모델|사용자 계정 컨트롤||  
|데이터 세트|사용자 계정 컨트롤||  
|보고서 파트||마이그레이션 후 보고서 파트에 대한 경로를 확인하거나 업데이트합니다.|  
|일정|사용자 계정 컨트롤|ListSchedules 메서드 [Subscription and Delivery Methods](../report-server-web-service/methods/subscription-and-delivery-methods.md)를 참조하세요.|  
|구독|예|List Subscriptions 메서드를 참조 하세요 [Subscription and Delivery Methods](../report-server-web-service/methods/subscription-and-delivery-methods.md) 와 ChangeSubscriptionOwner 메서드 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>|  
|스냅숏|||  
||||  
  
  
