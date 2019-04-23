---
title: ReportViewer (SSRS 자습서)를 사용 하 여 매개 변수가 있는 드릴스루 (RDLC) 보고서 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 79e43f273183d531a8fbc61fd71315a971213773
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59959959"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>ReportViewer를 사용하여 매개 변수가 있는 드릴스루(RDLC) 보고서 만들기(SSRS 자습서)
  [드릴스루](https://technet.microsoft.com/library/ff519554.aspx) 보고서는 다른 보고서 내에서 링크를 클릭했을 때 열리는 보고서입니다. 드릴스루 보고서는 원본 요약 보고서에 포함된 항목에 대한 세부 정보를 포함합니다. 이 자습서에서는 [로컬 모드 보고](local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)에서 매개 변수 및 쿼리가 있는 드릴스루 보고서를 만드는 다음과 같은 단원을 설명합니다.  
  
## <a name="requirements"></a>요구 사항  
 이 연습을 사용하려면 **AdventureWorks2008** 예제 데이터베이스에 대한 액세스 권한이 있어야 합니다. 이 연습에서 사용하는 쿼리는 **AdventureWorks2012** 데이터베이스에서도 작동합니다. 가져오는 방법에 대 한 자세한 내용은 합니다 **AdventureWorks2008** 예제 데이터베이스를 참조 하십시오 [연습: AdventureWorks 데이터베이스 설치](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx) for Microsoft Visual Studio 2010.  
  
 이 연습에서는 Transaction-SQL 쿼리와 ADO.NET [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) 및 [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) 개체를 잘 알고 있다고 가정합니다.  
  
 Visual Studio 2010 또는 Visual Studio 2012 및 ASP.NET 웹 사이트 템플릿을 사용하여 ReportViewer 컨트롤이 있는 ASP.NET 웹 페이지를 만듭니다. 컨트롤은 사용자가 만드는 보고서를 보도록 구성됩니다. 이 연습에서는 Microsoft Visual C#에서 애플리케이션을 만듭니다.  
  
## <a name="tasks"></a>태스크  
 [1단원: 새 웹 사이트 만들기](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [2단원: 부모 보고서에 대 한 데이터 연결 및 데이터 테이블 정의](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [3단원: 보고서 마법사를 사용 하 여 부모 보고서 디자인](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [4단원: 자식 보고서에 대 한 데이터 연결 및 데이터 테이블 정의](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [5단원: 보고서 마법사를 사용 하 여 자식 보고서 디자인](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [6단원: 응용 프로그램에 ReportViewer 컨트롤 추가](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [7단원: 부모 보고서에 드릴스루 동작 추가](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [8단원: 데이터 필터 만들기](../reporting-services/lesson-8-create-a-data-filter.md)   
 [9 단원: 빌드 및 응용 프로그램 실행](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 자습서 &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [보고서 디자이너로 보고서 디자인&#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
