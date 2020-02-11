---
title: SharePoint 라이브러리에 보고서 게시 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], reports in SharePoint integrated mode
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1cc957af5596acbf2478d55645b1386283970e33
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102527"
---
# <a name="publish-a-report-to-a-sharepoint-library"></a>SharePoint 라이브러리에 보고서 게시
  SharePoint 통합용으로 구성된 SharePoint 사이트에 보고서를 게시하려면 보고서 디자이너에서 프로젝트 속성을 설정해야 합니다. 프로젝트 속성에서 서버, 보고서 및 공유 데이터 원본에 대한 모든 참조는 정규화된 URL이어야 합니다. 보고서 정의에서 하위 보고서, 드릴스루 보고서 및 리소스(예: 웹 기반 이미지)에 대한 모든 참조는 정규화된 URL이어야 합니다.  
  
 프로젝트의 속성을 설정하려면 SharePoint 사이트에 대한 **멤버** 또는 **소유자** 권한이 있어야 합니다. 자세한 내용은 [SharePoint 모드의 보고서 서버에 게시된 보고서 항목에 대한 URL 예&#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)를 참조하세요.  
  
### <a name="to-publish-a-report-to-a-sharepoint-site"></a>보고서를 SharePoint 사이트에 게시하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 기존 또는 새로운 보고서 서버 프로젝트를 엽니다.  
  
2.  **프로젝트** 메뉴에서 **속성**을 클릭합니다. _\<프로젝트>_ **속성 페이지** 대화 상자가 열립니다.  
  
3.  **구성** 목록에서 보고서를 작성 및 게시하는 데 사용할 솔루션 빌드 구성의 이름을 선택합니다. 현재 구성은 **활성**( *\<configuration>* )으로 나열됩니다.  
  
4.  프로젝트의 공유 데이터 원본을 게시하고 이전에 게시된 공유 데이터 원본을 덮어쓰려면 **OverwriteDataSources** 를 **True**로 설정합니다.  
  
5.  필드 **Targetdatasourcefolder**에 SharePoint 라이브러리 또는 라이브러리 폴더에 대 한 URL을 입력 *http://TestServer/TestSite/Documents/DataSources)* 합니다 (예:).  
  
     값을 지정하지 않으면 **TargetReportFolder** 값이 사용됩니다.  
  
6.  **Targetreportfolder**에 라이브러리 또는 라이브러리 폴더에 대 한 URL을 입력 *http://TestServer/TestSite/Documents/Reports)* 합니다 (예:).  
  
7.  **TargetServerURL**에 SharePoint 최상위 사이트 또는 하위 사이트에 대한 URL을 입력합니다. 사이트를 지정 하지 않으면 기본 최상위 사이트 (예: *http://servername*, *http://servername/site*또는 *http://servername/site/subsite*)가 사용 됩니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. 솔루션 탐색기에서 게시하려는 보고서를 마우스 오른쪽 단추로 클릭하고 **배포**를 클릭합니다. 보고서가 **TargetReportFolder**에 지정된 위치에 게시됩니다. 출력 창에 배포 오류가 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로젝트 속성 페이지 대화 상자](../tools/project-property-pages-dialog-box.md)   
 [배포 속성 설정&#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)   
 [보고서 서버에 보고서 게시](publishing-reports-to-a-report-server.md)   
 [SharePoint 모드의 보고서 서버에 게시된 보고서 항목에 대한 URL 예&#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [보고서에 Office 데이터 연결&#40;.odc&#41; 사용&#40;SharePoint 통합 모드의 Reporting Services&#41;](../report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
