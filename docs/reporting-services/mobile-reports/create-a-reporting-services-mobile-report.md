---
title: "Reporting Services 모바일 보고서 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e84dc855-aede-4fb4-b721-e6d8787961f4
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7fce4526bb296113aedb62e5dcf94b50e198210f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-reporting-services-mobile-report"></a>Reporting Services 모바일 보고서 만들기
SQL Server 모바일 보고서 게시자는 신속 하 게 조정 가능한 표 행 및 열, 유동적인 모바일 보고서 요소는 디자인 화면에서 어떤 화면 크기에 맞게 조정 하는 SQL Server 2016 Reporting Services 모바일 보고서를 만들 수 있습니다.  
  
처음에 모바일 보고서를 만들 때 Reporting Services 웹 포털에서 로컬 컴퓨터의 SQL Server 모바일 보고서 게시자를 설치할 수 있습니다. 또는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkID=733527)에서 설치할 수 있습니다. 처음 만든 후에는 웹 포털이나 로컬에서 보고서 게시자를 시작할 수 있습니다.   
    
1. Reporting Services 웹 포털의 위쪽 막대에서 선택 **새로** > **모바일 보고서**합니다.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. 에 **레이아웃** 탭 모바일 보고서 게시자에서 탐색기, 계기, 차트, 지도, 또는 datagrid 선택한 다음 디자인 눈금으로 끕니다.  
  
3. 요소의 오른쪽 아래 모서리를 클릭하여 원하는 크기로 끕니다.  
  
   ![SSMRP_ResizeChart](../../reporting-services/mobile-reports/media/ssmrp-resizechart.png)  
  
   위 그림에 표시되어 있는 **마스터** 디자인 눈금에서는 보고서에 포함할 요소를 만듭니다. 나중에 [태블릿이나 휴대폰용 보고서 레이아웃을 지정](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)할 수 있습니다.     
     
   디자인 눈금 아래의 **시각적 속성** 에서는 다양한 속성을 설정할 수 있습니다.  
     
4. 왼쪽 위에서 **데이터** 탭을 선택하면 차트에 시뮬레이트된 데이터가 이미 연결되어 있음을 확인할 수 있습니다.   
  
   ![SSMRP_SimTable](../../reporting-services/mobile-reports/media/ssmrp-simtable.png)  
  
5. 오른쪽 위에서 **데이터 추가** 를 선택합니다.  
  
6. **로컬 Excel** 또는 **보고서 서버**를 선택합니다.  
  
   >**팁**: Excel에서 데이터를 추가하는 경우에는 다음 작업을 수행해야 합니다.  
    >* 모바일 보고서에서 사용할 [Excel 데이터를 준비](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md) 해야 합니다.  
    >* Excel 파일을 먼저 닫아야 합니다.  
7. 원하는 워크시트를 선택하고 **가져오기**를 선택합니다.   
   통합 문서에서 한 번에 여러 워크시트를 추가할 수 있습니다.  
    
     ![SSMRP_AddExcelData](../../reporting-services/mobile-reports/media/ssmrp-addexceldata.png)  
  
8. 계속 **데이터** 탭이 표시된 상태로 **데이터 속성** 상자에서 차트에 포함할 테이블과 필드를 선택합니다.  
  
   ![SSMRP_DataProps](../../reporting-services/mobile-reports/media/ssmrp-dataprops.png)  
  
9. 다시 **레이아웃** 탭으로 돌아와 **시각적 속성** 상자에서 **제목**, **시간 단위**, **숫자 형식**등의 속성을 설정할 수 있습니다.  
  
   ![SSMRP_ChartVizProps](../../reporting-services/mobile-reports/media/ssmrp-chartvizprops.png)  
    
10. 왼쪽 위에서 **미리 보기** 를 선택하여 보고서의 모양을 확인합니다.  
  
11. 이제 보고서를 저장합니다. 왼쪽 위의 저장 아이콘을 선택하고 **로컬에 저장** 또는 **서버에 저장**을 클릭합니다.  
  
   서버를 저장 하려면 SQL Server 2016 Reporting Services 보고서 서버에 액세스를 해야 합니다.  
     
   ### <a name="see-also"></a>참고 항목  
     
-   [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-   [휴대폰 또는 태블릿용 Reporting Services 모바일 보고서 레이아웃](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)  
  
   
