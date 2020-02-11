---
title: 필터 또는 문서 웹 파트 연결 (SharePoint 통합 모드의 Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Filter Web Part [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
- Documents Web Part [Reporting Services]
ms.assetid: 6a303135-c0ef-44cd-a423-1cea8df3dcf3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 062733f1ee68cd90ccc1b9a15d0cadc06b7e6f89
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109723"
---
# <a name="connect-filter-or-documents-web-part-reporting-services-in-sharepoint-integrated-mode"></a>필터 또는 문서 웹 파트 연결(SharePoint 통합 모드의 Reporting Services)
  SharePoint 제품을 사용하는 경우 필터 웹 파트 또는 문서 웹 파트와 보고서 뷰어 웹 파트가 포함된 대시보드나 웹 파트 페이지를 만들 수 있습니다. 선택한 버전은 [!INCLUDE[SPF2010](../includes/spf2010-md.md)] 또는 [!INCLUDE[SPS2010](../includes/sps2010-md.md)]입니다. 또한 지원되는 버전은 [!INCLUDE[winSPServ3](../includes/winspserv3-md.md)] 또는 [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007입니다. 필터 웹 파트를 연결하면 필터 웹 파트의 필터 값을 선택하여 같은 페이지의 매개 변수가 있는 보고서에 해당 값을 보낼 수 있습니다. 문서 웹 파트를 연결하면 문서 라이브러리의 보고서를 클릭하여 인접 보고서 뷰어 웹 파트의 보고서를 볼 수 있습니다.  
  
 필터 웹 파트는 보고서에 있는 하나 이상의 매개 변수에 값을 보내는 데 사용됩니다. 필터 웹 파트를 사용하려면 보고서에 웹 파트가 보낸 값, 데이터 형식 및 서식과 호환되는 매개 변수가 정의되어 있어야 합니다.  
  
 문서 웹 파트는 홈 사이트의 문서 라이브러리와 연결되어 있습니다. 문서 라이브러리에서 항목을 보거나, 추가하거나, 제거하려면 **모든 사이트 콘텐츠 보기**를 클릭합니다. 그런 다음 라이브러리에서 **문서**를 클릭합니다. 
  **새로 만들기**, **업로드**및 **동작** 메뉴를 사용하여 문서 라이브러리의 항목을 관리할 수 있습니다.  
  
### <a name="to-connect-a-filter-web-part"></a>필터 웹 파트를 연결하려면  
  
1.  웹 파트 페이지 또는 대시보드를 열거나 만듭니다.  
  
2.  
  **사이트 작업** 메뉴에서 **페이지 편집**을 클릭합니다.  
  
3.  **웹 파트 추가를**클릭 합니다.  
  
4.  **모든 웹 파트**의 **기타** 범주에서 **SQL Server Reporting Services 보고서 뷰어**를 선택 합니다.  
  
5.  **추가**를 클릭합니다. 영역의 맨 위에 웹 파트가 추가됩니다.  
  
6.  동일한 웹 파트 페이지 또는 대시보드의 다른 영역에서 **웹 파트 추가**를 클릭 합니다.  
  
7.  **모든 웹 파트**의 **필터** 섹션에서 웹 파트를 선택 합니다.  
  
8.  **추가**를 클릭합니다. 영역의 맨 위에 웹 파트가 추가됩니다.  
  
9. 웹 파트가 포함 된 영역에서 웹 파트 **편집** 메뉴를 클릭 하 고 **연결**, **필터 값 전송 대상**을 차례로 가리킨 다음 **보고서 뷰어** - *보고서 이름*을 선택 합니다.  
  
10. 변경 내용을 체크 인하고 페이지를 저장합니다.  
  
### <a name="to-connect-a-documents-web-part"></a>문서 웹 파트를 연결하려면  
  
1.  웹 파트 페이지 또는 대시보드를 열거나 만듭니다.  
  
2.  
  **사이트 작업** 메뉴에서 **페이지 편집**을 클릭합니다.  
  
3.  **웹 파트 추가를**클릭 합니다.  
  
4.  **모든 웹 파트**의 **목록 및 라이브러리** 섹션에서 문서를 선택 **합니다.**  
  
5.  **추가**를 클릭합니다. 영역의 맨 위에 웹 파트가 추가됩니다.  
  
6.  도구 창의 아래쪽에서 **적용** 을 클릭한 다음 **확인** 을 클릭하여 창을 닫습니다.  
  
7.  동일한 웹 파트 페이지 또는 대시보드의 다른 영역에서 **웹 파트 추가**를 클릭 합니다.  
  
8.  **모든 웹 파트**의 **기타** 범주에서 **SQL Server Reporting Services 보고서 뷰어를 선택 합니다.**  
  
9. **추가**를 클릭합니다. 영역의 맨 위에 웹 파트가 추가됩니다.  
  
10. 웹 파트가 포함 된 영역에서 웹 파트 **편집** 메뉴를 클릭 하 고 **연결**, **보고서 정의 가져오기**를 차례로 가리킨 다음 **문서**를 선택 합니다.  
  
11. 변경 내용을 체크 인하고 페이지를 저장합니다.  
  
## <a name="see-also"></a>참고 항목  
 [웹 페이지에 보고서 뷰어 웹 파트를 추가 하 여 SharePoint 통합 모드에서 Reporting Services &#40;&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)   
 [SharePoint 사이트의 보고서 뷰어 웹 파트](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [보고서 뷰어 웹 파트 사용자 지정](../../2014/reporting-services/customize-the-report-viewer-web-part.md)  
  
  
