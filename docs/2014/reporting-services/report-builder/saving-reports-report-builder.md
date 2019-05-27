---
title: 보고서 저장(보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e21b1c9e48dcccf8b72a60fbd381aac3d878c0dc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107626"
---
# <a name="saving-reports-report-builder"></a>보고서 저장(보고서 작성기)
  보고서 작성기에서 보고서 서버, SharePoint 라이브러리, 쓰기 권한이 있는 파일 공유 또는 컴퓨터에 보고서를 저장할 수 있습니다. 보고서를 연 동일한 위치에 보고서를 저장하거나, 다른 위치에 보고서를 저장하거나, 동일한 위치나 다른 위치에 새 이름으로 보고서를 저장할 수 있습니다. 기본적으로 보고서는 보고서를 연 위치에 다시 저장됩니다. 보고서를 저장할 때 실제로 저장하는 것은 보고서 레이아웃을 설명하는 보고서 정의이며, 데이터를 저장하지는 않습니다. 보고서를 실행할 때마다 보고서 데이터는 새로 고쳐지고 보고서를 이전에 실행했을 때와 다를 수 있습니다.  
  
 보고서를 다른 형식으로 저장하거나 데이터와 함께 보고서 정의를 저장하려면 다음 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기능 중 하나를 사용합니다.  
  
-   렌더링된 보고서를 CSV(쉼표로 구분된 파일), Excel 통합 문서 등의 다른 파일 형식으로 내보내고 해당 형식으로 보고서를 저장합니다. 보고서에서 데이터 피드를 생성하고 보고서 데이터를 저장할 수도 있습니다.  
  
-   보고서 구독을 만들어 파일 공유에 보고서를 배달하고 저장합니다.  
  
-   보고서 기록을 사용하여 렌더링된 보고서의 버전을 기록 복사본으로 저장합니다.  
  
 보고서 서버에서 보고서를 직접 보고 관리하는 방법에 대한 자세한 내용은 msdn.microsoft.com의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](https://go.microsoft.com/fwlink/?LinkId=154888)에서 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md) 및 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../report-server/reporting-services-report-server-native-mode.md)를 참조하세요.  
  
##  <a name="SavingReportDefinitions"></a> 보고서 정의 저장 하는 중  
 컴퓨터에 보고서를 저장할 수 있지만 보고서 서버에 보고서를 저장하면 많은 이점이 있습니다.  
  
 보고서 서버에 보고서를 저장하면 다음과 같은 이점이 있습니다.  
  
-   보고서를 저장한 폴더에 액세스할 수 있는 권한이 있는 다른 사용자가 보고서를 사용할 수 있습니다.  
  
-   보고서 관리자에서 보고서를 관리하고 볼 수 있습니다.  
  
-   데이터 원본, 이미지 및 하위 보고서와 같은 보고서 리소스가 쉽게 액세스할 수 있도록 한 곳에 저장됩니다.  
  
-   구독을 통해 다른 사용자에게 보고서를 배달할 수 있습니다.  
  
-   보고서가 보고서 서버 데이터베이스에 안전하게 저장됩니다.  
  
-   보고서 실행이 기록되어 성능 및 감사 정보를 제공할 수 있습니다.  
  
 보고서 서버에 보고서를 저장하는 것을 보고서 게시라고도 합니다. 보고서를 저장할 때 보고서 정의만 저장하게 됩니다. 보고서를 실행할 때마다 보고서 데이터는 새로 고쳐지고 보고서를 이전에 실행했을 때와 다를 수 있습니다. 데이터와 함께 보고서 정의를 저장하려면 보고서 기록 기능을 사용해야 합니다. 이 기능을 사용하여 데이터와 함께 보고서의 복사본을 저장할 수 있습니다.  
  

  
##  <a name="ExportingAndSavingReports"></a> 보고서 내보내기 및 저장  
 보관할 보고서가 적으면 보고서를 파일로 내보내고 저장하는 것이 좋습니다. PDF나 Excel 등의 애플리케이션으로 보고서를 내보내면 보고서를 파일로 저장하여 네트워크의 보호된 공유 디렉터리에 보관할 수 있습니다. 또는 보고서의 모든 복사본을 형식에 관계없이 보고서 서버 데이터베이스에 보관하려는 경우 저장된 PDF나 Excel 파일을 리소스 항목으로 업로드할 수 있습니다. 보고서를 내보내는 방법에 대 한 자세한 내용은 참조 하세요. [보고서 내보내기 &#40;보고서 작성기 및 SSRS&#41; ](export-reports-report-builder-and-ssrs.md) 하 고 [파일 또는 보고서 업로드 &#40;보고서 관리자&#41;](../reports/upload-a-file-or-report-report-manager.md).  
  

  
##  <a name="UsingFileShareDelivery"></a> 파일 공유 배달 사용  
 보관할 보고서가 많으면 보고서를 파일 시스템으로 직접 배달하는 구독을 만듭니다. 이 방식을 사용하려면 각 보고서에 대한 구독을 만들고 보고서를 저장할 공유 폴더를 선택하고 파일 작성 시간을 결정하는 일정을 정의해야 합니다. 구독을 정의하면 보고서 서버는 무인 모드에서 보고서를 실행하고 제공한 일정에 따라 보고서 파일을 보관 위치에 추가할 수 있습니다. 또한 일회 일정을 만들어 필요한 경우에만 보고서를 보관할 수 있습니다. 구독 및 파일 공유 배달에 대한 자세한 내용은 SQL Server 온라인 설명서의 [Reporting Services 설명서](https://go.microsoft.com/fwlink/?linkid=121312) 에 있는 "Reporting Services의 파일 배달"을 참조하십시오.  
  

  
##  <a name="UsingReportHistory"></a> 보고서 기록 사용  
 보고서 기록 기능을 사용하여 기록 복사본을 만들 수도 있습니다. 그런 다음 나중에 사용할 수 있도록 보고서 서버 데이터베이스를 백업하고 안전한 위치에 백업을 저장할 수 있습니다. 모든 보고서 기록은 보고서, 공유 데이터 원본 항목, 폴더, 구독 및 공유 일정과 함께 보고서 서버 데이터베이스에 저장됩니다. 백업을 만들어 보고서 기록의 영구 복사본과 보고서를 받는 사람을 나타내는 구독 정보 등의 메타데이터를 유지 관리할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서의 [Reporting Services 설명서](https://go.microsoft.com/fwlink/?linkid=121312) 에 있는 "보고서 기록 관리"를 참조하십시오.  
  

  
##  <a name="HowTo"></a> 방법 도움말 항목  
  
-   [보고서 서버에 보고서 저장&#40;보고서 작성기&#41;](save-reports-to-a-report-server-report-builder.md)  
  
-   [SharePoint 라이브러리에 보고서 저장&#40;보고서 작성기&#41;](save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [컴퓨터에 보고서 저장 &#40;보고서 작성기&#41;](../save-reports-to-your-computer-report-builder.md)  
  

  
## <a name="see-also"></a>관련 항목  
 [보고서, 보고서 파트 및 보고서 정의&#40;보고서 작성기 및 SSRS&#41;](../report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [설치, 제거 및 보고서 작성기 지원](../install-uninstall-and-report-builder-support.md)   
 [보고서 찾기, 보기 및 관리&#40;보고서 작성기 및 SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [보고서를 내보내는 &#40;보고서 작성기 및 SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](print-reports-report-builder-and-ssrs.md)  
  
  
