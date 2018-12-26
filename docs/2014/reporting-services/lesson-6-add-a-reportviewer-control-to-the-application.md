---
title: '6단원: 애플리케이션에 ReportViewer 컨트롤 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: afb73e5dc93efdadb0754072d652b7328aaa2151
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104003"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>6단원: 애플리케이션에 ReportViewer 컨트롤 추가
  보고서 마법사를 사용하여 자식 보고서를 디자인한 후에는 웹 사이트 애플리케이션에 ReportViewer 컨트롤을 추가합니다.  
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>애플리케이션에 ReportViewer 컨트롤을 추가하려면  
  
1.  **솔루션 탐색기**에서 **Default.aspx**를 마우스 오른쪽 단추로 클릭한 다음 **뷰 디자이너**를 클릭합니다.  
  
2.  **도구 모음** 창의 **AJAX 확장** 그룹에서 **ScriptManager** 컨트롤을 디자인 화면으로 끌어옵니다.  
  
3.  **보고** 그룹에서 **ReportViewer** 컨트롤을 **ScriptManager** 컨트롤 아래의 디자인 화면으로 끌어옵니다.  
  
4.  **ReportViewer** 컨트롤의 오른쪽 위 모퉁이에 있는 화살표를 클릭하여 **ReportViewer 태스크** 창을 엽니다.  
  
5.  **보고서 선택** 상자에서 만든 부모 보고서를 선택합니다.  
  
     보고서를 선택하면 보고서에 사용된 데이터 원본의 인스턴스가 자동으로 만들어집니다. 각 DataTable 및 해당 [DataSet](http://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) 컨테이너를 인스턴스화하는 코드가 생성됩니다. [ObjectDataSource](http://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource\(v=vs.100\).aspx) 컨트롤은 보고서에 사용된 각 데이터 원본에 해당하는 디자인 화면에 추가됩니다. 이 데이터 원본 컨트롤은 자동으로 구성됩니다.  
  
     Microsoft Visual Studio 2012를 사용하고 있는 경우 정규화된 이름(예: Projectnamespace.DataSet1TableAdapters.ProductTableAdapter)이 **비즈니스 개체 선택** 드롭다운 목록에 나열되어 있으면 ObjectDataSource 컨트롤이 프로젝트 네임스페이스로 정규화된 DataSet1과 바인딩되어 있는지 확인합니다. ObjectDataSource를 마우스 오른쪽 단추로 클릭한 다음 **데이터 원본 구성**을 클릭하여 목록 상자에 액세스할 수 있습니다.  
  
6.  빌드 메뉴에서 웹 사이트 빌드를 클릭합니다.  
  
     보고서가 컴파일되고 보고서 식의 구문 오류와 같은 오류가 모두 **오류 목록** 영역에 표시됩니다. Visual Studio 창의 아래쪽에 있는 **오류 목록** 을 클릭하여 **오류 목록** 영역을 표시합니다.  
  
## <a name="next-task"></a>다음 태스크  
 웹 사이트 애플리케이션에 ReportViewer 컨트롤을 성공적으로 추가했습니다. 이제 부모 보고서에 드릴스루 동작을 추가합니다.  
  
  
