---
title: 보고서 저장(보고서 작성기) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8682d55f6c805066f5b596e79a074f253db9faa9
ms.sourcegitcommit: 1800fc15075bb17b50d0c18b089d8a64d87ae726
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66499628"
---
# <a name="saving-reports-report-builder"></a>보고서 저장(보고서 작성기)
  보고서 작성기에서 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 서버, SharePoint 라이브러리, 쓰기 권한이 있는 파일 공유 또는 컴퓨터에 페이지를 매긴 보고서를 저장할 수 있습니다. 
  
보고서를 저장할 때 실제로 저장하는 것은 보고서 레이아웃을 설명하는 보고서 정의이며, 데이터를 저장하지는 않습니다. 보고서를 실행할 때마다 보고서 데이터는 새로 고쳐지고 보고서를 이전에 실행했을 때와 다를 수 있습니다.  
  
 보고서를 다른 형식으로 저장하거나 데이터와 함께 보고서 정의를 저장하려면 다음 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능 중 하나를 사용합니다.  
  
-   렌더링된 보고서를 CSV(쉼표로 구분된 파일), Excel 통합 문서 등의 다른 파일 형식으로 내보내고 해당 형식으로 보고서를 저장합니다. 보고서에서 데이터 피드를 생성하고 보고서 데이터를 저장할 수도 있습니다.  
  
-   보고서 구독을 만들어 파일 공유에 보고서를 배달하고 저장합니다.  
  
-   보고서 기록을 사용하여 렌더링된 보고서의 버전을 기록 복사본으로 저장합니다.  
  
 보고서 서버에서 보고서를 직접 보고 관리하는 방법에 대한 자세한 내용은 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) 및 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)를 참조하세요.  
  
##  <a name="SavingReportDefinitions"></a> 보고서 서버에 보고서 저장  
  보고서 서버에 보고서를 저장하는 것을 보고서 게시라고도 합니다. 컴퓨터에 보고서를 저장할 수 있지만 보고서 서버에 보고서를 저장하면 많은 이점이 있습니다.  
  
-   보고서를 저장한 폴더에 액세스할 수 있는 권한이 있는 다른 사용자가 보고서를 사용할 수 있습니다.  
  
-   보고서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 웹 포털에서 관리하여 볼 수 있습니다.  
  
-   데이터 원본, 이미지 및 하위 보고서와 같은 보고서 리소스가 쉽게 액세스할 수 있도록 한 곳에 저장됩니다.  
  
-   구독을 통해 다른 사용자에게 보고서를 배달할 수 있습니다.  
  
-   보고서가 보고서 서버 데이터베이스에 안전하게 저장됩니다.  
  
-   보고서 실행이 기록되어 성능 및 감사 정보를 제공할 수 있습니다.  
  
##  <a name="ExportingAndSavingReports"></a> 보고서 내보내기 및 저장  
 보관할 보고서가 적으면 보고서를 파일로 내보내고 저장하는 것이 좋습니다. PDF나 Excel 등의 애플리케이션으로 보고서를 내보내면 보고서를 파일로 저장하여 네트워크의 보호된 공유 디렉터리에 보관할 수 있습니다. 또는 보고서의 모든 복사본을 형식에 관계없이 보고서 서버 데이터베이스에 보관하려는 경우 저장된 PDF나 Excel 파일을 리소스 항목으로 업로드할 수 있습니다. 보고서를 내보내는 방법에 대한 자세한 내용은 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) 및 [파일 또는 보고서 업로드](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)를 참조하세요.  
  
##  <a name="UsingFileShareDelivery"></a> 파일 공유 배달 사용  
 보관할 보고서가 많으면 보고서를 파일 시스템으로 직접 배달하는 구독을 만듭니다. 이 방식을 사용하려면 각 보고서에 대한 구독을 만들고 보고서를 저장할 공유 폴더를 선택하고 파일 작성 시간을 결정하는 일정을 정의해야 합니다. 구독을 정의하면 보고서 서버는 무인 모드에서 보고서를 실행하고 제공한 일정에 따라 보고서 파일을 보관 위치에 추가할 수 있습니다. 또한 일회 일정을 만들어 필요한 경우에만 보고서를 보관할 수 있습니다. 구독 및 파일 공유 배달에 대한 자세한 내용은 [Reporting Services의 파일 공유 배달](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)을 참조하세요.  
  
##  <a name="UsingReportHistory"></a> 보고서 기록 사용  
 보고서 기록 기능을 사용하여 기록 복사본을 만들 수도 있습니다. 그런 다음 나중에 사용할 수 있도록 보고서 서버 데이터베이스를 백업하고 안전한 위치에 백업을 저장할 수 있습니다. 모든 보고서 기록은 보고서, 공유 데이터 원본 항목, 폴더, 구독 및 공유 일정과 함께 보고서 서버 데이터베이스에 저장됩니다. 백업을 만들어 보고서 기록의 영구 복사본과 보고서를 받는 사람을 나타내는 구독 정보 등의 메타데이터를 유지 관리할 수 있습니다. 자세한 내용은 [보고서 기록에서 스냅숏 만들기, 수정 및 삭제](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md)를 참조하세요.  
 
##  <a name="HowTo"></a> 방법 도움말 항목  
  
-   [보고서 서버에 보고서 저장&#40;보고서 작성기&#41;](../../reporting-services/report-builder/save-reports-to-a-report-server-report-builder.md)  
  
-   [SharePoint 라이브러리에 보고서 저장&#40;보고서 작성기&#41;](../../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
   
## <a name="see-also"></a>참고 항목  
 [보고서, 보고서 파트 및 보고서 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Install Report Builder](../install-windows/install-report-builder.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)  
  
  
