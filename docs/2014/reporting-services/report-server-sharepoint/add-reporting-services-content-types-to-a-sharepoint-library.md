---
title: 웹 페이지 (SharePoint 통합된 모드의 Reporting Services)에 보고서 뷰어 웹 파트 추가 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: cac75345-2380-467d-a394-0a2140908a5a
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c351c37c9666c3b0f5723fa8ea049efe788e6a02
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172054"
---
# <a name="add-the-report-viewer-web-part-to-a-web-page-reporting-services-in-sharepoint-integrated-mode"></a>웹 페이지에 보고서 뷰어 웹 파트 추가(SharePoint 통합 모드의 Reporting Services)
  보고서 뷰어 웹 파트를 사용하여 SharePoint 통합 모드로 구성된 보고서 서버에서 실행되는 보고서를 볼 수 있습니다. 또한 이 웹 파트를 사용하여 보고서 작성기나 보고서 디자이너에서 만들어 라이브러리에 업로드한 보고서 정의 파일(.rdl)을 표시할 수 있습니다.  
  
 웹 페이지에 보고서를 포함하려는 경우 보고서 뷰어 웹 파트를 해당 페이지에 추가할 수 있습니다.  
  
> [!NOTE]  
>  이름은 같지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 통해 설치된 보고서 뷰어 웹 파트는 RSWebParts.cab 파일에 포함된 보고서 뷰어 웹 파트와 다릅니다. 이 항목의 지침은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 추가 기능을 통해 설치되는 보고서 뷰어 웹 파트에만 해당됩니다.  
  
 웹 페이지에 웹 파트를 추가하려면 사이트 수준에서 페이지 추가 및 사용자 지정 권한이 있어야 합니다. 기본 보안 설정을 사용하는 경우 이 권한은 모든 권한 수준의 사용 권한이 있는 **소유자** 그룹의 멤버에게 부여됩니다.  
  
### <a name="to-embed-a-report-in-a-web-page"></a>웹 페이지에 보고서를 포함하려면  
  
1.  웹 파트 페이지 또는 대시보드를 열거나 만듭니다.  
  
2.  **사이트 동작**에서 **페이지 편집**을 클릭합니다.  
  
3.  **웹 파트 추가**를 클릭합니다.  
  
4.  웹 파트 범주 목록에서 **기타** 범주를 선택한 다음 **SQL Server Reporting Services 보고서 뷰어**를 선택합니다.  
  
5.  **추가**를 클릭합니다. 영역의 맨 위에 웹 파트가 추가됩니다. 해당 웹 파트를 영역의 다른 위치로 끌어 놓을 수도 있습니다.  
  
6.  뷰어에서 **도구 창을 열려면 여기를 클릭하십시오**를 클릭합니다.  
  
7.  찾아보기 (**...**) 단추를 클릭하여 현재 사이트 모음의 임의 라이브러리에 있는 보고서를 선택합니다. 보고서 URL을 입력할 수도 있습니다. 보고서의 URL을 확인하려면 해당 보고서를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 보고서 옆의 아래쪽 화살표는 클릭하지 마십시오. 보고서 URL은 항목의 속성 보기 페이지에 표시되지 않습니다. **속성** 대화 상자에서 URL을 복사하여 붙여넣는 경우 "%20" URL 인코딩을 공백으로 바꿉니다. 예를 들어 "Company%20Sales"는 "Company Sales"가 되어야 합니다.  
  
    > [!NOTE]  
    >  각 보고서 뷰어 웹 파트에는 단일 보고서가 포함되어 있습니다. URL은 동일한 웹 응용 프로그램 또는 팜 내의 사이트나 현재 SharePoint 사이트에 있는 보고서에 대한 정규화된 경로여야 합니다. URL은 문서 라이브러리나 보고서가 포함된 문서 라이브러리 내의 폴더로 확인되어야 합니다. 보고서 URL은 .rdl 파일 확장명을 포함해야 합니다. 보고서가 모델 또는 공유 데이터 원본 파일에 종속되어 있는 경우 URL에 이러한 파일을 지정할 필요가 없습니다. 보고서에 필요한 파일에 대한 참조가 포함되어 있습니다.  
  
8.  도구 창이 열려 있는 동안 속성을 설정하여 기본 모양과 레이아웃을 수정할 수 있습니다.  
  
9. 도구 창의 아래쪽에서 **적용** 을 클릭한 다음 **확인** 을 클릭하여 창을 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 사이트의 보고서 뷰어 웹 파트](../report-viewer-web-part-on-a-sharepoint-site.md)   
 [보고서 뷰어 웹 파트를 사용자 지정](../customize-the-report-viewer-web-part.md)   
 [SharePoint 사이트의 보고서 서버 항목에 대 한 권한 부여](../security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [설치 또는 제거는 Reporting Services 추가-SharePoint 용 &#40;SharePoint 2010 및 SharePoint 2013&#41;](../install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
