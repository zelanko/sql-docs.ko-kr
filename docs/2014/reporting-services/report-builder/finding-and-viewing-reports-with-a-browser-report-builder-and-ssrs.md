---
title: 브라우저를 사용하여 보고서 찾기 및 보기(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: edf4843a-2a0a-486f-be25-14a3c1c6bc72
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8813dba9c266c6a7930a636da27015c300426c79
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220093"
---
# <a name="finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs"></a>브라우저를 사용하여 보고서 찾기 및 보기(보고서 작성기 및 SSRS)
  지원되는 웹 브라우저에서 보고서 서버에 직접 연결하여 보고서를 볼 수 있습니다. 모든 보고서에는 보고서 서버에 대한 URL 주소가 있습니다. 보고서의 웹 주소를 입력하여 웹 응용 프로그램과는 상관없이 브라우저 창에 보고서를 열 수 있습니다. 보고서는 HTML 형식으로 열리고 페이지를 탐색하거나 보고서 내의 데이터 값을 검색하는 데 사용할 수 있는 보고서 도구 모음이 함께 표시됩니다. URL에 매개 변수를 설정하여 도구 모음을 숨기거나 보고서의 출력 형식을 선택할 수 있습니다.  
  
 해당 웹 주소를 통해 보고서를 여는 방법은 보고서를 보는 데 적합하지만 보고서를 관리하는 데는 적합하지 않습니다. 이 경우 항목의 속성 페이지나 구독 정의 페이지에 액세스할 수 없습니다. 이러한 태스크에는 보고서 관리자나 SharePoint 사이트를 사용해야 합니다.  
  
 보고서의 웹 주소를 모르는 경우 보고서 서버의 웹 주소를 연 다음 보고서 서버의 폴더 계층 구조를 탐색하여 원하는 보고서를 선택하고 표시할 수 있습니다. 다음 다이어그램에서는 브라우저 창에 표시되는 폴더 계층을 보여 줍니다.  
  
 ![브라우저의 폴더](../media/rs-browserfolder.GIF "브라우저의 폴더")  
브라우저의 폴더  
  
> [!NOTE]  
>  핸드헬드 디바이스에서 보고서에 액세스할 경우 브라우저를 사용하여 보고서를 열어야 합니다. 보고서 관리자는 핸드헬드 디바이스에서 사용할 수 없습니다.  
  
 사용할 수 있는 브라우저 종류에 대한 자세한 내용은 SQL Server 온라인 설명서의 [Reporting Services 설명서](http://go.microsoft.com/fwlink/?linkid=121312) 에 있는 "Reporting Services에서 지원하는 브라우저 종류(Browser Types Supported by Reporting Services)"를 참조하십시오.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="navigating-report-server-folders-in-a-web-browser"></a>웹 브라우저에서 보고서 서버 폴더 탐색  
 웹 브라우저를 사용하여 보고서 서버 폴더를 탐색하고 보고서를 실행할 수 있습니다. 보고서와 항목은 폴더 계층에서 링크로 표시됩니다. 링크를 클릭하여 보고서, 리소스 또는 폴더를 열거나 공유 데이터 원본의 내용을 볼 수 있습니다. 폴더 계층 탐색은 보고서의 URL을 모르는 경우에 유용합니다. 보고서 서버 웹 주소를 지정하여 폴더 계층 구조의 루트 노드에서 브라우저 연결을 연 다음 폴더 링크를 클릭하여 계층 구조를 탐색할 수 있습니다.  
  
 보고서 서버 가상 디렉터리에 액세스하면 사용자가 액세스할 수 있는 폴더, 보고서 및 업로드된 항목만 표시됩니다. 사용자 인터페이스에는 폴더 계층과 기본 정보만 표시됩니다. 기본 정보의 예에는 만든 날짜, 수정한 날짜, 파일 크기 및 개별 항목의 항목 유형이 있습니다.  
  
-   별도의 표시가 없는 링크는 보고서나 모델입니다.  
  
-   \<ds> 태그는 공유 데이터 원본을 나타냅니다.  
  
-   \<dir> 태그는 폴더 항목을 나타냅니다.  
  
-   파일 이름 확장명은 리소스를 나타냅니다. 파일 이름 확장명은 리소스의 MIME 형식을 나타냅니다. 예를 들어 .jpg는 JPEG 형식의 이미지를 나타냅니다.  
  
## <a name="typing-the-url-address-of-a-report"></a>보고서의 URL 주소 입력  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서는 보고서 서버의 특정 항목에 대한 URL 액세스를 지원합니다. 이 URL에는 보고서의 정규화된 경로와 보고서를 렌더링하기 위한 명령이 포함되어야 합니다. 보고서에 매개 변수가 포함되어 있으면 보고서를 여는 데 필요한 값도 모두 지정해야 합니다. 경로, 매개 변수 값 또는 렌더링 확장 프로그램에 공백이 포함된 보고서의 URL을 입력할 경우 원하는 결과를 얻으려면 URL 인코딩된 문자를 URL에 포함해야 합니다. 다음 예에서는 경로 이름, 매개 변수 및 렌더링 확장 프로그램에 공백에 대한 인코딩을 포함하는 보고서 URL을 보여 줍니다.  
  
 `http://<Webservername>/reportserver?/<reportfolder>/employee+sales+summary&ReportYear=2004&ReportMonth=06&EmpID=24&rs:Command=Render&rs:Format=HTML4.0`  
  
 Internet Explorer에서 URL에 사용할 수 있는 문자는 최대 2,083자까지입니다. 자세한 내용은 [Internet Explorer의 최대 URL 길이(Maximum URL length in Internet Explorer)](http://support.microsoft.com/kb/208427)를 참조하십시오.  
  
 URL을 통해 보고서에 액세스하는 방법은 SQL Server 온라인 설명서의 [Reporting Services 설명서](http://go.microsoft.com/fwlink/?linkid=121312) 에 있는 "URL 액세스(URL Access)"를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [찾기 및 보고서 관리자에서 보고서 보기 &#40;보고서 작성기 및 SSRS&#41;](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
  
  
