---
title: "3단원: 보고서 마법사를 사용하여 부모 보고서 디자인 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
caps.latest.revision: "9"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4de8072efe47f62d59f13f7a1e4ed936ee7d1887
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>3단원: 보고서 마법사를 사용하여 부모 보고서 디자인
부모 보고서에 대한 데이터 테이블 및 데이터 연결을 만든 후에는 보고서 디자이너의 보고서 마법사를 사용하여 부모 보고서를 디자인합니다. 보고서 디자이너에 대한 자세한 내용은 [보고서 디자이너로 보고서 디자인&#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)을 참조하세요.  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>보고서 마법사를 사용하여 부모 보고서를 디자인하려면  
  
1.  **솔루션 탐색기**에서 최상위 웹 사이트가 선택되어 있는지 확인합니다.  
  
2.  웹 사이트를 마우스 오른쪽 단추로 클릭하고 **새 항목 추가**를 선택합니다.  
  
3.  **새 항목 추가** 대화 상자에서 **보고서 마법사**를 선택하고 보고서 파일의 이름을 입력한 다음 **추가**를 선택합니다.  
  
    그러면 보고서 마법사가 시작됩니다.  
  
4.  **데이터 집합 속성** 페이지의 **데이터 원본** 상자에서, **2단원: 부모 보고서에 대한 데이터 연결 및 데이터 테이블 정의** 에서 만든 [DataSet1](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)을 선택합니다.  
  
    **사용 가능한 데이터 집합** 상자가 위에서 만든 **DataTable** 로 자동 업데이트됩니다.  
  
5.  **다음**을 선택합니다.  
  
6.  **필드 정렬** 페이지에서 다음을 수행합니다.  
  
    1.  **ProductID**, **Name**, **ProductNumber**, **SafetyStockLevel**및 **ReorderLevel** 을 **사용 가능한 필드** 에서 **값** 상자로 끌어옵니다.  
  
    2.  **Sum(ProductID)**, **Sum(SafetyStockLevel)**, **Sum(ReorderLevel)** 옆에 있는 화살표를 선택하고 **합계** 선택을 취소합니다.  
  
7.  **다음** 을 두 번 선택한 다음 **마침** 을 선택하여 **보고서 마법사**를 닫습니다.  
  
    이제 .rdlc 파일을 만드는 작업을 마쳤습니다. 보고서 디자이너에서 파일이 열립니다. 디자인한 테이블릭스가 이제 디자인 화면에 표시됩니다.  
  
8.  .rdlc 파일을 저장합니다.  
  
## <a name="next-task"></a>다음 태스크  
보고서 마법사를 사용하여 성공적으로 부모 보고서를 디자인했습니다. 이제 자식 보고서에 대한 데이터 테이블 및 데이터 연결을 만듭니다. [4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)를 참조하세요.  
  
  
  

