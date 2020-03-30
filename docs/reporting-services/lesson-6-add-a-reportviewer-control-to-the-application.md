---
title: '6단원: 애플리케이션에 ReportViewer 컨트롤 추가 | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9b13a3653b19d4079a47941a0bb05faa2821c823
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "62512538"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>6단원: 애플리케이션에 ReportViewer 컨트롤 추가
보고서 마법사를 사용하여 자식 보고서를 디자인한 후에는 웹 사이트 애플리케이션에 ReportViewer 컨트롤을 추가합니다. ASP.NET 보고서 웹 사이트를 사용하는 경우 default.aspx 페이지에 ReportViewer 컨트롤이 추가됩니다.   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>애플리케이션에 ReportViewer 컨트롤을 추가하려면  
  
1.  **솔루션 탐색기**에서 **Default.aspx**를 마우스 오른쪽 단추로 클릭한 다음 **뷰 디자이너**를 클릭합니다.  
  
2.  Default.aspx에 ReportViewer 컨트롤이 이미 있으면 **4단계**로 건너뜁니다. 컨트롤이 없으면 **도구 모음** 창의 **AJAX 확장** 그룹에서 **ScriptManager** 컨트롤을 디자인 화면으로 끌어옵니다.  
  
3.  **보고** 그룹에서 **ReportViewer** 컨트롤을 **ScriptManager** 컨트롤 아래의 디자인 화면으로 끌어옵니다.  
  
4.  **ReportViewer** 컨트롤의 오른쪽 위에 있는 화살표를 클릭하여 **ReportViewer 태스크** 창을 엽니다.  
  
5.  **보고서 선택** 상자에서 만든 부모 보고서를 선택합니다.  
  
    보고서를 선택하면 보고서에 사용된 데이터 원본의 인스턴스가 자동으로 만들어집니다. 각 DataTable 및 해당 [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) 컨테이너를 인스턴스화하는 코드가 생성됩니다. 보고서에 사용된 각 데이터 원본에 해당하는 [ObjectDataSource](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx) 컨트롤이 디자인 화면에 추가됩니다. 이 데이터 원본 컨트롤은 자동으로 구성됩니다.  
  
6.  빌드 메뉴에서 웹 사이트 빌드를 클릭합니다.  
  
    보고서가 컴파일되고 보고서 식의 구문 오류와 같은 오류가 모두 **오류 목록** 영역에 표시됩니다. Visual Studio 창의 아래쪽에 있는 **오류 목록** 을 클릭하여 **오류 목록** 영역을 표시합니다.  
  
## <a name="next-task"></a>다음 태스크  
웹 사이트 애플리케이션에 ReportViewer 컨트롤을 성공적으로 추가했습니다. 이제 부모 보고서에 드릴스루 동작을 추가합니다. [7단원: 부모 보고서에 드릴스루 동작 추가](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)를 참조하세요,  
  

