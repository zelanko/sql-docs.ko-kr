---
title: Reporting Services 구성 파일 수정(RSreportserver.config) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 958ef51f-2699-4cb2-a92e-3b4322e36a30
caps.latest.revision: 5
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: c8c94038b2573fdc16305c502fc0b7e01bf9600a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080579"
---
# <a name="modify-a-reporting-services-configuration-file-rsreportserverconfig"></a>Reporting Services 구성 파일 수정(RSreportserver.config)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 는 응용 프로그램 설정을 구성 파일 집합에 저장합니다. 설치 프로그램은 사용자가 설치하는 각 보고서 서버 인스턴스에 대한 구성 파일을 만듭니다. 각 파일 내에서 값은 설치 중 설정되거나 도구 및 응용 프로그램을 사용하여 작업을 위해 서버를 구성할 때 설정됩니다. 경우에 따라 파일을 직접 수정하여 고급 설정을 추가하거나 구성해야 합니다. 구성 설정은 XML 요소나 특성으로 지정됩니다. XML과 구성 파일에 대해 이해하고 있으면 텍스트나 코드 편집기를 사용하여 사용자 정의 가능한 설정을 수정할 수 있습니다.  
  
 일부 구성 설정은 도구를 통해서만 설정할 수 있습니다. 암호화된 값이 포함된 설정은 Reporting Services 구성 도구, 설치 프로그램 또는 **rsconfig** 명령줄 유틸리티를 통해 수정해야 합니다. 이러한 도구를 실행하려면 로컬 관리자 그룹의 멤버여야 합니다.  
  
> [!IMPORTANT]  
>  구성 파일을 수정할 때는 주의해야 합니다. 내부용으로 예약된 설정을 수정할 경우 설치가 불가능할 수도 있습니다. 일반적으로 특정 문제를 해결하려는 경우 외에는 구성 설정을 수정하지 않는 것이 좋습니다. 변경해도 문제가 없는 설정에 대한 자세한 내용은 [RSReportServer Configuration File](rsreportserver-config-configuration-file.md) 또는 [RSReportDesigner Configuration File](rsreportdesigner-configuration-file.md)을 참조하세요. 구성 파일에 대한 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 제품 설명서를 참조하세요.  
  
 항목 내용  
  
-   [구성 값 읽기 및 사용](#bkmk_read_values)  
  
-   [기본값 정보](#bkmk_default_values)  
  
-   [구성 설정 삭제](#bkmk_delete_config_settings)  
  
-   [Reporting Services 구성 파일을 편집하려면](#bkmk_edit_configuation_file)  
  
##  <a name="bkmk_read_values"></a> 구성 값 읽기 및 사용  
 보고서 서버는 서비스가 시작될 때 및 구성 파일이 저장될 때마다 구성 파일을 읽습니다. 새 값 및 수정된 값은 현재 응용 프로그램 도메인이 만료된 후 새 응용 프로그램 도메인에 적용됩니다. 가능하면 현재 응용 프로그램 도메인에서 아직 처리 중인 요청이 완료되도록 허용됩니다. 그러나 일부 설정의 경우 응용 프로그램 도메인 재활용 작업을 바로 수행해야 합니다. 이 경우 처리 중인 모든 요청이 새 응용 프로그램 도메인에서 다시 시작됩니다.  
  
 잘못된 값이 감지되면 보고서 서버는 Windows 응용 프로그램 로그에 오류를 기록하고 오류에 따라 시작되지 못하거나 기본값을 사용합니다.  
  
-   XML 형식이 잘못되었음을 나타내는 오류인 경우 보고서 서버는 시작되지 않습니다. 오류가 발생할 때 보고서 서버가 실행 중이면 보고서 서버는 다시 시작되거나 응용 프로그램 도메인이 재활용될 때까지 잘못된 구성 파일을 무시합니다. 오류가 감지되면 보고서 서버는 더 이상 시작되지 않습니다.  
  
-   잘못된 구성 값 오류인 경우 서버는 내부 기본값을 사용하고 추적 로그 파일에 오류를 기록합니다. 내부 기본값을 사용할 수 없는 드문 경우 잘못된 구성 설정이 서버 작업에 중요하면 서버가 rsServerConfigurationError 오류를 반환합니다. 누락되었거나 잘못된 중요한 설정에 대한 오류는 클라이언트 응용 프로그램의 HTML 오류 페이지에 반환되고 이벤트 로그에 기록됩니다.  
  
 성공적으로 적용된 변경 내용을 비롯하여 모든 구성 파일 변경 내용은 보고서 서버 추적 로그 파일에 기록됩니다. 오류만 응용 프로그램 이벤트 로그에 기록됩니다.  
  
##  <a name="bkmk_default_values"></a> 기본값 정보  
 대부분의 구성 설정에는 보고서 서버에서 내부적으로 지정된 기본값이 있습니다. 사용자 정의 값이 올바르지 않거나 지정되지 않은 경우 보고서 서버는 이러한 값을 사용합니다. 잘못된 구성 설정으로 인해 기본값을 사용해야 하는 경우 추적 로그 파일에 오류가 기록됩니다.  
  
##  <a name="bkmk_delete_config_settings"></a> 구성 설정 삭제  
 기본값이 지정된 구성 설정의 경우 구성 파일에서 해당 설정을 제거해도 아무런 영향이 없습니다. 실제로 대부분의 구성 설정은 내부적으로 정의되고 구성됩니다. 구성 파일에서 항목을 삭제해도 내부 복사본은 계속 사용할 수 있으며 해당 항목에 대해 정의된 기본값이 사용됩니다.  
  
##  <a name="bkmk_edit_configuation_file"></a> Reporting Services 구성 파일을 편집하려면  
  
1.  편집할 구성 파일을 찾습니다.  
  
    -   **RSReportServer.config** 는 다음 디렉터리에 있습니다.  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
        ```  
  
    -   **RSReportServerServices.exe.config** 는 다음 디렉터리에 있습니다.  
  
        ```  
        C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer\bin  
        ```  
  
    -   **RSReportDesigner.config** 는 다음 디렉터리에 있습니다.  
  
        ```  
        C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
        ```  
  
2.  변경 내용을 롤백해야 하는 경우에 대비하여 파일의 복사본을 저장합니다.  
  
3.  메모장 또는 코드 편집기에서 원래 파일을 엽니다. Textpad는 파일이 저장되기 전에 파일 길이를 설정하여 추적 로그 파일에 잘못된 문자 오류가 기록되게 하므로 사용하지 마세요.  
  
4.  추가 또는 사용할 요소나 값을 입력합니다. 요소는 대/소문자를 구분합니다. 요소를 추가하는 경우 올바른 대/소문자를 사용해야 합니다. 렌더링 확장 프로그램, 인증 확장 프로그램 또는 데이터 처리 확장 프로그램을 사용자 지정하는 경우 구성 파일 편집에 대한 특정 지침을 사용할 수 있습니다.  
  
    -   [보고서 서버 인증](../security/authentication-with-the-report-server.md)  
  
    -   [보고서 관리자에서 사용자 지정 인증 쿠키를 전달하도록 구성](../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)  
  
    -   [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수 사용자 지정](../customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
5.  파일을 저장합니다.  
  
6.  추적 로그 파일에서 오류가 발생하지 않았는지 확인합니다. 오류 상태가 표시되는 경우 설정 또는 해당 값이 잘못 지정된 것입니다. 오류를 발생시키는 설정에 대한 유효한 값을 보려면 [RSReportServer Configuration File](rsreportserver-config-configuration-file.md) 을 검토하세요. 추적 로그를 보는 방법은 [보고서 서버 서비스 추적 로그](report-server-service-trace-log.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [RSReportServer 구성 파일](rsreportserver-config-configuration-file.md)   
 [ReportingServicesService 구성 파일](reportingservicesservice-configuration-file.md)   
 [RSReportDesigner 구성 파일](rsreportdesigner-configuration-file.md)   
 [데이터 처리 확장 프로그램 배포](../extensions/data-processing/deploying-a-data-processing-extension.md)   
 [배달 확장 프로그램 배포](../extensions/delivery-extension/deploying-a-delivery-extension.md)   
 [렌더링 확장 프로그램 배포](../extensions/rendering-extension/deploying-a-rendering-extension.md)   
 [방법: 사용자 지정 보고서 항목 배포](../custom-report-items/how-to-deploy-a-custom-report-item.md)   
 [Reporting Services 구성 파일](reporting-services-configuration-files.md)  
  
  