---
title: Reporting Services의 전자 메일 배달 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], e-mail
- e-mail [Reporting Services]
- mail [Reporting Services]
ms.assetid: fda2f130-97b9-4258-9dbb-e93a70f4d08a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f21a974ee9beeeba8b50914092704f1879c5f501
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575565"
---
# <a name="e-mail-delivery-in-reporting-services"></a>Reporting Services의 전자 메일 배달
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 개별 사용자 또는 그룹에 보고서를 메일로 보낼 수 있는 메일 배달 확장 프로그램이 포함되어 있습니다. 보고서를 전자 메일로 배포하려면 1) 전자 메일 배달용 보고서 서버를 구성하고 2) 표준 구독 또는 데이터 기반 구독을 정의합니다. 단일 구독에서 전자 메일 메시지 하나에 여러 보고서를 포함해 배달할 수는 없습니다. 그러나 여러 구독을 만들 수는 있습니다.  
  
 보고서 서버는 표준 연결을 통해 전자 메일 서버에 연결합니다. SSL(Secure Sockets Layer)을 통해 암호화된 통신은 사용하지 않습니다. 전자 메일 서버는 보고서 서버와 동일한 네트워크에 있는 원격 또는 로컬 SMTP(Simple Mail Transport Protocol) 서버여야 합니다.  
  
 구독을 만드는 방법을 안내하는 자세한 단계는 다음 항목을 참조하세요.  
  
-   [기본 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
-   [SharePoint 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 모드 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드|  
  
## <a name="e-mail-delivery-options"></a>전자 메일 배달 옵션  
 보고서 서버 전자 메일 배달에서는 다음과 같은 방법으로 보고서를 배달할 수 있습니다.  
  
-   생성된 보고서에 대한 알림 및 하이퍼링크를 보냅니다.  
  
-   전자 메일 메시지의 제목: 줄에 알림을 보냅니다. 기본적으로 구독 정의의 제목: 줄에는 구독 처리 시 보고서별 정보로 대체되는 다음과 같은 변수가 포함되어 있습니다.  
  
     **@ReportName** 은(는) 보고서 이름을 지정합니다.  
  
     **@ExecutionTime** 은(는) 보고서가 실행된 시간을 지정합니다.  
  
     각 구독의 제목: 줄에서 이러한 변수를 정적 텍스트와 결합하거나 텍스트를 수정할 수 있습니다.  
  
-   포함된 보고서 또는 첨부된 보고서를 보냅니다. 렌더링 형식과 브라우저에 따라 보고서가 포함될지 또는 첨부될지가 결정됩니다.  
  
     브라우저에서 HTML 4.0 및 MHTML을 지원하고 웹 보관 파일 렌더링 형식을 선택한 경우 보고서는 메시지의 일부로 포함됩니다. CSV, PDF를 비롯한 다른 렌더링 형식은 모두 보고서를 첨부 파일로 배달합니다. 기본 모드 보고서 서버의 경우 RSReportServer.config 구성 파일에서 이 기능을 해제할 수 있습니다.  
  
     [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 보고서를 보내기 전에 첨부 파일 또는 메시지의 크기를 확인하지 않습니다. 첨부 파일 또는 메시지가 메일 서버에서 허용하는 최대 제한을 초과할 경우 보고서가 배달되지 않습니다. 큰 보고서의 경우 URL, 알림 등과 같은 다른 배달 옵션 중 하나를 선택하십시오.  
  
 구독을 생성할 때 보고서 배달 방식을 결정하는 배달 옵션을 설정합니다. 예를 들어 구독에서 **링크 포함** 을 선택하면 메일 메시지에 보고서에 대한 하이퍼링크가 포함됩니다.  
  
## <a name="native-mode-role-based-e-mail-settings"></a>기본 모드 역할 기반 전자 메일 설정  
 기본 모드 보고서 서버 환경에서 사용하는 전자 메일 배달 설정은 역할에 "개별 구독 관리" 태스크가 포함되어 있는지 아니면 "모든 구독 관리" 태스크가 포함되어 있는지에 따라 달라집니다.  
  
|태스크|사용 가능한 설정|  
|----------|------------------------|  
|개별 구독 관리|사용자가 보고서 배달을 자동화하고 자신에게 보고서가 배달되도록 할 수 있는 필드가 표시됩니다. 이 모드에서는 전자 메일 별칭이 적용되는 필드를 사용할 수 없습니다.|  
|모든 구독 관리|받는 사람:, 참조:, 숨은 참조: 및 회신: 필드를 비롯하여 보다 폭넓은 배포를 지원하는 필드를 표시하여 보고서를 더 많은 구독자에게 라우팅하는 추가 방법을 제공합니다. 전자 메일 별칭 필드의 사용 여부는 RSReportServer 구성 파일 설정을 통해 정의됩니다.|  
  
## <a name="specifying-e-mail-addresses-in-a-subscription"></a>구독에 전자 메일 주소 지정  
 인트라넷 내에서 보고서를 배포하고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 서버에 대한 SMTP 게이트웨이를 사용하는 경우 동료에게 전자 메일을 보낼 때처럼 전자 메일 별칭을 입력합니다. 외부 전자 메일 계정에 배달할 경우 전체 전자 메일 주소를 입력합니다. 추가 전자 메일 주소를 지정하여 구독에 다른 구독자를 추가하면 이 구독에서 생성된 보고서의 복사본이 해당 구독자에게 전달됩니다.  
  
 보고서 서버는 전자 메일 주소의 유효성을 검사하거나 전자 메일 서버로부터 전자 메일 주소를 가져오지 않습니다. 따라서 사용할 전자 메일 주소를 미리 알고 있어야 합니다. 기본적으로 조직의 내부 또는 외부에 있는 유효한 모든 전자 메일 계정에 전자 메일로 보고서를 보낼 수 있습니다. 그러나 구성 설정을 사용하면 이름이 식별된 메일 서버 호스트에만 전자 메일을 배달하도록 제한할 수 있습니다. 조직의 멤버가 아닌 사용자에게 전자 메일을 배달하려면 추가 호스트를 지정할 수 있습니다.  
  
 보고서를 배달하는 데 사용되는 전자 메일 메시지는 전자 메일 서버에 정의된 전자 메일 계정으로 보내야 합니다. 구성 설정에서 전자 메일 계정을 지정합니다. 전자 메일 계정은 전자 메일 배달 확장 프로그램에서 배달되는 모든 보고서에 사용되기 때문에 여러 계정을 지정하거나 개별 보고서의 계정을 변경할 수 없습니다.  
  
## <a name="controlling-e-mail-delivery"></a>전자 메일 배달 제어  
 전자 메일 배포를 특정 호스트 도메인으로 제한하도록 보고서 서버를 구성할 수 있습니다. 예를 들어 기본 보고서 서버가 **RSReportServer.config** 구성 파일에 나열된 도메인을 제외한 모든 도메인에 보고서를 배달하지 못하도록 할 수 있습니다.  
  
 구독의 **받는 사람** 필드를 숨기도록 구성 설정을 지정할 수도 있습니다. 이런 경우 보고서는 구독을 정의하는 사용자에게만 배달됩니다. 그러나 사용자에게 보고서를 보낸 다음에는 보고서가 전달되지 않도록 명시적으로 방지할 수 없습니다.  
  
 보고서 배포를 제어하는 가장 효율적인 방법은 보고서 서버 URL로만 보내도록 보고서 서버를 구성하는 것입니다. 보고서 서버는 Windows 인증 및 역할 기반 인증 모델을 사용하여 보고서에 대한 액세스를 제어합니다. 보기 권한이 없는 사용자에게 전자 메일을 통해 보고서가 실수로 전달된 경우 보고서 서버는 해당 보고서를 표시하지 않습니다. 구독에 대한 자세한 내용은 다음 항목을 참조하세요.  
  
## <a name="e-mail-server-configuration"></a>전자 메일 서버 구성  
 기본 모드 보고서 서버의 경우에는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 파일을 편집하는 방식으로 기본 모드 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 관리자를 통해 메일 배달 확장 프로그램을 구성합니다. SharePoint 모드 보고서 서버의 경우에는 SharePoint 관리 페이지 및 PowerShell 스크립트에서 전자 메일 배달 확장 프로그램을 구성합니다.  
  
 
 기본 모드 보고서 서버를 구성하는 방법은 [메일 설정 - Reporting Services 기본 모드(구성 관리자)](../install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)를 참조하세요.
 
 
 SharePoint 모드 보고서 서버를 구성하는 방법에 대한 자세한 내용은 다음을 참조하십시오.  
  
  
## <a name="see-also"></a>참고 항목  
 [태스크 및 권한](../../reporting-services/security/tasks-and-permissions.md)   
 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [데이터 기반 구독](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [역할 할당](../../reporting-services/security/role-assignments.md)  
  
  
