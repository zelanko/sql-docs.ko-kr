---
title: 기본 모드 보고서 서버에서 보고서 게시 또는 보기 문제 해결 | Microsoft Docs
ms.date: 02/28/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: df7720a1-d178-45bb-8d6f-63e208cae7fe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d89b4156225de984854076f8218c29f033e4a0d3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653041"
---
# <a name="troubleshoot-publishing-or-viewing-a-report-on-a-native-mode-report-server"></a>기본 모드 보고서 서버에서 보고서 게시 또는 보기 문제 해결
  
  
  
기본 모드로 구성된 보고서 서버에 보고서를 게시하거나 업로드하면 보고서 서버에 표시된 보고서와 관련된 문제가 발생할 수 있습니다. 이 항목에서는 이러한 문제를 해결하는 데 유용한 정보를 제공합니다.   
  
## <a name="why-am-i-being-prompted-for-credentials-when-i-publish-a-report"></a>보고서를 게시할 때 자격 증명을 입력하라는 메시지가 표시되는 이유  
보고서를 보고서 서버에 배포하려면 서버의 주소를 지정해야 합니다. 자격 증명 정보를 입력하라는 Reporting Services 로그인 대화 상자가 표시될 수 있습니다.   
  
보고서 서버 이름이 올바르게 지정되지 않은 경우  
  
  
기본 모드의 보고서 서버에 보고서를 배포할 때 일반적으로 발생하는 오류는 보고서 서버 이름 대신 보고서 폴더 이름을 지정하는 것입니다.   
  
보고서 서버 URL이 보고서 관리자의 가상 디렉터리 주소(예: `http://localhost/reportserver`)가 아닌 보고서 서버의 주소(예: `http://localhost/reports`)인지 확인하십시오. 보고서 서버에 대해 기본 포트 번호인 80이 아닌 다른 포트 번호를 지정한 경우 보고서 서버 주소에서 이를 지정해야 합니다(예: `http://localhost:81/reportserver`).   
  
 ## <a name="nothing-happens-when-i-toggle-items-in-my-published-report"></a>게시된 보고서에서 항목을 전환할 때 아무 작업도 수행되지 않는 경우  
  로컬 미리 보기에서 보고서를 표시할 때 보고서의 항목을 전환하여 표시하거나 숨길 수 있습니다. 동일한 보고서를 보고서 서버에 게시한 후 볼 때는 항목을 전환해도 아무 작업도 수행되지 않습니다.   
  
\<보고서 서버 이름> 밑줄(_)이 포함된 경우  
  
보고서가 오류 없이 실행되었으나 토글 항목이 작동하지 않으면(예: 확장 아이콘(+)을 클릭해도 동작이 발생하지 않는 경우) 보고서 서버를 호스팅하는 컴퓨터의 이름을 확인합니다. 컴퓨터 이름에 밑줄이 있으면 토글 항목이 작동하지 않습니다. 이것은 알려진 문제이며 해결 방법이 없습니다.   
  
토글 항목을 포함하는 보고서를 실행하려면 이름에 밑줄 문자가 없는 컴퓨터를 사용해야 합니다.  
  
## <a name="images-and-charts-do-not-load-when-i-use-run-as-and-a-browser-to-run-my-report"></a>Run As 명령을 사용하거나 브라우저를 통해 보고서를 실행하면 이미지 및 차트가 로드되지 않는 경우  
다른 보안 컨텍스트에서 보고서 관리자를 실행할 때는 보고서의 일부 보고서 항목이 표시되지 않을 수 있습니다.   
  
### <a name="insufficient-permissions-on-internet-temporary-file-folders"></a>인터넷 임시 파일 폴더에 대한 사용 권한이 부족한 경우  
  
일부 경우에는 보고서 관리자를 사용하여 차트 또는 이미지를 포함하는 게시된 보고서를 볼 때 차트 또는 이미지가 표시되지 않을 수 있습니다. 예를 들어 Microsoft Windows **다음 계정으로 실행** 명령을 사용하여 다른 보안 컨텍스트를 사용하는 보고서를 보려고 할 때 사용자에게 보고서 서버가 차트 및 이미지를 임시 인터넷 파일로 캐시하는 폴더에 대한 사용 권한이 없을 수 있습니다.   
  
캐시된 파일이 포함된 폴더에 대한 액세스 권한이 있는지 확인하십시오.   
    
## <a name="see-also"></a>참고 항목  
[Reporting Services 및 파워 뷰 브라우저 지원](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[오류 및 이벤트(Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Reporting Services 보고서의 데이터 검색 문제 해결](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services 구독 및 배달 문제 해결](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

