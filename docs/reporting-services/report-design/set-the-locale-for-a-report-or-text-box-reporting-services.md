---
title: "보고서 또는 입력란 (Reporting Services)에 대 한 로캘을 설정 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locales [Reporting Services]
ms.assetid: df115b01-184b-47f0-b5ec-0ad965ff9bee
caps.latest.revision: 43
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3ce894281c47d0e54837917b05e785e9d106cdfa
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="set-the-locale-for-a-report-or-text-box-reporting-services"></a>보고서 또는 입력란에 대한 로캘 설정(Reporting Services)
  보고서 또는 입력란의 **Language** 속성에는 날짜, 통화 또는 숫자 값과 같이 언어 및 국가에 따라 다른 보고서 데이터를 표시하기 위한 기본 형식을 결정하는 로캘 설정이 포함됩니다. 입력란의 **Language** 속성은 보고서의 **Language** 속성을 재정의합니다. **Language**에 값을 지정하지 않을 경우 Reporting Services는 게시된 보고서에 대해서는 보고서 서버의 운영 체제 로캘을 사용하고 보고서 미리 보기에 대해서는 보고서 작성 컴퓨터의 로캘을 사용합니다.  
  
 HTML 보고서의 경우 보고서 또는 입력란의 **Language** 속성에 대한 식에 기본 제공 필드 User!Language를 사용하여 기본 **Language** 값을 재정의하고 브라우저 클라이언트의 HTTP 헤더로 지정된 언어를 사용할 수 있습니다.  
  
 보고서의 **Language** 속성을 URL로 지정할 수도 있습니다. 자세한 내용은 [URL에 보고서 매개 변수 언어 설정](../../reporting-services/set-the-language-for-report-parameters-in-a-url.md)을 참조하세요.  
  
### <a name="to-set-the-locale-for-a-report"></a>보고서에 대한 로캘을 설정하려면  
  
1.  디자인 뷰에서 보고서 디자인 화면 바깥쪽을 클릭하여 보고서를 선택합니다.  
  
2.  속성 창의 **Language** 속성에서 보고서에 사용할 언어를 입력하거나 선택합니다.  
  
### <a name="to-set-the-locale-for-a-text-box"></a>입력란에 대한 로캘을 설정하려면  
  
1.  디자인 뷰에서 로캘 설정을 적용할 입력란을 선택합니다.  
  
2.  속성 창에서 다음을 수행합니다.  
  
    -   **Calendar** 속성에서 날짜에 사용할 달력을 입력하거나 선택합니다.  
  
    -   **Direction** 속성에서 텍스트의 방향을 입력하거나 선택합니다.  
  
    -   **Language** 속성에서 입력란에 사용할 언어를 입력하거나 선택합니다. 이 값은 보고서의 **Language** 속성을 재정의합니다.  
  
    -   **NumeralLanguage** 속성에서 입력란의 숫자에 사용할 형식을 입력하거나 선택합니다.  
  
    -   **NumeralVariant** 속성에서 입력란의 숫자에 사용할 형식의 변형을 입력하거나 선택합니다.  
  
    -   **UnicodeBiDi** 속성에서 입력란에 사용할 양방향 포함 수준을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [다국어 배포 또는 글로벌 배포 (Reporting Services)에 대 한 솔루션 디자인 고려 사항](http://msdn.microsoft.com/en-us/55630eca-d1e5-4ac6-93c7-9a3f15c0d08a)  
  
  

