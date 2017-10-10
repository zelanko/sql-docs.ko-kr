---
title: "Reporting Services 보고서 뷰어 웹 파트와 필터 또는 문서 웹 파트에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 87d4b4a3f0c01804329f3a7b0688632c20ed6c9b
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>Reporting Services 보고서 뷰어 웹 파트와 필터 또는 문서 웹 파트에 연결

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SharePoint 제품을 사용 하는 경우 필터 웹 파트 또는 문서 웹 파트와 보고서 뷰어 웹 파트가 포함 된 페이지는 대시보드 또는 웹 파트를 만들 수 있습니다. 선택한 버전은 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 또는 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]입니다. 또한 지원되는 버전은 [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] 또는 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007입니다. 필터 웹 파트를 연결 하면 필터 웹 파트의 필터 값을 선택 하는 동일한 페이지에 매개 변수가 있는 보고서에 값을 보낼 수 있습니다. 문서 웹 파트를 연결 하 여 문서 라이브러리의 보고서를에서 클릭 하 여 인접 보고서 뷰어 웹 파트에는 보고서를 볼 수 있습니다.

> [!NOTE]
> SQL Server 2016 후 SharePoint와 reporting Services 통합을 사용할 수 없습니다.

 필터 웹 파트는 보고서에 하나 이상의 매개 변수에 값을 보내는 데 사용 됩니다. 필터 웹 파트를 사용 하려면 보고서의 값, 데이터 형식 및 형식에 웹 파트가 보낸와 호환 되는 매개 변수가 정의 되어 있어야 합니다.  
  
 문서 웹 파트는 홈 사이트의 문서 라이브러리와 관련이 있습니다. 문서 라이브러리에서 항목을 보거나, 추가하거나, 제거하려면 **모든 사이트 콘텐츠 보기**를 클릭합니다. 그런 다음 라이브러리에서 **문서**를 클릭합니다. **새로 만들기**, **업로드**및 **동작** 메뉴를 사용하여 문서 라이브러리의 항목을 관리할 수 있습니다.  
  
## <a name="connect-a-filter-web-part"></a>필터 웹 파트 연결
  
1.  열거나 웹 파트 페이지 또는 대시보드를 만듭니다.  
  
2.  **사이트 작업** 메뉴에서 **페이지 편집**을 클릭합니다.  
  
3.  클릭 **웹 파트 추가**합니다.  
  
4.  **모든 웹 파트**에 **기타** 범주를 **SQL Server Reporting Services 보고서 뷰어**합니다.  
  
5.  **추가**를 클릭합니다. 웹 파트는 위쪽 영역에 추가 됩니다.  
  
6.  동일한 웹 파트 페이지 또는 대시보드의 다른 영역에서 클릭 **웹 파트 추가**합니다.  
  
7.  **모든 웹 파트**에 **필터** 섹션에서 웹 파트를 선택 합니다.  
  
8.  **추가**를 클릭합니다. 웹 파트는 위쪽 영역에 추가 됩니다.  
  
9. 웹 파트가 포함 된 영역에 웹 파트를 클릭 합니다. **편집** 메뉴에서 **연결**, 가리킨 **필터 값 전송 대상**를 선택한 후 **보고서 뷰어** - *보고서 이름*합니다.  
  
10. 변경 내용을 체크 인하고 페이지를 저장합니다.  
  
## <a name="connect-a-documents-web-part"></a>문서 웹 파트 연결  
  
1.  열거나 웹 파트 페이지 또는 대시보드를 만듭니다.  
  
2.  **사이트 작업** 메뉴에서 **페이지 편집**을 클릭합니다.  
  
3.  클릭 **웹 파트 추가**합니다.  
  
4.  **모든 웹 파트**에 **목록 및 라이브러리** 섹션에서 **문서.**  
  
5.  **추가**를 클릭합니다. 웹 파트는 위쪽 영역에 추가 됩니다.  
  
6.  도구 창의 아래쪽에서 **적용** 을 클릭한 다음 **확인** 을 클릭하여 창을 닫습니다.  
  
7.  동일한 웹 파트 페이지 또는 대시보드의 다른 영역에서 클릭 **웹 파트 추가**합니다.  
  
8.  **모든 웹 파트**에 **기타** 범주에서 **SQL Server Reporting Services 보고서 뷰어.**  
  
9. **추가**를 클릭합니다. 웹 파트는 위쪽 영역에 추가 됩니다.  
  
10. 웹 파트가 포함 된 영역에 웹 파트를 클릭 합니다. **편집** 메뉴에서 **연결**, 가리킨 **보고서 정의를 가져올**를 선택한 후  **문서**합니다.  
  
11. 변경 내용을 체크 인하고 페이지를 저장합니다.  
  
## <a name="see-also"></a>참고 항목

 [웹 페이지에 보고서 뷰어 웹 파트 추가](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [SharePoint 사이트에서 보고서 뷰어 웹 파트](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [보고서 뷰어 웹 파트를 사용자 지정](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
