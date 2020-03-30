---
title: 웹 페이지에 보고서 뷰어 웹 파트 추가 | Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 562c762871db5c29476d10a81ac52dad46f65ad5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65579395"
---
# <a name="add-the-report-viewer-web-part-to-a-web-page"></a>웹 페이지에 보고서 뷰어 웹 파트 추가

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

보고서 뷰어 웹 파트를 사용하여 SharePoint 통합 모드로 구성된 보고서 서버에서 실행되는 보고서를 볼 수 있습니다. 또한 이 웹 파트를 사용하여 보고서 작성기나 보고서 디자이너에서 만들어 라이브러리에 업로드한 보고서 정의 파일(.rdl)을 표시할 수 있습니다.

웹 페이지에 보고서를 포함하려는 경우 보고서 뷰어 웹 파트를 해당 페이지에 추가할 수 있습니다.

> [!NOTE]
> 이 문서는 SharePoint 제품용 Reporting Services 추가 기능과 함께 제공되는 보고서 뷰어 웹 파트에 관련된 것입니다. SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

웹 페이지에 웹 파트를 추가하려면 사이트 수준에서 페이지 추가 및 사용자 지정 권한이 있어야 합니다. 기본 보안 설정을 사용하는 경우 이 권한은 모든 권한 수준의 사용 권한이 있는 **소유자** 그룹의 멤버에게 부여됩니다.

## <a name="to-embed-a-report-in-a-web-page"></a>웹 페이지에 보고서를 포함하려면

1.  웹 파트 페이지 또는 대시보드를 열거나 만듭니다.  
  
2.  **사이트 동작**에서 **페이지 편집**을 클릭합니다.  
  
3.  **웹 파트 추가**를 클릭합니다.  
  
4.  웹 파트 범주 목록에서 **기타** 범주를 선택한 다음 **SQL Server Reporting Services 보고서 뷰어**를 선택합니다.  
  
5.  **추가**를 클릭합니다. 영역의 맨 위에 웹 파트가 추가됩니다. 해당 웹 파트를 영역의 다른 위치로 끌어 놓을 수도 있습니다.  
  
6.  뷰어에서 **도구 창을 열려면 여기를 클릭하십시오**를 클릭합니다.  
  
7.  찾아보기 ( **...** ) 단추를 클릭하여 현재 사이트 모음의 임의 라이브러리에 있는 보고서를 선택합니다. 보고서 URL을 입력할 수도 있습니다. 보고서의 URL을 확인하려면 해당 보고서를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 보고서 옆의 아래쪽 화살표는 클릭하지 마십시오. 보고서 URL은 항목의 속성 보기 페이지에 표시되지 않습니다. **속성** 대화 상자에서 URL을 복사하여 붙여넣는 경우 "%20" URL 인코딩을 공백으로 바꿉니다. 예를 들어 "Company%20Sales"는 "Company Sales"가 되어야 합니다.  
  
    > [!NOTE]  
    >  각 보고서 뷰어 웹 파트에는 단일 보고서가 포함되어 있습니다. URL은 동일한 웹 애플리케이션 또는 팜 내의 사이트나 현재 SharePoint 사이트에 있는 보고서에 대한 정규화된 경로여야 합니다. URL은 문서 라이브러리나 보고서가 포함된 문서 라이브러리 내의 폴더로 확인되어야 합니다. 보고서 URL은 .rdl 파일 확장명을 포함해야 합니다. 보고서가 모델 또는 공유 데이터 원본 파일에 종속되어 있는 경우 URL에 이러한 파일을 지정할 필요가 없습니다. 보고서에 필요한 파일에 대한 참조가 포함되어 있습니다.  
  
8.  도구 창이 열려 있는 동안 속성을 설정하여 기본 모양과 레이아웃을 수정할 수 있습니다.  
  
9. 도구 창의 아래쪽에서 **적용** 을 클릭한 다음 **확인** 을 클릭하여 창을 닫습니다.  
  
## <a name="see-also"></a>참고 항목

 [SharePoint 사이트의 보고서 뷰어 웹 파트](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [보고서 뷰어 웹 파트 사용자 지정](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)   
 [SharePoint 사이트의 보고서 서버 항목에 대한 사용 권한 부여](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [SharePoint용 Reporting Services 추가 기능 설치 또는 제거](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
