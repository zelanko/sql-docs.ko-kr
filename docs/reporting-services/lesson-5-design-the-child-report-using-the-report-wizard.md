---
title: "5단원: 보고서 마법사를 사용하여 하위 보고서 디자인 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: "8"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b84722749ad94251c057a43858e2da98b37d2adb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>5단원: 보고서 마법사를 사용하여 자식 보고서 디자인
자식 보고서에 대한 데이터 테이블 및 데이터 연결을 만든 후에는 보고서 디자이너의 보고서 마법사를 사용하여 자식 보고서를 디자인합니다. 보고서 디자이너에 대한 자세한 내용은 [보고서 디자이너로 보고서 디자인&#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)을 참조하세요.  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>보고서 마법사를 사용하여 자식 보고서를 디자인하려면  
  
1.  **솔루션 탐색기**에서 최상위 웹 사이트가 선택되어 있는지 확인합니다.  
  
2.  웹 사이트를 마우스 오른쪽 단추로 클릭하고 **새 항목 추가**를 선택합니다.  
  
3.  **새 항목 추가** 대화 상자에서 **보고서 마법사**를 클릭하고 보고서 파일의 이름을 입력한 다음 **추가**를 선택합니다.  
  
    그러면 보고서 마법사가 시작됩니다.  
  
4.  **데이터 집합 속성** 페이지의 **데이터 원본** 상자에서 **DataSet2**를 선택합니다.  
  
    **사용 가능한 데이터 집합** 상자가 만들어진 DataTable로 자동 업데이트됩니다.  
  
5.  **다음**을 선택합니다.  
  
6.  **필드 정렬** 페이지에서 다음을 수행합니다.  
  
    1.  **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**및 **StockedQty**를 **사용 가능한 필드** 에서 **값** 상자로 끌어옵니다.  
  
    2.  **Sum(ProductID)**, **Sum(PurchaseOrderID)**, **Sum(PurchaseOrderDetailID)**, **Sum(OrderQty)**, **Sum(ReceivedQty)**, **Sum(RejectedQty)** 및 **Sum(StockedQty)** 옆에 있는 화살표를 선택하고 **합계** 선택을 취소합니다.  
  
7.  **다음**을 두 번 선택한 다음 **마침**을 선택하여 **보고서 마법사**를 닫습니다.  
  
    이제 .rdlc 파일을 만드는 작업을 마쳤습니다. 보고서 디자이너에서 파일이 열립니다. 디자인한 테이블릭스가 이제 디자인 화면에 표시됩니다.  
  
8.  .rdlc 파일이 열려 있는 상태에서 다음을 수행하여 매개 변수를 추가합니다.  
  
    1.  **보고서 데이터** 창의 **매개 변수**를 마우스 오른쪽 단추로 클릭한 다음 **매개 변수 추가**를 선택합니다.  
  
    2.  **이름** 상자에 **productid**를 입력합니다.  
  
    3.  **데이터 형식** 목록 상자에서 **정수**를 선택했는지 확인합니다.  
  
    4.  **확인**을 클릭합니다.  
  
9. .rdlc 파일을 저장합니다.  
  
## <a name="next-task"></a>다음 태스크  
보고서 마법사를 사용하여 성공적으로 자식 보고서를 디자인했습니다. 이제 웹 사이트 응용 프로그램에 ReportViewer 컨트롤을 추가합니다. [6단원: 응용 프로그램에 ReportViewer 컨트롤 추가](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)를 참조하세요.  
  
  
  

