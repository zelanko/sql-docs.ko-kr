---
title: 기본 모드 보고서 서버 구독 만들기 및 관리 | Microsoft Docs
ms.date: 05/28/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5bcfeabda2eda62a6a4118ac5542e83a4b0afd66
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76971311"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>기본 모드 보고서 서버 구독 만들기 및 관리
  표준 구독은 전자 메일을 통해 또는 공유 폴더로 보고서를 배달하려는 개인이 만든 구독입니다. 이 항목에서는 개별 사용자가 만들고 관리하는 표준 구독에 대한 정보를 제공합니다. 데이터 기반 구독의 경우 다른 요구 사항과 단계가 필요하며 이에 대해서는 별도의 항목에 설명되어 있습니다. 자세한 내용은 [데이터 기반 구독 만들기, 수정 및 삭제](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)를 참조하세요.  
  
 **문서 내용:**  
  
-   [구독에 대한 일반 요구 사항](#bkmk_create_subscription)  
  
-   [파일 공유 구독을 만들려면](#bkmk_create_fileshare_subscription)  
  
-   [메일 구독을 만들려면](#bkmk_create_email_subscription)  
  
-   [구독을 수정하려면](#bkmk_modify_subscription)  
  
-   [구독을 삭제하려면](#bkmk_delete_subscription)  
  
##  <a name="general-requirements-for-subscriptions"></a><a name="bkmk_create_subscription"></a> 구독에 대한 일반 요구 사항  
 이 문서에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 웹 포털을 사용하여 기본 모드 보고서 서버에서 구독을 만드는 방법에 대해 설명합니다. 구독을 정의한 후에는 웹 포털의 내 구독 페이지 또는 특정 보고서의 **구독** 탭을 통해 구독에 액세스할 수 있습니다.  
  
 [SharePoint 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) 에서는 SharePoint 사이트에서 애플리케이션 페이지를 사용하여 SharePoint 모드 보고서 서버의 보고서를 구독하는 방법을 설명합니다.  
  
-   전자 메일 배달을 사용하려면 구독을 만들기 전에 SMTP 서버 또는 게이트웨이 연결에 대해 보고서 서버를 구성해야 합니다. 자세한 내용은 [Reporting Services의 전자 메일 배달](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)을 참조하세요.  
  
-   파일 공유 배달을 이용하려면 먼저 대상 폴더를 정의해야 합니다. 자세한 내용은 [구독 설정 및 파일 공유 계정(Configuration Manager)](../install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)을 참조하세요.  
  
 보고서를 구독하려면 먼저 저장된 자격 증명을 사용하거나 자격 증명을 사용하지 않도록 보고서 데이터 원본을 구성해야 합니다. 자세한 내용은 [Reporting Services 데이터 원본에 자격 증명 저장](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)을 참조하세요. 그렇지 않으면 **새 구독** 단추를 사용할 수 없습니다.  
  
 이 문서에서는 데이터 기반 구독을 만드는 방법에 대해 설명하지 않습니다. 데이터 기반 구독을 만드는 방법에 대한 지침은 [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)를 참조하세요.  
  
## <a name="to-create-a-file-share-subscription"></a><a name="bkmk_create_fileshare_subscription"></a> 파일 공유 구독을 만들려면  
  
1. [보고서 서버의 웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)을 찾습니다.  
  
2.  원하는 보고서로 이동합니다. 보고서를 마우스 오른쪽 단추로 클릭하고 **구독**을 선택합니다.  
  
3.  **설명**: 보고서 구독에 대한 설명을 최대 512자로 입력합니다.  
  
4.  **소유자**: 소유자 필드는 기본적으로 현재 사용자로 채워지며 구독을 만들 때 편집할 수 없습니다. 하지만 구독을 저장한 이후 소유자와 설명을 포함한 구독 속성을 변경할 수 있습니다.  

5. **구독 유형** 아래에서 **표준 구독** 라디오 단추를 선택합니다.

6. **일정** 섹션 아래에서 다음 중 하나를 선택합니다.  
   - **공유 일정**  
   - **보고서별 일정**.  

    일정 예약에 대한 자세한 내용은 [일정](../../reporting-services/subscriptions/schedules.md)을 참조하세요.
  
7. **대상** 아래에서 **Windows 파일 공유**를 선택합니다.  
  
8. **배달 옵션(Windows 파일 공유)** 아래에서 다음을 지정합니다.  
   - **파일 이름**: 보고서의 파일 이름을 입력합니다.
   - **파일을 만들 때 파일 확장명 추가**: 이 옵션은 파일 이름에 3자로 된 파일 확장명을 추가합니다. 파일 확장명은 선택하는 보고서 출력 형식에 따라 결정됩니다.  
   - **경로**: 보고서를 배달할 기존 폴더에 대한 UNC(범용 명명 규칙) 경로를 입력합니다(예: \\<servername\>\<myreports>). 경로의 시작 부분에는 백슬래시 문자를 두 번 넣고 뒷부분에는 백슬래시를 지정하지 마세요.  
  
     ![파일 공유 구독](../../reporting-services/subscriptions/media/create-and-manage-subscriptions-for-native-mode-report-servers/subscription-file-share-delivery-option.png "파일 공유 구독")  
  
   - **렌더링 형식**: 파일 배달에 대한 보고서 출력 형식을 선택합니다. 보고서를 열 때 사용할 데스크톱 애플리케이션에 맞는 형식을 선택합니다. 보고서를 단일 스트림으로 렌더링하지 않거나 정적 파일(예: HTML 4.0)에서 지원될 수 없는 대화형 작업을 발생시키는 형식은 사용하지 마세요.  
  
   - **자격 증명**: 파일 공유 계정과 특정 Windows 사용자 자격 증명 중 사용할 자격 증명을 선택합니다. 보고서 관리자가 파일 공유 계정을 구성하지 않은 경우 **파일 공유 계정 사용** 이 비활성화됩니다. 자세한 내용은 [구독 설정 및 파일 공유 계정&#40;연결 관리자&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)을 참조하세요. **사용자 이름** 및 **암호** 입력란에서 파일 공유에 액세스하는 데 필요한 자격 증명을 지정합니다. 사용자 이름에는 *\<domain>* \\ *\<user name>* 형식을 사용합니다.  
  
   - **덮어쓰기 옵션**:  
     - **기존 파일을 최신 버전으로 덮어쓰기**  
     - **이전 버전이 있으면 파일을 덮어쓰지 않음**에서는 기존 파일이 검색될 경우 배달이 수행되지 않습니다.  
     - **새 버전 추가 시 파일 이름 자동 증가**에서는 보고서 서버가 이름이 같은 기존 파일과 구분할 수 있도록 파일 이름에 번호를 추가합니다.  

9. 매개 변수가 있는 보고서의 경우 이 구독에 대한 보고서에 사용할 매개 변수를 지정합니다. 이 매개 변수는 요청 시 실행 보고서나 다른 예약된 보고서를 실행하는 데 사용하는 매개 변수와 다를 수 있습니다.  
  
보고서는 정적 파일로 배달됩니다. 보고서에 대화형 기능(예: 추가 행과 열에 대한 링크)이 있는 경우 해당 기능은 사용할 수 없습니다.  
  
##  <a name="to-create-an-e-mail-subscription"></a><a name="bkmk_create_email_subscription"></a> 메일 구독을 만들려면  
  
1. [보고서 서버의 웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)을 찾습니다.  
  
2. 원하는 보고서로 이동합니다. 보고서를 마우스 오른쪽 단추로 클릭하고 **구독**을 선택합니다.  
  
3. **설명**: 보고서 구독에 대한 설명을 최대 512자로 입력합니다.  
  
4.  **소유자**: 소유자 필드는 기본적으로 현재 사용자로 채워지며 구독을 만들 때 편집할 수 없습니다. 하지만 구독을 저장한 이후 소유자와 설명을 포함한 구독 속성을 변경할 수 있습니다.  

5. **구독 유형** 아래에서 **표준 구독** 라디오 단추를 선택합니다.

6. **일정** 섹션 아래에서 다음 중 하나를 선택합니다.  
   - **공유 일정**  
   - **보고서별 일정**.  

    일정 예약에 대한 자세한 내용은 [일정](../../reporting-services/subscriptions/schedules.md)을 참조하세요.
  
7. **대상** 아래에서 **메일**을 선택합니다.  **메일** 옵션을 사용할 수 없는 경우 보고서 서버가 메일 구독에 대해 구성되지 않은 것입니다. [Reporting Services 서비스 애플리케이션에 대한 메일 구성](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)을 참조하세요.
  
8. **배달 옵션(메일)** 아래에서 다음을 지정합니다.
   - **받는 사람**: 받는 사람: 필드의 수신자 이름은 도메인 사용자 계정을 사용하여 자동으로 지정됩니다. 형식이 [user name]@[domain.com]인지 확인합니다. 보고서 서버 구성 설정에 따라 **받는 사람** 필드가 사용자 계정을 사용하여 자동으로 지정되는지 여부가 결정됩니다. 구성 설정 메일 주소를 변경하는 방법에 대한 자세한 내용은 [Reporting Services 애플리케이션에 대한 메일 구성](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)을 참조하세요.

     >[!NOTE]  
     > 사용 권한에 따라 보고서를 배달할 전자 메일 주소를 입력할 수 있습니다. 전자 메일 주소를 여러 개 지정하려면 세미콜론(;)으로 구분합니다. **참조**, **숨은 참조**및 **회신** 입력란에 메일 주소를 추가로 입력할 수도 있습니다. 이 작업을 수행하려면 모든 구독을 관리할 수 있는 권한이 있어야 합니다.  
  
   - **제목**: "@ReportName은 @ExecutionTime에서 실행됩니다."가 기본값입니다. 제목을 편집할 수는 있지만 @ReportName 및 @ExecutionTime은 **주체** 필드에 지원되는 유일한 전역 변수입니다.  
  
     ![전자 메일 구독](../../reporting-services/subscriptions/media/create-and-manage-subscriptions-for-native-mode-report-servers/subscription-e-mail-delivery-option.png "전자 메일 구독")  

   - **보고서 포함**: 보고서의 복사본을 포함하거나 첨부하려면 이 옵션을 선택합니다. 보고서 형식은 선택하는 렌더링 형식에 따라 결정됩니다. 보고서 크기가 전자 메일 시스템에 정의된 크기를 넘을 경우에는 이 옵션을 선택하지 마세요.  
  
   - **링크 포함**: 메일 메시지 본문에 보고서에 대한 URL 링크를 포함하려면 이 옵션을 선택합니다.  
  
     >[!NOTE]  
     >이러한 옵션을 선택하지 않으면 제목 줄의 알림 텍스트만 전송됩니다.  
  
   - **렌더링 형식** 목록 상자에서 렌더링 형식을 선택합니다. 이 옵션은 **보고서 포함** 을 선택하여 보고서 복사본을 포함시키거나 첨부한 경우에만 사용할 수 있습니다.  
      - 메일 메시지 본문에 보고서를 포함하려면 **MHTML(웹 보관 파일)** 을 선택합니다.  
      - 보고서를 첨부 파일로 전송하려면 다른 렌더링 형식을 선택합니다.  
  
   - **중요도** 목록 상자에서 중요도를 선택합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange에서는 이 설정에 따라 메일 메시지의 중요도 수준 플래그가 설정됩니다.  
   - 원할 경우 **설명**을 입력합니다.
  
9. 매개 변수가 있는 보고서의 경우 이 구독에 대한 보고서에 사용할 매개 변수를 지정합니다. 사용자가 지정한 매개 변수는 요청 시 실행 보고서나 다른 일정이 예약된 보고서를 실행하는 데 사용하는 매개 변수와 다를 수 있습니다.  
  
##  <a name="to-modify-a-subscription"></a><a name="bkmk_modify_subscription"></a> 구독을 수정하려면  
 언제든지 구독을 수정할 수 있습니다. 처리 중인 구독을 수정한 경우 배달 확장 프로그램에서 구독 데이터를 받기 전에 구독이 보고서 서버에 저장되면 업데이트된 설정이 사용됩니다. 그렇지 않으면 기존 설정이 사용됩니다.  
  
 구독을 만드는 사용자가 해당 구독을 소유합니다. 각 사용자는 자신이 소유한 구독을 수정하거나 삭제할 수 있습니다. 구독 속성 페이지에서 보고서 소유자를 변경하거나 소유권을 프로그래밍 방식으로 변경할 수 있습니다. 자세한 내용은  
  
-   [PowerShell을 사용하여 Reporting Services 구독 소유자 변경, 나열 및 구독 실행](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 구독을 찾으려면 **내 구독** 페이지를 사용하거나 보고서와 관련된 구독 정의를 확인합니다. 구독을 직접 검색하거나 소유자 이름, 트리거 정보, 상태 정보 등을 기반으로 구독을 검색할 수 없습니다.  
  
 보고서 서버 관리자도 구독을 수정하거나 삭제할 수 있습니다.  
  
>[!NOTE]  
> 보고서 서버 관리자라 하더라도 지정된 보고서 서버에서 사용 중인 각각의 구독을 한 장소에서 모두 관리할 수는 없습니다. 그러나 보고서 서버 관리자는 각 구독에 액세스하여 수정하거나 삭제할 수 있습니다.  
  
##  <a name="to-delete-a-subscription"></a><a name="bkmk_delete_subscription"></a> 구독을 삭제하려면  
구독을 삭제하려면  
  
1. [보고서 서버의 웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)을 찾습니다.  
  
2. 웹 포털의 도구 모음에서 **내 구독**을 선택하고 수정하거나 삭제할 구독으로 이동합니다.  
  
3. 보고서를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
보고서 서버에서 현재 처리 중인 구독을 취소하는 방법에 대한 자세한 내용은 [실행 중인 프로세스 관리](../../reporting-services/subscriptions/manage-a-running-process.md)를 참조하세요.  
  
 구독을 종료하려는 경우 해당 구독을 찾을 수 없으면 받고 있는 보고서를 확인하여 이름으로 검색합니다. 보고서에 액세스되면 구독에서 자신의 이름을 제거할 수 있습니다. 구독을 찾을 수 없는 경우 해당 구독이 데이터 기반 구독일 수 있습니다. 자세한 내용은 보고서 서버 관리자에게 문의하세요.  
  
 기본 보고서가 삭제되면 구독이 자동으로 삭제됩니다. 처리 중인 구독을 삭제하는 경우 배달 확장 프로그램에서 구독 데이터를 받기 전에 삭제 작업을 수행하면 구독이 중지됩니다. 그렇지 않으면 구독이 계속해서 처리됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
 [PowerShell을 사용하여 Reporting Services 구독 소유자 변경, 나열 및 구독 실행](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
 [데이터 기반 구독](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
 [보고서 서버의 웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)  
 [내 구독 사용&#40;기본 모드 보고서 서버&#41;](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
