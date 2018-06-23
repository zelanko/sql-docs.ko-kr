---
title: (SharePoint 통합된 모드의 Reporting Services) 보고서에서 텍스트, 숫자 또는 날짜 찾기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- searching reports
ms.assetid: 309dffe5-00f5-404f-bb63-9e6046253ae0
caps.latest.revision: 11
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 6fe713a9ef49efdf6cb1a04da094f877fc614582
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092613"
---
# <a name="find-text-numbers-or-dates-in-a-report-reporting-services-in-sharepoint-integrated-mode"></a>보고서에서 텍스트, 숫자 또는 날짜 찾기(SharePoint 통합 모드의 Reporting Services)
  찾을 단어나 구(검색 단어는 최대 256자까지 입력 가능)를 입력하여 보고서 내용을 검색할 수 있습니다. 검색은 보고서에서 일치하는 값을 찾아 해당 값이 포함된 보고서 부분에 중점을 두는 탐색 기술입니다.  
  
 검색은 대/소문자를 구분하며 현재 선택한 페이지나 섹션에서 시작됩니다. 보고서에 표시되는 내용만 검색 작업에 포함됩니다. 보고서에 확장하거나 축소하는 영역이 포함되어 있는 경우 축소된 영역의 값은 검색 중에 건너뜁니다. 현재 보고서에 있는 텍스트, 숫자 또는 날짜만 검색할 수 있습니다. 자동 생성된 클릭 광고 보고서를 사용하여 데이터를 탐색하는 경우 이전에 생성된 보고서에서 본 용어는 검색할 수 없으며 데이터 경로 아래의 보고서에 나타날 수 있는 용어를 검색하여 찾을 수도 없습니다.  
  
 검색할 값을 입력할 때는 보고서에 표시되는 대로 값을 입력합니다. 문장의 모든 단어가 보고서에 있는 경우가 아니면 "이달의 평균 수익은 얼마입니까" 등의 질문을 사용하지 마십시오.  
  
 한 번에 하나의 용어나 값만 검색할 수 있습니다. 검색 연산자(예: AND 또는 OR)나 기호 및 와일드카드는 사용할 수 없습니다. 데이터의 교집합 영역(예: 특정 제품에 대한 특정 월의 순매출 검색)은 검색할 수 없습니다. 이러한 종류의 분석을 수행하려면 보고서 작성기를 사용하여 클릭 광고 보고서를 만들거나 사용합니다.  
  
 보고서 데이터에 대한 액세스를 제한하는 데이터베이스 및 모델 보안 설정이 검색 작업에 적용됩니다. 모델을 데이터 원본으로 사용하는 클릭 광고 보고서에서 값을 검색 중이며 모델의 일부에 액세스할 수 없는 경우 해당 모델 부분이 나타내는 데이터는 검색에서 제외됩니다.  
  
### <a name="to-find-data-in-a-report"></a>보고서에서 데이터를 찾으려면  
  
1.  보고서를 엽니다.  
  
2.  보고서 도구 모음에서 찾으려는 텍스트, 숫자 또는 날짜를 입력합니다.  
  
     보고서 도구 모음이 표시되지 않는 경우 숨겨진 것으로 보고서 도구 모음에서 제공하는 기능을 사용할 수 없습니다. 보고서 뷰어 웹 파트의 속성에 따라 도구 모음의 표시 여부가 결정됩니다.  
  
3.  **찾기**를 클릭합니다.  
  
4.  같은 값을 계속 검색하려면 **다음**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [웹 페이지에 보고서 뷰어 웹 파트를 추가할 &#40;Reporting Services sharepoint에서 통합 모드&#41;](../report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  