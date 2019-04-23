---
title: URL에 보고서 매개 변수 전달 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], passing parameters
- passing parameters [Reporting Services]
ms.assetid: f93a94cc-27b5-435a-aa85-69e6ec6459ad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f05aaedf8e3b8bb15d5d15d47823752832e659a5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59944139"
---
# <a name="pass-a-report-parameter-within-a-url"></a>URL에 보고서 매개 변수 전달
  보고서 매개 변수를 보고서 URL에 포함시켜 보고서에 전달할 수 있습니다. 이러한 URL 매개 변수는 보고서 처리 엔진에 직접 전달되기 때문에 접두사가 붙지 않습니다.  
  
> [!IMPORTANT]  
>  URL에는 SharePoint를 통해 요청을 라우팅하는 `_vti_bin` 프록시 구문과 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] HTTP 프록시를 포함하는 것이 중요합니다. 프록시는 몇 가지 컨텍스트를 HTTP 요청에 추가하며 이 컨텍스트는 SharePoint 모드 보고서 서버에 대한 보고서의 올바른 실행을 보장하는 데 필요합니다.  
>   
>  프록시 구문을 포함하지 않으면 접두사 *rp:* 로 매개 변수를 시작해야 합니다.  
  
 모든 쿼리 매개 변수에는 해당하는 보고서 매개 변수가 있을 수 있습니다. 해당 보고서 매개 변수를 전달하여 보고서에 쿼리 매개 변수를 전달할 수 있습니다. 자세한 내용은 [관계형 쿼리 디자이너에서 쿼리 빌드&#40;보고서 작성기 및 SSRS&#41;](report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!IMPORTANT]
>  보고서 매개 변수는 대/소문자를 구분합니다.  
> 
> [!NOTE]
>  보고서 매개 변수는 대/소문자를 구분하고 다음과 같은 특수 문자를 사용합니다.  
> 
>  -   URL 문자열에서 공백 문자는 URL 인코딩 표준에 따라 "%20" 문자로 바뀝니다.  
> -   URL의 매개 변수 부분에서 공백 문자는 더하기 문자(+)로 대체됩니다.  
> -   문자열의 모든 부분에서 세미콜론은 "%3A" 문자로 바뀝니다.  
> -   브라우저에서 적절한 URL 인코딩을 자동으로 수행하며 문자를 수동으로 인코딩할 필요는 없습니다.  
  
 URL에 보고서 매개 변수를 설정하려면 다음 구문을 사용 합니다.  
  
```  
  
parameter=value  
```  
  
 예를 들어 보고서에 정의된 두 개의 매개 변수 "ReportMonth" 및 "ReportYear"를 지정하려면 기본 모드 보고서 서버에 다음 URL을 사용합니다.  
  
```  
http://myrshost/ReportServer?/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2&ReportMonth=3&ReportYear=2008  
```  
  
 예를 들어 보고서에 정의된 두 개의 같은 매개 변수를 지정하려면 SharePoint 통합 모드 보고서 서버에 다음 URL을 사용합니다. `/_vti_bin`을 참고하세요.  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl&ReportMonth=3&ReportYear=2008  
```  
  
 매개 변수에 대해 null 값을 전달하려면 다음 구문을 사용합니다.  
  
```  
  
parameter  
:isnull=true  
  
```  
  
 예:  
  
```  
SalesOrderNumber:isnull=true  
```  
  
 `Boolean` 값을 전달하려면 False에 0을 사용하고 True에 1을 사용합니다. `Float` 값을 전달하려면 서버 로캘의 소수 구분 기호를 포함합니다.  
  
> [!NOTE]  
>  보고서에 기본값을 가진 보고서 매개 변수가 포함되어 있고 `Prompt` 속성의 값이 `false`이면(즉, 보고서 관리자에서 사용자에게 확인 속성이 선택되지 않음) URL 내에서 해당 보고서 매개 변수에 대한 값을 전달할 수 없습니다. 이러한 기능을 통해 관리자는 최종 사용자가 특정 보고서 매개 변수의 값을 추가하거나 수정하지 못하도록 설정할 수 있습니다.  
  
##  <a name="bkmk_examples"></a> 추가 예  
 다음 URL 예제에는 공백 및 여러 매개 변수가 포함됩니다.  
  
-   "SQL Server 사용자 교육 팀" 폴더 이름에는 공백이 포함되므로 "+"가 공백을 각각 대체합니다.  
  
-   "팀 프로젝트 보고서" 보고서 이름에는 공백이 포함되므로 "+"가 공백을 각각 대체합니다.  
  
-   두 개의 매개 변수 "teamgrouping2" 및 "teamgrouping1"에 값 "xgroup" 및 "ygroup"을 전달합니다.  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup  
```  
  
 다음 URL 예제에는 다중 값 매개 변수 "OrderID"를 포함합니다. 다중 값 매개 변수의 형식은 각 값에 대해 매개 변수 이름을 반복합니다.  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup&OrderID=747&OrderID=787&OrderID=12  
```  
  
 다음 URL 예제는 기본 모드 보고서 서버에 대해 "7/1/2005" 값이 포함된 *SellStartDate*의 단일 매개 변수를 전달합니다.  
  
```  
http://myserver/ReportServer/Pages/ReportViewer.aspx?%2fProduct_and_Sales_Report_AdventureWorks&SellStartDate=7/1/2005  
```  
  
## <a name="see-also"></a>관련 항목  
 [URL 액세스&#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 액세스 매개 변수 참조](url-access-parameter-reference.md)  
  
  
