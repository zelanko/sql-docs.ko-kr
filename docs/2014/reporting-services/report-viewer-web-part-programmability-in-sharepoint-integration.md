---
title: SharePoint 통합의 보고서 뷰어 웹 파트 프로그래밍 기능 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a0bc7e2d99190e142647ab8732e2d2d48b3ea2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63255141"
---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>SharePoint 통합의 보고서 뷰어 웹 파트 프로그래밍 기능
  보고서 뷰어 웹 파트는 `T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart` 서버 컨트롤로, 개발자가 사용자 지정 SharePoint 애플리케이션을 만드는 데 사용할 수 있는 공용 API(응용 프로그래밍 인터페이스) 집합을 포함합니다. 웹 파트 연결을 사용하여 보고서 뷰어 웹 파트에 보고서 경로 및 매개 변수를 제공하는 사용자 지정 웹 파트를 만들 수 있습니다. 사용자 지정 SharePoint 웹 파트 페이지 내에 웹 파트를 포함하고 공용 API를 사용하여 웹 파트를 사용자 지정할 수도 있습니다.  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>사용자 지정 웹 파트를 사용하여 보고서 뷰어 웹 파트에 연결  
 보고서 뷰어 웹 파트는 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 또는 `T:Microsoft.SharePoint.WebPartPages.IFilterValues`를 구현하는 SharePoint 웹 파트에 대한 연결 소비자입니다. <xref:System.Web.UI.WebControls.WebParts.IWebPartRow>문서**웹 파트와 같은** 웹 파트는 보고서 뷰어 웹 파트와 동일한 웹 파트 페이지에 배치되는 경우 보고서 뷰어 웹 파트에 보고서 경로를 제공할 수 있습니다. 마찬가지로, `T:Microsoft.SharePoint.WebPartPages.IFilterValues` **텍스트 필터** 또는 **선택 필터**와 같은 웹 파트는 보고서 뷰어 웹 파트와 동일한 웹 파트 페이지에 배치 될 때 보고서 뷰어 웹 파트에 보고서 매개 변수를 제공할 수 있습니다.  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>IWebPartRow를 사용하여 보고서 경로 공급자 구현  
 웹 파트 연결을 통해 보고서 뷰어 웹 파트에 보고서 경고를 제공하려면 다음을 수행하십시오.  
  
1.  <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 인터페이스를 구현하는 웹 파트를 만듭니다.  
  
2.  이 웹 파트를 보고서 뷰어 웹 파트와 동일한 웹 파트 페이지에 추가합니다.  
  
3.  웹 기반 웹 파트 디자인 사용자 인터페이스에서 웹 파트를 보고서 뷰어 웹 파트에 연결합니다.  
  
    > [!NOTE]  
    >  보고서 뷰어 웹 파트에는 한 번에 하나의 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트만 연결할 수 있으며, <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트와 `T:Microsoft.SharePoint.WebPartPages.IFilterValues` 웹 파트를 동시에 모두 연결할 수는 없습니다.  
  
 
  <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트가 `T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart`와 함께 올바르게 작동하려면 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A> 메서드에서 다음을 수행해야 합니다.  
  
-   입력 매개 변수로 <xref:System.Data.DataRowView> 개체를 사용하여 콜백 메서드를 호출합니다.  
  
-   <xref:System.Data.DataRowView> 개체에 보고서 경로를 포함하는 "DocUrl"이라는 열이 있는지 확인합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010용 추가 기능의 보고서 뷰어 웹 파트에서도 "FileRef" 열을 사용한 보고서 경로 받기를 지원합니다.  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>IFilterValues를 사용하여 보고서 매개 변수 공급자 구현  
 
  `T:Microsoft.SharePoint.WebPartPages.IFilterValues`를 구현하는 웹 파트는 보고서 뷰어 웹 파트에 하나의 매개 변수 값을 제공할 수 있습니다. 보고서 뷰어 웹 파트로 전달되는 이 매개 변수 값에는 보고서 정의에서 보고서 매개 변수에 대해 설정된 것과 동일한 제한(예: 데이터 형식, 유효한 값 등)이 적용됩니다.  
  
 보고서 뷰어 웹 파트에 보고서 매개 변수를 제공하려면 다음을 수행하십시오.  
  
1.  `T:Microsoft.SharePoint.WebPartPages.IFilterValues` 인터페이스를 구현하는 웹 파트를 만듭니다.  
  
2.  이 웹 파트를 `T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart`와 동일한 페이지에 추가합니다.  
  
3.  웹 기반 웹 파트 디자인 사용자 인터페이스에서 `T:Microsoft.SharePoint.WebPartPages.IFilterValues` 웹 파트를 보고서 뷰어 웹 파트에 연결합니다.  
  
    > [!NOTE]  
    >  보고서 뷰어 웹 파트에는 한 번에 여러 `T:Microsoft.SharePoint.WebPartPages.IFilterValues` 웹 파트를 연결할 수 있습니다. 그러나 보고서 뷰어 웹 파트에 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트와 `T:Microsoft.SharePoint.WebPartPages.IFilterValues` 웹 파트를 동시에 모두 연결할 수는 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [IFilterValues 인터페이스](https://msdn.microsoft.com/library/office/microsoft.sharepoint.webpartpages.ifiltervalues\(v=office.15\).aspx)  
  
  
