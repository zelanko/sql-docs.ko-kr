---
title: 동작 속성 대화 상자 (보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.shared.action.f1
- "10413"
- "10504"
- sql12.rtp.rptdesigner.calculatedseriesproperties.action.f1
- sql12.rtp.rptdesigner.pictureproperties.action.f1
- sql12.rtp.rptdesigner.actionproperties.f1
- sql12.rtp.rptdesigner.charttitleproperties.action.f1
- "10133"
- "10052"
- "10147"
- sql12.rtp.rptdesigner.chartproperties.action.f1
- "10122"
- sql12.rtp.rptdesigner.serieslabelproperties.action.f1
- sql12.rtp.rptdesigner.textboxproperties.action.f1
- "10162"
- "10168"
- sql12.rtp.rptdesigner.textproperties.action.f1
- sql12.rtp.rptdesigner.placeholderproperties.action.f1
- "10250"
- "10129"
- "10244"
- sql12.rtp.rptdesigner.seriesproperties.action.f1
ms.assetid: 2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9
caps.latest.revision: 13
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 4cae7e5c0de408c4a2ed9636e3c941f8e0a32b0e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090610"
---
# <a name="action-properties-dialog-box-report-builder-and-ssrs"></a>동작 속성 대화 상자(보고서 작성기 및 SSRS)
  **동작** 대화 상자를 사용하여 링크를 지원하는 차트, 계기 및 지도 요소에 대한 하이퍼링크 옵션을 활성화할 수 있습니다. 사용자가 보고서를 클릭하여 URL로 이동하거나, 동일한 보고서 서버 또는 보고서 서버와 통합된 SharePoint 사이트에 있는 다른 보고서로 이동하거나, 동일한 보고서 내의 다른 위치로 이동할 수 있는 동작을 정의합니다.  
  
## <a name="options"></a>변수  
 **동작으로 사용**  
 사용자가 항목을 클릭할 때 수행할 동작을 나타내려면 이 옵션을 선택합니다.  
  
 **없음**  
 항목을 클릭했을 때 아무런 동작도 수행하지 않도록 지정하려면 이 옵션을 선택합니다.  
  
 **보고서로 이동**  
 보고서 서버에 있는 드릴스루 보고서에 대한 링크를 만들려면 이 옵션을 선택합니다. **보고서로 이동**을 선택하면 다음 옵션이 추가로 표시됩니다.  
  
 **보고서 지정**  
 드릴스루 보고서로 사용할 보고서 이름을 입력하거나 선택합니다. 드릴스루 보고서는 이 보고서와 동일한 보고서 서버에 있어야 합니다.  
  
 기본 모드로 구성된 보고서 서버에 게시된 보고서의 경우 파일 이름 확장명 없이 전체 경로나 상대 경로를 사용합니다. 보고서가 현재 보고서와 같은 폴더에 있으면 보고서 이름만 사용합니다. 보고서가 동일한 보고서 서버의 다른 폴더에 있으면 상대 경로 또는 전체 경로를 사용합니다. 상대 경로는 현재 폴더에서 시작하여 폴더 계층의 위로 이동합니다(예: ../Folder2/Report1). 전체 경로는 홈 폴더인 /에서 시작합니다. 예를 들면 /Reports/Report1과 같은 형태입니다.  
  
 SharePoint 통합 모드로 구성된 보고서 서버에 게시된 보고서의 경우 파일 이름 확장명(.rdl)을 포함하여 정규화된 URL을 사용합니다(예: 예를 들어 http://*\<SharePointservername > /\<사이트 >*/Documents/Report1.rdl 합니다. 상대 경로는 지원되지 않습니다.  
  
 자세한 내용은 msdn.microsoft.com의 [보고서 작성기 설명서](http://go.microsoft.com/fwlink/?LinkId=154494)에서 [외부 항목에 대한 경로 지정&#40;보고서 작성기 및 SSRS&#41;](report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)을 참조하세요.  
  
 **이러한 매개 변수를 사용 하 여 보고서를 실행 하려면**  
 드릴스루 보고서에 전달할 매개 변수 목록을 추가합니다. 매개 변수 이름은 대상 보고서에 대해 정의된 매개 변수와 일치해야 합니다. **추가** 단추와 **삭제** 단추를 사용하여 매개 변수를 추가 및 제거하고 위쪽 화살표와 아래쪽 화살표를 사용하여 매개 변수 목록의 순서를 지정합니다.  
  
 **추가**  
 드릴스루 보고서에 전달할 새 매개 변수를 추가합니다.  
  
 **Delete**  
 드릴스루 보고서의 매개 변수를 삭제합니다.  
  
 **위쪽 화살표**  
 매개 변수를 목록에서 위로 이동합니다.  
  
 **아래쪽 화살표**  
 매개 변수를 목록에서 아래로 이동합니다.  
  
 **이름**  
 드릴스루 보고서에 정의된 매개 변수의 이름을 입력합니다.  
  
 **Value**  
 드릴스루 보고서의 명명된 매개 변수에 전달할 값을 입력하거나 선택합니다. 식을 편집하려면 **식** 단추(*fx*)를 클릭합니다.  
  
 **생략**  
 매개 변수가 실행되지 않도록 하려면 이를 선택합니다. 기본적으로 이 확인란은 선택 취소하여 비활성화되어 있습니다. 확인란을 선택하려면 **식** 단추(*fx*)를 클릭하고 **True** 을 입력하거나 식을 만듭니다. **식** 대화 상자에서 **확인** 을 클릭하면 확인란이 선택됩니다.  
  
 **책갈피로 이동**  
 현재 보고서에서 책갈피 링크를 정의하려면 이 옵션을 선택합니다. **책갈피로 이동**을 선택하면 다음 옵션이 추가로 표시됩니다.  
  
 **책갈피 선택**  
 사용자가 링크를 클릭할 때 이동할 보고서의 책갈피 ID를 입력하거나 선택합니다. 식을 변경하려면 식 단추(**fx**)를 클릭합니다. 책갈피 ID는 정적 ID이거나 책갈피 ID를 반환하는 식일 수 있습니다. 식은 책갈피 ID가 들어 있는 필드를 포함할 수 있습니다.  
  
 책갈피에 연결하려면 먼저 보고서 항목의 책갈피 속성을 설정해야 합니다. 책갈피 속성을 설정하려면 보고서 항목을 선택하고 속성 창에서 SalesChart 또는 5TopSales와 같이 책갈피 ID에 대한 값이나 식을 입력합니다.  
  
 **URL로 이동**  
 웹 페이지에 대한 링크를 정의하려면 이 옵션을 선택합니다. 웹 페이지의 URL 또는 이를 반환하는 식을 입력하거나 선택합니다. 식을 변경하려면 **식** 단추(*fx*)를 클릭합니다. 식은 URL이 들어 있는 필드를 포함할 수 있습니다. **URL로 이동**을 선택하면 다음 옵션이 추가로 표시됩니다.  
  
 **URL 선택**  
 항목의 URL을 입력합니다. 기본 모드로 구성된 보고서 서버에 게시된 항목의 경우 전체 경로나 상대 경로를 사용합니다. 예를 들어 http://*\<서버 이름 >*/images/image1.jpg입니다. SharePoint 통합 모드로 구성 된 보고서 서버에 게시 된 항목의 경우 정규화 된 URL을 사용 하 여 (예를 들어 http://*\<SharePointservername > /\<사이트 >*  /이미지/설명 / image1.jpg)입니다.  
  
## <a name="see-also"></a>관련 항목  
 [차트&#40;보고서 작성기 및 SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [대화 상자, 창 및 마법사에 대한 보고서 작성기 도움말](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [하위 보고서 및 매개 변수 추가&#40;보고서 작성기 및 SSRS&#41;](report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [대화형 정렬, 문서 구조 및 링크 &#40;보고서 작성기 및 SSRS&#41;](report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
  