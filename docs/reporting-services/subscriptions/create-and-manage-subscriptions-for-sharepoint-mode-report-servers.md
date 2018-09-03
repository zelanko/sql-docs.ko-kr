---
title: SharePoint 모드 보고서 서버에 구독 만들기 및 관리 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], creating
- subscriptions [Reporting Services], deleting
- subscriptions [Reporting Services], managing
ms.assetid: 44be7ee2-33ce-46e4-9d1a-a20aaf43a227
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8f3f3534e61339bbf9b27a157352e27ebfa807b0
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43270050"
---
# <a name="create-and-manage-subscriptions-for-sharepoint-mode-report-servers"></a>SharePoint 모드 보고서 서버 구독 만들기 및 관리
  SharePoint 모드 보고서 서버와 통합된 SharePoint 웹 응용 프로그램에서 보고서를 배달하는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독을 만들 수 있습니다. 구독은 보고서를 문서 라이브러리, 파일 폴더 또는 전자 메일로 배달할 수 있습니다. 이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독을 만들기 위한 요구 사항 및 단계를 요약합니다.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 &#124; SharePoint 2010 및 SharePoint 2013|  
  
 구독을 만들 때 3가지 방법으로 구독 배달 방식을 지정할 수 있습니다.  
  
-   **문서 라이브러리**: 원래 보고서 기반의 문서를 원래 보고서와 같은 SharePoint 사이트 내의 라이브러리로 배달하는 구독을 만들 수 있습니다. 다른 서버 또는 동일한 사이트 모음 내 다른 사이트의 라이브러리로는 문서를 배달할 수 없습니다. 문서를 배달하려면 보고서가 배달되는 라이브러리에 대한 항목 추가 권한이 있어야 합니다.  
  
-   **파일 폴더:** 원래 보고서 기반의 문서를 파일 시스템의 공유 폴더로 배달할 수 있습니다. 이때 네트워크 연결을 통해 액세스할 수 있는 기존 폴더를 선택해야 합니다.  
  
-   **메일:** 보고서 서버 메일 배달 확장 프로그램을 사용하도록 보고서 서버가 구성되어 있는 경우 보고서 또는 내보낸 보고서 파일(출력 형식으로 저장됨)을 받은 편지함으로 보내는 구독을 만들 수 있습니다. 보고서 또는 보고서 URL 없이 알림만 받으려면 **보고서에 대한 링크 포함** 및 **메시지 내에 보고서 표시** 확인란의 선택을 취소합니다.  
  
 **항목 내용**  
  
-   [구독에 대한 일반 요구 사항](#bkmk_subscription_requirements)  
  
-   [SharePoint 라이브러리로 보고서를 배달할 구독을 만들려면](#bkmk_tosharepoint_library)  
  
-   [SharePoint 라이브러리로 보고서를 배달할 구독을 만들려면](#bkmk_tosharepoint_library)  
  
-   [보고서 서버 전자 메일 배달을 위한 구독을 만들려면](#bkmk_subscription_for_email)  
  
-   [구독을 보거나 수정하려면](#bkmk_to_modify_subscription)  
  
-   [구독을 삭제하려면](#bkmk_to_delete_subscription)  
  
##  <a name="bkmk_subscription_requirements"></a> 구독에 대한 일반 요구 사항  
 구독을 만들려면 보고서가 저장된 자격 증명을 사용해야 하며 사용자에게 보고서를 보고 경고를 만들 수 있는 권한이 있어야 합니다.  
  
 구독을 만들 때는 출력 파일 형식을 선택할 수 있습니다. 보고서가 모든 형식에서 다 잘 작동하는 것은 아닙니다. 구독 형식을 선택하기 전에 보고서를 열고 다른 형식으로 내보내 해당 보고서가 예상대로 표시되는지 확인하세요.  
  
 **구독을 만들 수 있으려면 사용자에게 SharePoint의** 항목 편집 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 목록 권한이 필요합니다. 자세한 내용은 [보고서 서버 항목에 대한 SharePoint 사이트 및 목록 사용 권한 참조](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  보고서를 라이브러리나 공유 폴더로 배달하는 구독은 원래 보고서를 기반으로 하는 새 정적 파일을 만들지만 이는 보고서 뷰어 웹 파트에서 실행되는 진정한 보고서 정의가 아닙니다. 원래 보고서에 드릴스루 링크와 같은 대화형 기능이나 동적 콘텐츠가 있는 경우 이러한 기능은 대상 위치로 배달되는 정적 파일에서 사용할 수 없게 됩니다. "웹 페이지"를 선택하는 경우 일부 대화형 작업을 유지할 수 있지만 문서가 보고서 뷰어에서 실행하는 .rdl 파일이 아니므로 보고서를 클릭 광고하면 사이트로 돌아가기 위해 스크롤해야 할 브라우저 세션에 새 페이지가 생성됩니다.  
  
 내보낸 보고서의 파일 확장명을 .rdl로 바꿀 수 없으며 해당 보고서를 보고서 뷰어 웹 파트에서 실행할 수 없습니다. 실제 보고서를 제공하는 구독을 만들려면 보고서 서버 전자 메일 배달 확장 프로그램을 사용하고 보고서에 대한 링크를 포함하는 옵션을 설정합니다.  
  
 배달된 문서가 들어 있는 라이브러리의 버전 설정에 따라 각 배달 시 문서의 새 버전을 만들지 여부가 결정됩니다. 기본적으로 각 라이브러리에서 버전 설정이 사용됩니다. 구체적으로 **버전 관리 안 함**을 선택하지 않으면 배달 시 문서의 새 주 버전이 생성됩니다. 문서의 주 버전만 생성되며, 부 버전을 허용하는 버전 관리 옵션을 선택해도 부 버전은 구독 배달의 결과로 생성되지 않습니다. 유지되는 주 버전 번호를 제한하면 최대 제한에 도달할 경우 이전 배달이 새 배달로 바뀝니다.  
  
 구독에 대해 선택할 수 있는 출력 형식은 보고서 서버에 설치된 렌더링 확장 프로그램에 따라 달라집니다. 즉, 보고서 서버의 렌더링 확장 프로그램에서 지원하는 출력 형식만 선택할 수 있습니다.  
  
###  <a name="bkmk_tosharepoint_library"></a> SharePoint 라이브러리로 보고서를 배달할 구독을 만들려면  
  
1.  보고서가 포함된 SharePoint 라이브러리를 찾습니다.  
  
2.  보고서 옆의 아래쪽 화살표를 클릭한 후 **구독 관리**를 선택합니다.  
  
3.  **구독 추가**를 클릭합니다.  
  
4.  **배달 확장 프로그램**에서 **SharePoint 문서 라이브러리**를 선택합니다.  
  
5.  **문서 라이브러리**에서 동일한 사이트 내의 라이브러리를 선택합니다.  
  
6.  **파일 옵션**에서 구독으로 만들 문서의 파일 이름과 제목을 지정합니다.  
  
7.  **출력 형식**에서 응용 프로그램 형식을 선택합니다.  
  
     MHTML(웹 보관 파일)은 자체 포함된 HTML 파일을 생성하므로 기본값이지만 원래 보고서에 있을 수 있는 대화형 보고서 기능을 유지하지 않습니다.  
  
8.  **덮어쓰기 옵션**에서 이후 배달 시 파일을 덮어쓸지 여부를 결정하는 옵션을 지정합니다. 이전 배달을 유지하려면 **고유 이름으로 파일 만들기**를 선택합니다. 그러면 새 파일에 번호가 추가되어 고유한 파일 이름이 생성됩니다.  
  
9. **배달 이벤트**에서 구독이 실행되도록 하는 일정이나 이벤트를 지정합니다. 사용자 지정 일정을 만들거나, 사용 가능한 경우 공유 일정을 선택하거나, 스냅숏 데이터를 사용하여 실행되는 보고서에 대해 데이터가 새로 고쳐질 때마다 구독을 실행할 수 있습니다. 일정 및 데이터 처리에 대한 자세한 내용은 [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)를 참조하세요.  
  
10. 매개 변수가 있는 보고서에 대한 구독을 만드는 경우 **매개 변수**에서 구독 처리 시 보고서에 사용할 값을 지정합니다. 선택한 보고서에 매개 변수가 없는 경우 매개 변수 섹션이 이 페이지에 표시되지 않습니다. 매개 변수에 대한 자세한 내용은 [게시된 보고서에 매개 변수 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)을 참조하세요.  
  
###  <a name="bkmk_subscription_for_sharedfolder"></a> 공유 폴더 배달을 위한 구독을 만들려면  
  
1.  보고서가 포함된 SharePoint 라이브러리를 찾습니다.  
  
2.  보고서 옆의 아래쪽 화살표를 클릭한 후 **구독 관리**를 선택합니다.  
  
3.  **구독 추가**를 클릭합니다.  
  
4.  **배달 확장 프로그램**에서 **Windows 파일 공유**를 선택합니다.  
  
5.  **파일 이름**에 공유 폴더에서 만들 파일의 이름을 입력합니다.  
  
6.  **경로**에 컴퓨터의 네트워크 이름을 포함하는 UNC(Uniform Naming Convention) 형식으로 폴더 경로를 입력합니다. 이때 폴더 경로에 후행 백슬래시를 포함하지 마세요. 예를 들어 경로는 `\\ComputerName01\Public\MyReports`가 될 수 있습니다. 여기서 Public 및 MyReports는 공유 폴더입니다.  
  
7.  **렌더링 형식**에서 보고서의 응용 프로그램 형식을 선택합니다.  
  
8.  **쓰기 모드**에서 **없음**, **자동 증가**, **덮어쓰기**중 하나를 선택합니다. 이러한 옵션은 이후 배달 시 파일을 덮어쓸지 여부를 결정합니다. 이전 배달을 유지하려면 **자동 증가**를 선택합니다. 그러면 새 파일에 번호가 추가되어 고유한 파일 이름이 생성됩니다. **없음**을 선택하면 동일한 이름의 파일이 대상 위치에 있는 경우 배달되지 않습니다.  
  
9. **파일 확장명**에서 응용 프로그램 파일 형식에 해당하는 파일 확장명을 추가하려면 **True** 를 선택하고 확장명 없이 파일을 만들려면 False를 선택합니다.  
  
10. **사용자 이름** 및 **암호**에 공유 폴더에 대한 쓰기 권한이 있는 자격 증명을 입력합니다.  
  
11. **배달 이벤트**에서 구독이 실행되도록 하는 일정이나 이벤트를 지정합니다. 사용자 지정 일정을 만들거나, 사용 가능한 경우 공유 일정을 선택하거나, 스냅숏 데이터를 사용하여 실행되는 보고서에 대해 데이터가 새로 고쳐질 때마다 구독을 실행할 수 있습니다. 일정 및 데이터 처리에 대한 자세한 내용은 [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)를 참조하세요.  
  
12. 매개 변수가 있는 보고서에 대한 구독을 만드는 경우 **매개 변수**에서 구독 처리 시 보고서에 사용할 값을 지정합니다. 매개 변수에 대한 자세한 내용은 [게시된 보고서에 매개 변수 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)을 참조하세요.  
  
###  <a name="bkmk_subscription_for_email"></a> 보고서 서버 전자 메일 배달을 위한 구독을 만들려면  
  
1.  보고서가 포함된 SharePoint 라이브러리를 찾습니다.  
  
2.  보고서 옆의 아래쪽 화살표를 클릭한 후 **구독 관리**를 선택합니다.  
  
3.  **구독 추가**를 클릭합니다.  
  
4.  **배달 확장 프로그램**에서 **메일**을 선택합니다.  
  
5.  **배달 옵션**에서 보고서를 보낼 메일 주소를 지정합니다.  
  
6.  필요에 따라 제목 줄을 수정할 수 있습니다. 제목 줄은 보고서 이름과 보고서가 처리된 시간을 캡처하는 기본 제공 매개 변수를 사용합니다. 사용할 수 있는 기본 제공 매개 변수는 이 두 가지뿐입니다. 매개 변수는 제목 줄에 나타나는 텍스트를 사용자 지정하는 자리 표시자이지만 이를 정적 텍스트로 바꿀 수 있습니다.  
  
7.  보고서 URL을 메시지 본문에 포함하려면 **이 보고서에 대한 링크 포함** 을 선택합니다.  
  
8.  **보고서 내용**에서 실제 보고서를 메시지 본문에 포함할지 여부를 지정합니다.  
  
     렌더링 형식과 브라우저에 따라 보고서가 포함될지 또는 첨부될지가 결정됩니다. 브라우저에서 HTML 4.0 및 MHTML을 지원하고 웹 보관 파일 렌더링 형식을 선택한 경우 보고서는 메시지의 일부로 포함됩니다. CSV, PDF를 비롯한 다른 렌더링 형식은 모두 보고서를 첨부 파일로 배달합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서를 보내기 전에 첨부 파일 또는 메시지의 크기를 확인하지 않습니다. 첨부 파일 또는 메시지가 메일 서버에서 허용하는 최대 제한을 초과할 경우 보고서가 배달되지 않습니다. 큰 보고서의 경우 URL이나 알림과 같은 다른 배달 옵션 중 하나를 선택하십시오.  
  
9. **배달 이벤트**에서 구독이 실행되도록 하는 일정이나 이벤트를 지정합니다. 사용자 지정 일정을 만들거나, 사용 가능한 경우 공유 일정을 선택하거나, 스냅숏 데이터를 사용하여 실행되는 보고서에 대해 데이터가 새로 고쳐질 때마다 구독을 실행할 수 있습니다. 일정 및 데이터 처리에 대한 자세한 내용은 [처리 옵션 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)를 참조하세요.  
  
10. 매개 변수가 있는 보고서에 대한 구독을 만드는 경우 **매개 변수**에서 구독 처리 시 보고서에 사용할 값을 지정합니다. 매개 변수에 대한 자세한 내용은 [게시된 보고서에 매개 변수 설정&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)을 참조하세요.  
  
###  <a name="bkmk_to_modify_subscription"></a> 구독을 보거나 수정하려면  
  
1.  보고서가 포함된 SharePoint 라이브러리를 찾습니다.  
  
2.  보고서 옆의 아래쪽 화살표를 클릭한 후 **구독 관리**를 클릭합니다.  
  
3.  각 구독은 배달 유형으로 식별됩니다. 구독 유형을 클릭하여 기존 속성을 보고 변경합니다.  
  
###  <a name="bkmk_to_delete_subscription"></a> 구독을 삭제하려면  
  
1.  보고서가 포함된 SharePoint 라이브러리를 찾습니다.  
  
2.  보고서 옆의 아래쪽 화살표를 클릭한 후 **구독 관리**를 클릭합니다.  
  
3.  구독 옆에 있는 확인란을 클릭하고 **삭제**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services의 전자 메일 배달](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)   
 [Reporting Services의 파일 공유 배달](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [Reporting Services의 SharePoint 라이브러리 배달](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md)   
 [이메일 전송을 위한 보고서 서버 구성(SSRS 구성 관리자)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)  
  
  
