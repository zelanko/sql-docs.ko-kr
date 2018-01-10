---
title: "SharePoint 통합의 보고서 뷰어 웹 파트 프로그래밍 기능 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 714017b7-1bd6-4950-a3c6-d0df8450a877
caps.latest.revision: "8"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ded31cca0464d16657d095b6f3fac5344cbd33c0
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="report-viewer-web-part-programmability-in-sharepoint-integration"></a>SharePoint 통합의 보고서 뷰어 웹 파트 프로그래밍 기능
  보고서 뷰어 웹 파트는 서버 컨트롤로, 개발자가 사용자 지정 SharePoint 응용 프로그램을 만드는 데 사용할 수 있는 공용 API(응용 프로그래밍 인터페이스) 집합을 포함합니다. 웹 파트 연결을 사용하여 보고서 뷰어 웹 파트에 보고서 경로 및 매개 변수를 제공하는 사용자 지정 웹 파트를 만들 수 있습니다. 사용자 지정 SharePoint 웹 파트 페이지 내에 웹 파트를 포함하고 공용 API를 사용하여 웹 파트를 사용자 지정할 수도 있습니다.  
  
## <a name="connecting-to-report-viewer-web-part-with-custom-web-parts"></a>사용자 지정 웹 파트를 사용하여 보고서 뷰어 웹 파트에 연결  
 보고서 뷰어 웹 파트는 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 또는 T:Microsoft.SharePoint.WebPartPages.IFilterValues를 구현하는 SharePoint 웹 파트에 대한 연결 소비자입니다. **문서** 웹 파트와 같은 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트는 보고서 뷰어 웹 파트와 동일한 웹 파트 페이지에 배치되는 경우 보고서 뷰어 웹 파트에 보고서 경로를 제공할 수 있습니다. 마찬가지로, **텍스트 필터** 또는 **선택 필터**와 같은 T:Microsoft.SharePoint.WebPartPages.IFilterValues 웹 파트는 보고서 뷰어 웹 파트와 동일한 웹 파트 페이지에 배치되는 경우 보고서 뷰어 웹 파트에 보고서 매개 변수를 제공할 수 있습니다.  
  
### <a name="implementing-a-report-path-provider-with-iwebpartrow"></a>IWebPartRow를 사용하여 보고서 경로 공급자 구현  
 웹 파트 연결을 통해 보고서 뷰어 웹 파트에 보고서 경고를 제공하려면 다음을 수행하십시오.  
  
1.  <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 인터페이스를 구현하는 웹 파트를 만듭니다.  
  
2.  이 웹 파트를 보고서 뷰어 웹 파트와 동일한 웹 파트 페이지에 추가합니다.  
  
3.  웹 기반 웹 파트 디자인 사용자 인터페이스에서 웹 파트를 보고서 뷰어 웹 파트에 연결합니다.  
  
    > [!NOTE]  
    >  보고서 뷰어 웹 파트에는 한 번에 하나의 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트만 연결할 수 있으며, <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트와 T:Microsoft.SharePoint.WebPartPages.IFilterValues 웹 파트를 동시에 모두 연결할 수는 없습니다.  
  
 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트를 T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart와 함께 제대로 작동하려면 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow.GetRowData%2A> 메서드에서 다음을 수행해야 합니다.  
  
-   입력 매개 변수로 <xref:System.Data.DataRowView> 개체를 사용하여 콜백 메서드를 호출합니다.  
  
-   <xref:System.Data.DataRowView> 개체에 보고서 경로를 포함하는 "DocUrl"이라는 열이 있는지 확인합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2010용 추가 기능의 보고서 뷰어 웹 파트에서도 "FileRef" 열을 사용한 보고서 경로 받기를 지원합니다.  
  
### <a name="implementing-a-report-parameter-provider-with-ifiltervalues"></a>IFilterValues를 사용하여 보고서 매개 변수 공급자 구현  
 T:Microsoft.SharePoint.WebPartPages.IFilterValues를 구현하는 웹 파트는 보고서 뷰어 웹 파트에 하나의 매개 변수 값을 제공할 수 있습니다. 보고서 뷰어 웹 파트로 전달되는 이 매개 변수 값에는 보고서 정의에서 보고서 매개 변수에 대해 설정된 것과 동일한 제한(예: 데이터 형식, 유효한 값 등)이 적용됩니다.  
  
 보고서 뷰어 웹 파트에 보고서 매개 변수를 제공하려면 다음을 수행하십시오.  
  
1.  T:Microsoft.SharePoint.WebPartPages.IFilterValues 인터페이스를 구현하는 웹 파트를 만듭니다.  
  
2.  웹 파트를 T:Microsoft.ReportingServices.SharePoint.UI.WebParts.ReportViewerWebPart와 동일한 페이지에 추가합니다.  
  
3.  웹 기반 웹 파트 디자인 사용자 인터페이스에서 T:Microsoft.SharePoint.WebPartPages.IFilterValues 웹 파트를 보고서 뷰어 웹 파트에 연결합니다.  
  
    > [!NOTE]  
    >  한 번에 여러 개의 T:Microsoft.SharePoint.WebPartPages.IFilterValues 웹 파트를 보고서 뷰어 웹 파트에 연결할 수 있습니다. 그러나 <xref:System.Web.UI.WebControls.WebParts.IWebPartRow> 웹 파트와 T:Microsoft.SharePoint.WebPartPages.IFilterValues 웹 파트를 보고서 뷰어 웹 파트에 동시에 모두 연결할 수 없습니다.  
  
  
