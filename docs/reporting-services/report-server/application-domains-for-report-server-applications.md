---
title: "보고서 서버 응용 프로그램의 응용 프로그램 도메인 | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "응용 프로그램 도메인 [Reporting Services]"
  - "응용 프로그램 도메인 재활용"
ms.assetid: a455e2e6-8764-493d-a1bc-abe80829f543
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 18
---
# 보고서 서버 응용 프로그램의 응용 프로그램 도메인
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 보고서 서버는 보고서 서버 웹 서비스, 보고서 관리자 및 백그라운드 처리 응용 프로그램을 포함하는 단일 서비스로 구현됩니다. 각 응용 프로그램은 단일 보고 서버 프로세스 내 자체 응용 프로그램 도메인에서 실행됩니다. 대부분의 경우 응용 프로그램 도메인은 내부적으로 생성, 구성 및 관리됩니다. 그러나 보고서 서버 응용 프로그램 도메인에 대해 재활용 작업이 발생하는 방식을 이해하면 성능 또는 메모리 문제를 조사하거나 서비스 장애 문제를 해결하는 경우 도움이 될 수 있습니다.  
  
> [!NOTE]  
>  기본 인증을 사용하는 보고서 서버에서 보고서 작성기 액세스를 구성하는 경우 보고서 작성기는 자체 응용 프로그램 도메인에서 실행됩니다. 이 응용 프로그램 도메인은 서버 프로세스에서 실행되는 다른 응용 프로그램 도메인과 다릅니다. 이 도메인은 서비스 컨트롤러에 의해 관리되며 보고서 서버의 메모리 부족에 대한 응답으로 메모리 할당을 다시 조정하는 메모리 관리 기능의 영향을 받지 않습니다.  
  
 다음 목록에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 응용 프로그램에 대해 응용 프로그램 도메인 재활용 작업을 발생시키는 이벤트를 설명합니다.  
  
-   미리 정의된 간격에 따라 발생하는 예약된 재활용 작업  
  
-   보고서 서버의 구성 변경  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 구성 변경  
  
-   메모리 할당 실패  
  
 다음 표에서는 이러한 이벤트에 대한 응답으로 발생하는 응용 프로그램 도메인 재활용 동작을 요약하여 설명합니다.  
  
|이벤트|이벤트 설명|적용 대상|구성 가능 여부|재활용 작업 설명|  
|-----------|-----------------------|----------------|------------------|-----------------------------------|  
|미리 정의된 간격에 따라 발생하는 예약된 재활용 작업|기본적으로 응용 프로그램 도메인은 12시간 간격으로 재활용됩니다.<br /><br /> 예약된 재활용 작업은 전반적인 프로세스 상태를 개선하는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램에 일반적입니다.|보고서 서버 웹 서비스<br /><br /> 보고서 관리자<br /><br /> 백그라운드 처리 응용 프로그램|예 RSReportServer.config 파일의**RecycleTime** 구성 설정에 따라 재활용 간격이 결정됩니다.<br /><br /> **MaxAppDomainUnloadTime** 은 백그라운드 처리가 완료되도록 허용되는 대기 시간을 설정합니다.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 은 웹 서비스 및 보고서 관리자에 대한 재활용 작업을 관리합니다.<br /><br /> 백그라운드 처리 응용 프로그램의 경우 보고서 서버는 일정에서 시작되는 새 작업에 대해 새 응용 프로그램 도메인을 만듭니다. 이미 진행 중인 작업은 대기 시간이 만료될 때까지 현재 응용 프로그램 도메인에서 완료되도록 허용됩니다.|  
|보고서 서버의 구성 변경|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 RSReportServer.config 파일 변경에 대한 응답으로 응용 프로그램 도메인을 재활용합니다.|보고서 서버 웹 서비스<br /><br /> 보고서 관리자<br /><br /> 백그라운드 처리 응용 프로그램|아니요.|재활용 작업이 발생하지 않도록 할 수는 없습니다. 그러나 구성 변경에 대한 응답으로 발생하는 재활용 작업은 예약된 재활용 작업과 같은 방식으로 처리됩니다. 현재 요청 및 작업이 현재 응용 프로그램 도메인에서 완료되는 동안 새 요청에 대해 새 응용 프로그램 도메인이 만들어집니다.|  
|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 구성 변경|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 모니터링하는 파일(예: machine.config 파일, Web.config 파일 및 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 프로그램 파일)에 변경 내용이 있는 경우 응용 프로그램 도메인을 재활용합니다.|보고서 서버 웹 서비스<br /><br /> 보고서 관리자|아니요.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 은 해당 작업을 관리합니다.<br /><br /> [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 에서 시작된 재활용 작업은 백그라운드 처리 응용 프로그램 도메인에 영향을 주지 않습니다.|  
|메모리 부족 및 메모리 할당 실패|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR은 메모리 할당 실패 시 또는 서버의 메모리가 매우 부족한 상태인 경우 응용 프로그램 도메인을 즉시 재활용합니다.|보고서 서버 웹 서비스<br /><br /> 보고서 관리자<br /><br /> 백그라운드 처리 응용 프로그램|아니요.|메모리가 매우 부족한 경우 보고서 서버는 현재 응용 프로그램 도메인에서 새 요청을 받지 않습니다. 서버가 새 요청을 거부하는 동안에는 HTTP 503 오류가 발생합니다. 이전 응용 프로그램 도메인이 언로드될 때까지 새 응용 프로그램 도메인이 만들어지지 않습니다. 즉, 서버의 메모리가 매우 부족한 상태에서 구성 파일을 변경하는 경우 진행 중인 요청 및 작업이 시작 또는 완료되지 않을 수 있습니다.<br /><br /> 메모리 할당이 실패하면 모든 응용 프로그램 도메인이 즉시 다시 시작되고, 진행 중이던 작업 및 요청이 삭제됩니다. 이러한 작업 및 요청은 수동으로 다시 시작해야 합니다.|  
  
## 계획되거나 계획되지 않은 재활용 작업  
 재활용 작업은 이 작업을 발생시키는 조건에 따라 계획되거나 계획되지 않을 수 있습니다.  
  
-   계획된 재활용 작업은 RSReportServer.config 파일에 정의된 정기적 간격에 따라 발생합니다. 기본값은 12시간 간격입니다. 이는 전반적인 프로세스 상태를 개선하는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램에 일반적입니다. 계획된 재활용 작업의 경우 보고서 서버는 새 요청에 대해 추가 응용 프로그램 도메인을 만듭니다. 이미 진행 중인 요청은 대기 시간이 만료될 때까지 현재 응용 프로그램 도메인에서 완료되도록 허용됩니다. 계획된 재활용 작업을 제어하는 구성 설정은 서버 전체에 대해 설정됩니다. 각 응용 프로그램에 대해 서로 다른 재활용 일정 또는 메모리 임계값을 구성할 수 없습니다.  
  
-   계획되지 않은 재활용 작업은 구성 변경, 메모리 부족 및 메모리 할당 실패에 대한 응답으로 임의의 시간에 발생합니다.  
  
    -   구성 변경의 경우 보고서 서버는 새 요청을 응용 프로그램 도메인의 새 인스턴스로 리디렉션하는 소프트 재활용을 사용하려고 합니다. 소프트 재활용이 실패하면 서버는 진행 중인 모든 요청을 취소하고 현재 응용 프로그램 도메인을 종료하며 응용 프로그램 도메인을 다시 시작하는 하드 응용 프로그램 도메인 재활용을 시작합니다.  
  
    -   메모리 할당 실패는 서버에서 수행되는 보고서 처리량에 비해 시스템 리소스가 부족함을 나타냅니다. 모든 응용 프로그램 도메인에 대해 하드 재활용 작업은 메모리 할당 실패에 대한 응답으로 발생합니다. 모든 요청 큐는 지워집니다. 취소된 요청은 다시 시작되지 않습니다. 대화형으로 보고서를 보고 있던 사용자는 보고서를 새로 고치거나 다시 열어야 합니다. 예약된 처리는 다음 예약된 시간에 발생합니다. 지연이 허용되지 않는 경우 보고서 스냅숏을 수동으로 새로 고치거나 구독 일정 또는 보고서 스냅숏 일정을 수정하여 즉시 실행되도록 할 수 있습니다.  
  
 재활용 작업을 발생시키는 상황에 따라 보고서 서버 웹 서비스, 보고서 관리자 및 백그라운드 처리 응용 프로그램의 응용 프로그램 도메인은 함께 또는 개별적으로 재활용될 수 있습니다.  
  
-    [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 에서 시작된 재활용 작업은 보고서 서버 웹 서비스 및 보고서 관리자와 같은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램에 영향을 줍니다. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 은 모니터링하는 파일에 변경 내용이 있는지 여부에 따라 응용 프로그램 도메인을 재활용합니다. 일반적으로 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 에서 시작된 재활용 작업은 백그라운드 처리 응용 프로그램에 대한 재활용 작업과 무관합니다.  
  
-   일반적으로 보고서 서버에서 시작된 재활용 작업은 보고서 서버 웹 서비스, 보고서 관리자 및 백그라운드 처리 응용 프로그램에 영향을 줍니다. 재활용 작업은 구성 설정 변경에 대한 응답으로 발생하며 서비스가 다시 시작됩니다.  
  
## 응용 프로그램 도메인에 대한 RSReportServer 구성 설정  
 구성 설정은 [RSReportServer 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)에 지정되어 있습니다. 다음 예에서는 계획된 응용 프로그램 도메인 재활용 동작에 대한 기본 구성 설정을 보여 줍니다.  
  
 `<RecycleTime>720</RecycleTime>`  
  
 `<MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>`  
  
 다음 표에서는 이러한 요소를 설명합니다.  
  
|요소|적용 대상|정의|  
|-------------|----------------|----------------|  
|**RecycleTime**|3가지 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 응용 프로그램 도메인|응용 프로그램 도메인이 재활용되는 빈도를 지정합니다. 기본 재활용 일정은 일반적으로 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램 도메인 재활용에 적용되는 12시간 패턴을 따릅니다. 예약된 시간에 모든 새 요청이 응용 프로그램 도메인의 새 인스턴스로 전달됩니다. 원본 인스턴스에서 현재 진행 중인 요청은 완료되도록 허용됩니다. 모든 프로세스가 완료되면 원본 인스턴스가 삭제되고 새 인스턴스가 유일한 활성 응용 프로그램 도메인 인스턴스가 됩니다.<br /><br /> 기본값은 720분입니다.|  
|**MaxAppDomainUnloadTime**|백그라운드 처리 응용 프로그램 도메인에만|기본적으로 보고서 서버는 재활용 작업 중에 응용 프로그램 도메인이 종료되도록 허용되는 30분의 대기 시간을 할당합니다. 할당된 시간 동안 현재 진행 중인 작업을 완료할 수 없거나 대기 시간이 허용하는 것보다 작업이 오래 걸릴 경우 응용 프로그램 도메인 인스턴스가 즉시 다시 시작됩니다. 완료되지 않은 모든 작업은 종료됩니다.<br /><br /> 상태를 보거나 보고서 서버에서 실행되는 작업을 취소하는 방법에 대한 자세한 내용은 [보고서 서버 작업 취소&#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)를 참조하세요.|  
  
> [!NOTE]  
>  보고서 서버 웹 서비스와 보고서 관리자는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램이지만 두 응용 프로그램 모두 IIS에서 호스팅되는 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 응용 프로그램에 대해 machine.config에 지정되어 있을 수 있는 예약된 응용 프로그램 도메인 재활용에 응답하지 않습니다.  
  
## 관련 항목:  
 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [보고서 서버 응용 프로그램을 위한 사용 가능한 메모리 구성](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
  
  