---
title: 구독 및 배달(Reporting Services) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- reports [Reporting Services], distributing
- distributing reports [Reporting Services]
- published reports [Reporting Services], distributing
- sending reports
- sharing reports
- delivering reports [Reporting Services]
- distributing reports [Reporting Services], subscriptions
- subscriptions [Reporting Services], about subscriptions
- subscriptions [Reporting Services]
ms.assetid: be7ec052-28e2-4558-bc09-8479e5082926
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e04bdc6edaf53e73c7f26dd85a512dbda369ebb1
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52711965"
---
# <a name="subscriptions-and-delivery-reporting-services"></a>구독 및 배달(Reporting Services)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독은 특정 시간 또는 이벤트에 대한 응답으로 보고서를 지정하는 파일 형식으로 배달하는 구성입니다. 예를 들어 수요일마다 MonthlySales.rdl 보고서를 Microsoft Word 문서로 파일 공유에 저장합니다. 구독을 사용하면 특정 보고서 매개 변수 값 집합을 사용하여 일정을 예약한 다음 보고서 배달을 자동화할 수 있습니다.  
  
 단일 보고서에 대해 여러 구독을 만들어 구독 옵션을 다양화할 수 있습니다. 예를 들어 서로 다른 매개 변수 값을 지정하여 세 가지 버전의 보고서(예: 서부 지역 판매 보고서, 동부 지역 판매 보고서, 모든 판매 보고서)를 생성할 수 있습니다.  
  
 ![ssrs 구독 흐름 예제](../../reporting-services/subscriptions/media/ssrs-subscription-example-flow.png "ssrs 구독 흐름 예제")  
  
 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서는 구독을 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2017의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md)을 참조하세요.  
  
 **항목 내용**  
  
-   [구독 및 배달 시나리오](#bkmk_subscription_scenarios)  
  
-   [표준 및 데이터 기반 구독](#bkmk_standard_and_datadriven)  
  
-   [구독 요구 사항](#bkmk_subscription_requirements)  
  
-   [배달 확장 프로그램](#bkmk_delivery_extensions)  
  
-   [구독 요소](#bkmk_parts_of_subscription)  
  
-   [구독 처리 방법](#bkmk_subscription_processing)  
  
-   [구독의 프로그래밍 방식 제어](#bkmk_code)  
  
 **이 섹션의 항목:**  
  
-   [Reporting Services의 메일 배달](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md) 보고서 서버 메일 배달 작업 및 구성에 대해 설명합니다.  
  
-   [기본 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) 기본 모드 보고서 서버로 구독을 만드는 자세한 단계입니다.  
  
-   [SharePoint 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) SharePoint 모드 보고서 서버로 구독을 만드는 자세한 단계입니다.  
  
-   [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md) 보고서 서버 파일 공유 배달 작업 및 구성에 대해 설명합니다.  
  
-   [Disable or Pause Report and Subscription Processing](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)입니다.  
  
-   [SharePoint Library Delivery in Reporting Services](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md) SharePoint 라이브러리에 대한 구독 배달에 대해 설명합니다.  
  
-   [데이터 기반 구독](../../reporting-services/subscriptions/data-driven-subscriptions.md) 데이터 기반 구독을 사용하여 실행 시 보고서 출력을 사용자 지정하는 방법에 대한 정보를 제공합니다.  
  
-   [Reporting Services 구독 모니터링](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
  
-   [PowerShell을 사용하여 Reporting Services 구독 소유자 변경, 나열 및 구독 실행](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
##  <a name="bkmk_subscription_scenarios"></a> 구독 및 배달 시나리오  
 각 구독에 대해 배달 옵션을 구성하고, 사용 가능한 옵션은 선택한 배달 확장 프로그램에 의해 결정됩니다. 배달 확장 프로그램은 여러 방식의 배포를 지원하는 모듈입니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 여러 가지 배달 확장 프로그램이 포함되며 배달 확장 프로그램은 타사에서 제공할 수 있습니다.  
  
 개발자인 경우 추가 시나리오를 지원하기 위해 사용자 지정 배달 확장 프로그램을 만들 수 있습니다. 자세한 내용은 [Implementing a Delivery Extension](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)을 참조하세요.  
  
 다음 테이블은 일반적인 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독 시나리오를 설명합니다.  
  
|시나리오|설명|  
|--------------|-----------------|  
|전자 메일 보고서|전자 메일은 개별 사용자 및 그룹에 보고합니다. 배포할 보고서를 받으려면 구독을 만들고 그룹 별칭 또는 전자 메일 별칭을 지정합니다. 런타임에 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에서 구독 데이터를 결정하도록 할 수 있습니다. 멤버 목록이 변경된 그룹에 동일한 보고서를 보내려면 쿼리를 사용하여 런타임에 구독 목록을 파생시킵니다.|  
|오프라인으로 보고서 보기|사용자는 다음 구독 출력 형식 중 하나를 선택할 수 있습니다.<br /><br /> - 보고서 데이터를 가진 XML 파일<br />- CSV(쉼표로 분리)<br />- PDF<br />- MHTML(웹 보관 파일)<br />- Microsoft Excel<br />- TIFF 파일<br />- Microsoft Word<br /><br /> 보관할 보고서는 심야 백업 일정을 지정한 공유 폴더로 직접 보낼 수 있습니다. 브라우저에서 로드하는 데 시간이 오래 걸리는 대용량 보고서는 데스크톱 애플리케이션에서 볼 수 있는 형식으로 공유 폴더로 보낼 수 있습니다.|  
|캐시 미리 로드|매개 변수가 있는 보고서 인스턴스가 여러 개 있거나 보고서를 볼 사람이 많은 경우 캐시에서 보고서를 미리 로드하여 보고서를 표시하기 위해 걸리는 처리 시간을 줄일 수 있습니다.|  
|데이터 기반 보고서|데이터 기반 구독을 사용하여 런타임에 보고서 출력, 배달 옵션 및 보고서 매개 변수 설정을 사용자 지정합니다. 구독에서는 쿼리를 사용하여 런타임에 데이터 원본의 입력된 값을 가져옵니다. 데이터 기반 구독을 사용하여 구독 처리 시 결정되는 구독자 목록으로 보고서를 보낼 메일 병합 작업을 수행할 수 있습니다.|  
  
##  <a name="bkmk_standard_and_datadriven"></a> 표준 및 데이터 기반 구독  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 두 가지 구독인 **표준** 과 **데이터 기반**구독을 지원합니다. 표준 구독은 개별 사용자가 만들어 관리합니다. 표준 구독은 구독 처리 시에 변경되지 않는 정적 값으로 구성됩니다. 각 표준 구독에는 보고서 표시 옵션, 배달 옵션 및 보고서 매개 변수 세트가 하나씩 있습니다.  
  
 데이터 기반 구독은 받는 사람, 보고서 매개 변수 또는 애플리케이션 형식을 지정하는 데 사용되는 값을 제공하는 외부 데이터 원본을 쿼리하여 런타임에 구독 정보를 가져옵니다. 받는 사람 목록이 아주 크거나 받는 사람마다 보고서 출력을 다르게 나타내려는 경우 데이터 기반 구독을 사용할 수 있습니다. 데이터 기반 구독을 사용하려면 쿼리 작성에 대한 전문 지식이 필요하며 매개 변수 사용 방법을 잘 알고 있어야 합니다. 일반적으로 보고서 서버 관리자가 이러한 구독을 만들고 관리합니다. 자세한 내용은 다음 항목을 참조하세요.  
  
-   [데이터 기반 구독](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
  
-   [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
  
##  <a name="bkmk_subscription_requirements"></a> 구독 요구 사항  
 보고서에 대한 구독을 만들려면 다음과 같은 사전 요구 사항을 충족해야 합니다.  
  
|요구 사항|설명|  
|-----------------|-----------------|  
|Permissions|보고서에 대한 액세스 권한이 있어야 합니다. 보고서를 구독하려면 보고서를 볼 사용 권한이 있어야 합니다.<br /><br /> 기본 모드 보고서 서버의 경우 다음과 같은 역할 할당은 구독에 영향을 줍니다.<br /><br /> - "개별 구독 관리" 태스크를 사용하면 특정 보고서에 대한 구독을 생성, 수정 및 삭제할 수 있습니다. 미리 정의된 역할에서 이 태스크는 브라우저 및 보고서 작성기 역할의 일부입니다. 사용자는 이 태스크를 포함하는 역할 할당을 사용하여 자신이 만든 구독만 관리할 수 있습니다.<br />- "모든 구독 관리" 태스크를 사용하면 모든 구독을 액세스 및 수정할 수 있습니다. 이 태스크는 데이터 기반 구독을 만드는 데 필요합니다. 미리 정의된 역할에서 내용 관리자 역할에만 이 태스크가 포함됩니다.|  
|저장된 자격 증명|구독을 만들려면 보고서는 런타임에 데이터를 검색하기 위해 저장된 자격 증명을 사용하거나 자격 증명을 사용하지 말아야 합니다. 현재 사용자의 가장된 자격 증명이나 위임된 자격 증명을 사용하여 외부 데이터 원본에 연결하도록 구성된 보고서는 구독할 수 없습니다. 저장된 자격 증명은 Windows 계정이거나 데이터베이스 사용자 계정일 수 있습니다. 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요.<br /><br /> 사용자에게는 보고서를 보고 개별 구독을 만들 수 있는 권한이 있어야 합니다. 또한 보고서 서버에서**예약된 이벤트 및 보고서 배달** 을 설정해야 합니다. 자세한 내용은 [기존_기본 모드 보고서 서버 구독 만들기 및 관리](https://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)를 참조하세요.|  
|보고서의 사용자 종속 값|표준 구독의 경우에는 사용자 계정 정보를 필터에 통합하거나 보고서에 표시되는 텍스트로 통합하는 보고서에 대한 구독을 만들 수 있습니다. 보고서에서 사용자 계정 이름은 현재 사용자로 확인되는 **User!UserID** 식을 통해 지정됩니다. 구독을 만들 때 구독을 만드는 사용자는 현재 사용자로 간주됩니다.|  
|모델 항목 보안 불가|모델에 모델 항목 보안 설정이 포함된 경우 모델을 데이터 원본으로 사용하는 보고서 작성기 보고서를 구독할 수 없습니다. 모델 항목 보안을 사용하는 보고서만 이러한 제한을 받습니다.|  
|매개 변수 값|보고서에서 매개 변수를 사용하는 경우 보고서 자체 또는 정의된 구독에 매개 변수 값을 지정해야 합니다. 보고서에 기본값이 정의된 경우 기본값을 사용하도록 매개 변수 값을 설정할 수 있습니다.|  
  
##  <a name="bkmk_delivery_extensions"></a> 배달 확장 프로그램  
 구독은 보고서 서버에서 처리되고 서버에 배포된 배달 확장 프로그램을 통해 배포됩니다. 기본적으로 공유 폴더 또는 전자 메일 주소로 보고서를 보내는 구독을 만들 수 있습니다. 보고서 서버가 SharePoint 통합 모드로 구성되어 있는 경우 보고서를 SharePoint 라이브러리로 보낼 수도 있습니다.  
  
 사용자는 구독을 만들 때 사용 가능한 배달 확장 프로그램 중 하나를 선택하여 보고서를 배달하는 방법을 결정할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 다음과 같은 배달 확장 프로그램이 포함되어 있습니다.  
  
|배달 확장 프로그램|설명|  
|------------------------|-----------------|  
|Windows 파일 공유|보고서를 정적 애플리케이션 파일 형식으로 네트워크에서 액세스할 수 있는 공유 폴더로 배달합니다.|  
|전자 메일|알림 또는 보고서를 전자 메일 첨부 파일 또는 URL 링크로 배달합니다.|  
|SharePoint 라이브러리|보고서를 정적 애플리케이션 파일 형식으로 SharePoint 사이트에서 액세스할 수 있는 SharePoint 라이브러리로 배달합니다. 해당 사이트는 SharePoint 통합 모드에서 실행되는 보고서 서버와 통합되어야 합니다.|  
|Null|Null 배달 공급자는 즉시 볼 수 있는 매개 변수가 있는 보고서와 함께 캐시를 미리 로드하는 데 사용되는 매우 특수화된 배달 확장 프로그램입니다. 이 메서드는 개별 구독의 사용자가 사용할 수 없습니다. Null 배달은 데이터 기반 구독에서 캐시를 미리 로드하여 보고서 서버 성능을 향상시키기 위해 관리자가 사용합니다.|  
  
> [!NOTE]  
>  보고서 배달은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 아키텍처의 확장 가능한 부분입니다. 타사 공급업체는 보고서를 다른 위치나 디바이스로 라우팅하는 사용자 지정 배달 확장 프로그램을 만들 수 있습니다. 사용자 지정 배달 확장 프로그램에 대한 자세한 내용은 [Implementing a Delivery Extension](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)을 참조하세요.  
  
##  <a name="bkmk_parts_of_subscription"></a> 구독 요소  
 구독 정의는 다음과 같은 요소로 구성됩니다.  
  
-   무인 모드로 실행할 수 있는 보고서(저장된 자격 증명을 사용하거나 자격 증명을 사용하지 않는 보고서)에 대한 포인터  
  
-   배달 방법(예: 전자 메일) 및 배달 모드 설정(예: 전자 메일 주소)  
  
-   보고서를 특정 형식으로 나타내기 위한 렌더링 확장 프로그램  
  
-   이벤트로 표시되는 구독 처리 조건  
  
     일반적으로 보고서 실행 조건은 시간을 기반으로 합니다. 예를 들어 UTC 시간으로 화요일 오후 3시마다 특정 보고서를 실행할 수 있습니다. 그러나 보고서가 스냅숏으로 실행되는 경우 스냅숏을 새로 고칠 때마다 구독이 실행되도록 지정할 수 있습니다.  
  
-   보고서를 실행할 때 사용되는 매개 변수  
  
     매개 변수는 옵션이며 매개 변수 값이 적용되는 보고서에 대해서만 지정됩니다. 구독은 일반적으로 사용자 소유이므로 지정되는 매개 변수 값은 구독에 따라 다릅니다. 예를 들어 각 부서의 영업 관리자는 해당 부서의 데이터를 반환하는 매개 변수를 사용합니다. 모든 매개 변수에는 명시적으로 정의된 값이나 유효한 기본값이 있어야 합니다.  
  
 구독 정보는 보고서 서버 데이터베이스에 개별 보고서와 함께 저장됩니다. 구독을 연결된 보고서와 별도로 관리할 수는 없습니다. 설명, 다른 사용자 지정 텍스트 또는 기타 요소를 포함하도록 구독을 확장할 수 없습니다. 구독은 초기에 나열한 항목만 포함할 수 있습니다.  
  
##  <a name="bkmk_subscription_processing"></a> 구독 처리 방법  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 에는 보고서의 일정을 예약하고 보고서를 사용자에게 배달하는 기능을 제공하는 일정 예약 및 배달 프로세서가 포함되어 있습니다. 보고서 서버는 계속해서 이벤트를 모니터링하며 여기에 응답합니다. 구독에 대해 정의된 조건과 일치하는 이벤트가 발생하면 보고서 서버는 해당 구독을 읽고 보고서 처리 및 배달 방법을 결정합니다. 보고서 서버는 구독에 지정된 배달 확장 프로그램을 요청합니다. 배달 확장 프로그램이 실행되면 보고서 서버는 구독으로부터 배달 정보를 추출한 후 처리를 위해 배달 확장 프로그램에 전달합니다.  
  
 배달 확장 프로그램은 보고서를 구독에 정의된 형식으로 렌더링한 다음 보고서 또는 알림을 지정된 대상에 배달합니다. 보고서를 배달할 수 없으면 보고서 서버 로그 파일에 해당 항목이 기록됩니다. 다시 시도 작업을 지원하려면 첫 번째 시도가 실패할 경우 배달을 다시 시도하도록 보고서 서버를 구성할 수 있습니다.  
  
### <a name="processing-a-standard-subscription"></a>표준 구독 처리  
 표준 구독은 보고서 인스턴스를 1개 생성합니다. 보고서는 단일 공유 폴더 또는 구독에 지정된 전자 메일 주소에 배달됩니다. 보고서 레이아웃 및 데이터는 달라지지 않습니다. 보고서에서 매개 변수를 사용하는 경우 표준 구독은 보고서의 각 매개 변수에 대해 단일 값으로 처리됩니다.  
  
### <a name="processing-a-data-driven-subscription"></a>데이터 기반 구독 처리  
 데이터 기반 구독은 여러 대상에 배달되는 많은 보고서 인스턴스를 만들 수 있습니다. 보고서 레이아웃은 달라지지 않지만 매개 변수 값이 구독자 결과 집합으로부터 전달될 경우 보고서의 데이터가 달라질 수 있습니다. 보고서 렌더링 방법에 영향을 주는 배달 옵션 및 보고서가 전자 메일에 첨부되는지 또는 링크되는지 여부도 행 집합에서 값이 전달될 때 구독자에 따라 달라질 수 있습니다.  
  
 데이터 기반 구독은 여러 개의 배달을 만들 수 있습니다. 보고서 서버는 구독 쿼리로부터 반환되는 행 집합의 각 행에 대해 하나의 배달을 만듭니다.  
  
### <a name="report-delivery-characteristics"></a>보고서 배달 특징  
 표준 구독을 통해 배달되는 보고서는 일반적으로 정적 보고서로 렌더링됩니다. 이러한 보고서는 최신 보고서 실행 스냅숏을 기반으로 하거나 배달 완료를 위한 정적 보고서로 생성됩니다. 요청 시 실행되는 보고서에 대한 구독에서 **링크 포함** 옵션을 선택한 경우 사용자가 하이퍼링크를 클릭하면 보고서 서버에서 보고서를 실행합니다.  
  
> [!NOTE]  
>  URL을 통해 배달되는 보고서는 보는 동안에 보고서 서버에 연결된 채 업데이트되거나 삭제될 수 있습니다. 구독에 대해 선택한 배달 옵션에 따라 보고서가 URL로 배달될지, 전자 메일 메시지의 본문에 포함될지, 첨부 파일로 보내질지 여부가 결정됩니다.  
  
 데이터 기반 구독을 통해 배달되는 보고서는 구독을 처리하는 동안 다시 생성될 수 있습니다. 보고서 서버는 데이터 기반 구독을 완료하기 위해 보고서의 특정 인스턴스 또는 해당 데이터 세트에서 잠그지 않습니다. 구독에서 구독자마다 다른 매개 변수 값을 사용하는 경우 보고서 서버에서는 보고서를 다시 생성하여 필요한 결과를 만듭니다. 첫 번째 보고서 복사본이 작성되어 배달된 후에 기본으로 사용되는 데이터가 업데이트되면 프로세스의 후반에 보고서를 받은 사용자는 다른 결과 집합에 기반한 데이터를 볼 수 있습니다. 스냅숏으로 실행되는 보고서를 사용하여 모든 구독자에게 동일한 보고서 인스턴스가 배달되는지 확인할 수 있습니다. 그러나 구독이 처리되는 동안 스냅숏에 대해 예약된 업데이트가 발생하는 경우에도 사용자의 보고서에 다른 데이터가 표시될 수 있습니다.  
  
### <a name="triggering-subscription-processing"></a>구독 처리 트리거  
 보고서 서버는 일정에 지정된 시간 기반 이벤트나 스냅숏 업데이트 이벤트를 사용하여 구독 처리를 트리거합니다.  
  
 시간 기반 트리거는 보고서별 일정이나 공유 일정을 사용하여 구독 실행 시기를 지정합니다. 요청 시 실행 보고서 및 캐시된 보고서의 경우 일정이 유일한 트리거 옵션입니다.  
  
 스냅숏 업데이트 이벤트는 보고서 스냅숏의 예약된 업데이트를 사용하여 구독을 트리거합니다. 보고서에 설정된 보고서 실행 속성에 따라, 보고서가 새 데이터로 업데이트될 때마다 트리거되는 구독을 정의할 수 있습니다.  
  
##  <a name="bkmk_code"></a> 구독의 프로그래밍 방식 제어  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 개체 모델을 사용하면 프로그래밍 방식으로 구독 및 구독 처리를 감사하고 제어할 수 있습니다.  예를 들어 다음을 참조하고 시작하세요.  
  
-   [PowerShell을 사용하여 Reporting Services 구독 소유자 변경, 나열 및 구독 실행](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   PowerShell을 사용하여 구독을 활성화 및 비활성화하는 방법의 예제는 [Disable or Pause Report and Subscription Processing](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md)을 참조하세요.  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
-   **파일 공유 계정**을 사용하도록 구성된 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구독을 나열하는 예제 PowerShell 스크립트는 [구독 설정 및 파일 공유 계정&#40;구성 관리자&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [일정](../../reporting-services/subscriptions/schedules.md)   
 [Reporting Services 보고서 서버&#40;기본 모드&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services 구독 모니터링](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)  
  
  
