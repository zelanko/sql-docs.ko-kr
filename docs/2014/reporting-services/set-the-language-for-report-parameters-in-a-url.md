---
title: URL에 보고서 매개 변수 언어 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- overriding report language settings
- report servers [Reporting Services], language settings
- languages [Reporting Services]
- URL access [Reporting Services], language overrides
- international considerations [Reporting Services]
- global considerations [Reporting Services]
ms.assetid: e1ccf22f-80d6-45bc-aae0-f5f263275092
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c6150d3060861d2e485ea8e3cd5ad2a0eecc6e38
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031404"
---
# <a name="set-the-language-for-report-parameters-in-a-url"></a>URL에 보고서 매개 변수 언어 설정
  *rs:ParameterLanguage* URL액세스 매개 변수를 사용하면 날짜, 시간, 통화, 숫자 등의 culture 구분 보고서 매개 변수가 브라우저 언어를 사용하여 해석되는 문제가 완화됩니다. *rs:ParameterLanguage*를 사용하면 URL이 브라우저와 상관없이 해석됩니다. 예를 들어 보고서 서버가 독일어 지역 설정으로 설정되었지만 사용자가 영어-미국으로 설정된 브라우저를 사용하여 URL을 통해 보고서에 액세스한다면 보고서 서버에 전달되는 매개 변수 값이 잘못 해석됩니다.  
  
 보고서에 대해 다음 URL을 고려하십시오.  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008  
```  
  
 위의 경우 "de-de" 문화권에서 실행되는 서버는 전자 메일 구독 또는 하이퍼링크를 통해 URL을 생성합니다. 하이퍼링크에서는 보고서가 독일어 날짜/시간 표준에 따라 시작 날짜 2008년 10월 4일과 종료 날짜 2008년 10월 11일로 매개 변수화되어야 함을 나타냅니다. 하지만 사용자가 "en-us"로 설정된 브라우저를 통해 URL에 액세스하면 미국 영어 날짜/시간 표준에 따라 서버에서 값을 2008년 4월 10일과 2008년 11월 10일로 해석하게 됩니다. 이 문제를 해결하려면 *rs:ParameterLanguage* 를 사용하여 매개 변수 해석을 위한 브라우저 언어를 다시 정의할 수 있습니다.  
  
```  
http://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
```  
  
 URL 액세스 매개 변수 **rc:Parameters** 에 대한 **true** 및 *false*값 이외에 이제 **Collapsed**값을 전달할 수 있습니다. URL에서 *rc:Parameters*=**Collapsed** 를 사용할 경우 HTML 뷰어의 매개 변수 프롬프트 영역이 보이지 않도록 축소되지만 사용자가 표시 여부를 선택할 수 있습니다. **false** 값을 사용하면 HTML 뷰어 도구 모음에서 매개 변수 프롬프트 영역이 제거되어 최종 사용자가 사용할 수 없습니다.  
  
## <a name="see-also"></a>관련 항목  
 [URL 액세스&#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  
