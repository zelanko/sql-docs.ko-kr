---
title: Reporting Services 보고서 렌더링 문제 해결 | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 1e0fb399-4c16-438a-92cb-db3e877896d0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 73b5fe3ae626076b6579671038c50ccc8cd87380
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43281938"
---
# <a name="troubleshoot-reporting-services-report-rendering-issues"></a>Reporting Services 보고서 렌더링 문제 해결
보고서 데이터와 레이아웃 정보가 조합되면 컴파일된 보고서가 보고서 렌더러로 전송됩니다. 예를 들어 보고서를 로컬로 미리 볼 때는 HTML 렌더러를 사용하여 컴파일된 보고서를 표시합니다. 이 항목을 사용하여 보고서 렌더링 관련 문제를 해결할 수 있습니다.   
  
## <a name="why-do-i-have-extra-white-space-including-blank-pages-in-my-report"></a>보고서에서 빈 페이지와 같은 추가 공백이 발생함  
보고서 항목은 보고서 처리 중에 보고서의 일부로 정의된 공백을 유지하도록 자동으로 조정됩니다. 보고서 디자인 뷰의 공백이 유지됩니다. 보고서 디자인 화면에서 흰색 배경은 보고서를 대상 매체에 따라 보거나, 내보내거나, 인쇄할 때 유지되는 공백을 나타냅니다.  
  
### <a name="white-space-and-page-breaks-interact-during-rendering"></a>렌더링 시 공백 및 페이지 나누기 상호 작용  
보고서를 보거나 파일 형식으로 내보낼 때 연결된 렌더링 확장 프로그램은 보고서를 처리하고 이를 지정된 파일 형식으로 저장합니다. 각 렌더링 확장 프로그램은 특정 규칙에 따라 보고서의 공백을 처리합니다. 공백은 페이지 설정 속성, 보고서 항목에 설정된 페이지 나누기, 보고서 본문에 배치된 보고서 항목의 상대적 위치, 특정 보고서 항목의 KeepTogether 속성 및 보고서 항목이 부모 컨테이너에 있는지 여부에도 영향을 받습니다.   
  
보고서 너비 때문에 추가 페이지를 없애려면 보고서 디자인 화면의 가장자리를 끌어 가장 바깥쪽 보고서 항목에 맞춰 정렬합니다. 왼쪽에서 오른쪽으로의 보고서 레이아웃의 경우 오른쪽 가장자리를 끌어 가장 바깥쪽 보고서 항목에 맞춰 정렬합니다. 자세한 내용은 [Rendering Behaviors](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="white-space-is-not-preserved-at-the-end-of-a-report"></a>보고서 끝에 있는 공백을 유지하지 않는 경우  
Reporting Services는 보고서 끝에 있는 공백을 유지할지, 제거할지를 제어할 수 있는 옵션을 제공합니다.   
  
보고서 끝에 있는 공백을 유지하려면 보고서를 선택하고 속성 창에서 ConsumeContainerWhitespace로 스크롤하고 False를 입력합니다.   
  
## <a name="why-do-my-reports-look-different-when-exported-to-different-formats"></a>보고서를 다른 형식으로 내보내면 모양이 달라짐  
보고서를 실행한 후 Excel, Word 또는 PDF와 같은 다른 형식으로 내보낼 수 있습니다. 보고서를 내보내는 형식에 따라 특정 규칙과 제한이 적용될 수 있습니다. 보고서를 만들 때 이러한 제한 사항을 고려하면 대부분의 문제를 해결할 수 있습니다. 보고서에서 약간 다른 레이아웃을 사용하거나, 보고서 내의 항목을 주의해서 맞추거나, 보고서 바닥글을 한 줄 텍스트로 제한하는 등의 작업이 필요할 수 있습니다. 기본 제공 전역 변수인 RenderFormat을 사용하면 조건에 따라 렌더러마다 각기 다른 보고서 레이아웃을 사용할 수도 있습니다. 다른 기본 제공 전역 변수를 사용하면 손쉽게 내보내는 형식의 페이지 매김을 관리하고 Excel에서 워크시트 탭의 이름을 지정할 수 있습니다. 자세한 내용은 [보고서 내보내기](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) 및 [기본 제공 Globals 및 Users 참조 사용](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)을 참조하세요.  
  
## <a name="how-can-i-view-all-my-report-data-on-one-page"></a>모든 보고서 데이터를 한 페이지에 표시하는 방법  
데이터 양이 많지 않은 보고서의 대화형 보기 환경을 위해 모든 데이터를 한 페이지에 표시할 수 있습니다.   
  
소프트 페이지 나누기 렌더러의 경우 모든 데이터를 한 페이지 표시하려면 보고서 속성에서 InteractiveHeight를 0으로 설정합니다. 이렇게 하면 소프트 페이지 나누기 렌더러에서 기존 페이지 나누기는 무시됩니다.   
  
> [!NOTE]  
> 보고서에 페이지 나누기가 없으면 사용자가 첫 번째 페이지를 보기 전에 전체 보고서를 처리해야 합니다.   
  
렌더러 범주에 대한 자세한 내용은 [렌더링 동작](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="reports-do-not-run-when-your-browser-is-configured-to-prompt-for-credentials"></a>자격 증명을 요청하도록 브라우저가 구성된 경우 보고서가 실행되지 않음  
자격 증명을 요청하도록 브라우저가 구성되어 있고 Windows 통합 인증을 사용하도록 데이터 원본이 구성된 경우 오류 메시지가 나타나면서 보고서를 볼 수 없을 수 있습니다. 데이터 원본이 보고서 서버와는 다른 컴퓨터에 있고 Windows 인증을 사용하도록 데이터 원본이 구성되어 있으며 자격 증명을 요청하도록 브라우저가 설정되어 있는 경우 이러한 문제가 발생합니다. 다음은 이러한 경우 나타나는 메시지의 예입니다.  
  
Microsoft SQL Server 연결 유형에 맞게 데이터 원본이 구성된 경우:  
`An error has occurred during report processing.`  
`Cannot create a connection to data source 'localhost'.`  
`Login failed for user '(null)'. Reason: Not associated with a trusted SQL Server connection.`  
  
Microsoft SharePoint 목록 연결 유형에 맞게 데이터 원본이 구성된 경우:  
`An error occurred during client rendering.`   
`An error has occurred during report processing.`   
`Query execution failed for dataset 'DataSet1'.`   
`The request failed with HTTP status 401: Unauthorized.`  
  
**이 문제를 해결하려면:** Windows 자격 증명 대신 저장된 자격 증명을 사용하도록 데이터 원본을 수정합니다.  
  
**이 문제는:** 자격 증명을 요청하도록 구성된 브라우저에 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
[오류 및 이벤트(Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Reporting Services 보고서의 데이터 검색 문제 해결](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services 구독 및 배달 문제 해결](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

