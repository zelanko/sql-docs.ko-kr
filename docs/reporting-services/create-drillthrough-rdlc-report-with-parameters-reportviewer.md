---
title: "매개 변수가-ReportViewer 드릴스루 (RDLC) 보고서 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8ce79884745b9e2fc9fbddfd7d312e982b2dd61c
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>매개 변수가-ReportViewer 드릴스루 (RDLC) 보고서 만들기
[드릴스루](http://technet.microsoft.com/library/ff519554.aspx) 보고서는 다른 보고서 내에서 링크를 클릭했을 때 열리는 보고서입니다. 드릴스루 보고서는 원본 요약 보고서에 포함된 항목에 대한 세부 정보를 포함합니다. 이 자습서에서는 [로컬 모드 보고](http://msdn.microsoft.com/library/ff487969.aspx)에서 매개 변수 및 쿼리가 있는 드릴스루 보고서를 만드는 다음과 같은 단원을 설명합니다.  
  
## <a name="requirements"></a>요구 사항  
이 연습을 사용하려면 **AdventureWorks2014** 샘플 데이터베이스에 대한 액세스 권한이 있어야 합니다. **AdventureWorks2014** 샘플 데이터베이스를 가져오는 방법에 대한 자세한 내용은 [Microsoft SQL Server 데이터베이스 제품 샘플](http://msftdbprodsamples.codeplex.com/)을 참조하세요.  
  
이 연습에서는 Transaction-SQL 쿼리와 ADO.NET [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) 및 [DataTable](http://msdn.microsoft.com/library/system.data.datatable.aspx) 개체를 잘 알고 있다고 가정합니다.  
  
Visual Studio 2015 및 ASP.NET 웹 응용 프로그램을 사용하여 ReportViewer 컨트롤이 있는 ASP.NET 웹 페이지를 만듭니다. 컨트롤은 사용자가 만드는 보고서를 보도록 구성됩니다. 이 연습에서는 Microsoft Visual C#에서 응용 프로그램을 만듭니다.  
  
## <a name="tasks"></a>태스크  
[1단원: 새 웹 사이트 만들기](../reporting-services/lesson-1-create-a-new-web-site.md)  
[2단원: 부모 보고서에 대한 데이터 연결 및 데이터 테이블 정의](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[3단원: 보고서 마법사를 사용하여 부모 보고서 디자인](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[5단원: 보고서 마법사를 사용하여 자식 보고서 디자인](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[6단원: 응용 프로그램에 ReportViewer 컨트롤 추가](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[7단원: 부모 보고서에 드릴스루 동작 추가](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[8단원: 데이터 필터 만들기](../reporting-services/lesson-8-create-a-data-filter.md)  
[Lesson 9: Build and Run the Application](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>참고 항목  
[Reporting Services&#40;SSRS&#41; 자습서](../reporting-services/reporting-services-tutorials-ssrs.md)  
[보고서 디자이너로 보고서 디자인&#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  


