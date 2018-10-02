---
title: RSReportDesigner 구성 파일 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], configuration file
- RSReportDesigner configuration file
ms.assetid: fdcc9c58-3bad-45b3-ba8e-c7816d64f14c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dff986f9007e721521a2bc4ac7094d0a72c1d4f5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836161"
---
# <a name="rsreportdesigner-configuration-file"></a>RSReportDesigner 구성 파일
  RSReportDesigner.config 파일에는 보고서 디자이너에 사용할 수 있는 렌더링 및 데이터 처리 확장 프로그램에 대한 설정이 저장됩니다. 데이터 처리 확장 프로그램 정보는 **Data** 요소에 저장됩니다. 렌더링 확장 프로그램 정보는 **Render** 요소에 저장됩니다. **Designer** 요소는 보고서 디자이너에 사용된 쿼리 작성기를 열거합니다.  
  
 보고서 디자이너에서는 포함된 보고서 서버 기능을 사용하여 보고서를 미리 봅니다. 미리 보기 작업에 대한 로컬 서버 쪽 처리를 지원하도록 서버 관련 설정을 지정할 수 있습니다. 보고서 서버 구성 설정에 대한 자세한 내용은 [RsReportServer.config 구성 파일](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)을 참조하세요.  
  
## <a name="file-location"></a>파일 위치  
 이 파일은 \Program Files\Microsoft Visual Studio 8\Common7\IDE\PrivateAssemblies에 있습니다.  
  
## <a name="editing-guidelines"></a>편집 지침  
 사용자 지정 확장 프로그램을 배포 또는 제거하거나, 미리 보기 중에 캐싱을 해제하거나, 서비스 팩을 업그레이드한 후 새 데이터 처리 확장 프로그램을 등록하는 경우 외에는 이 파일의 설정을 수정하지 마십시오.  
  
 렌더링 확장 프로그램 설정을 사용자 지정하는 경우 구성 파일 편집에 대한 특정 지침이 제공됩니다. 자세한 내용은 [RSReportServer.Config의 렌더링 확장 프로그램 매개 변수 사용자 지정](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)을 참조하세요.  
  
 구성 파일을 편집하는 방법에 대한 일반적인 지침은 [Reporting Services 구성 파일 수정&#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)을 참조하세요.  
  
## <a name="example-configuration-file"></a>구성 파일 예  
 다음 예에서는 RSReportDesigner.config 파일의 형식을 보여 줍니다.  
  
```  
<Configuration>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="InstanceName" Value="Microsoft.ReportingServices.PreviewServer" />  
  <Add Key="SessionCookies" Value="true" />  
  <Add Key="SessionTimeoutMinutes" Value="3" />  
  <Add Key="PolicyLevel" Value="rspreviewpolicy.config" />  
  <Add Key="CacheDataForPreview" Value="true" />  
  <Extensions>  
    <Render> . . . </Render>  
    <Data> . . . </Data>  
    <Designer> . . . </Designer>  
```  
  
## <a name="configuration-settings"></a>Configuration 설정  
  
|설정|설명|  
|-------------|-----------------|  
|**SecureConnectionLevel**|웹 서비스 연결 보안 수준을 지정합니다. 유효한 값은 0에서 3 사이이며 0은 보안 수준이 가장 낮습니다. 자세한 내용은 [Using Secure Web Service Methods](../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)을 참조하세요.|  
|**InstanceName**|미리 보기 서버의 식별자입니다. 이 값은 수정하지 마세요.|  
|**SessionCookies**|보고서 서버가 브라우저 쿠키를 사용하여 세션 정보를 유지 관리할지 여부를 지정합니다. 유효한 값은 **true** 및 **false**이고 기본값은 **true**입니다. 이 값을 false로 설정하면 세션 데이터가 **reportservertempdb** 데이터베이스에 저장됩니다.|  
|**SessionTimeoutMinutes**|세션 쿠키의 유효 기간을 지정합니다. 기본값은 3분입니다.|  
|**PolicyLevel**|보안 정책 구성 파일을 지정합니다. 유효한 값은 Rspreviewpolicy.config입니다. 자세한 내용은 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)을 참조하세요.|  
|**CacheDataForPreview**|**True**로 설정되어 있으면 보고서 디자이너는 로컬 컴퓨터에 캐시 파일의 데이터를 저장합니다. 유효한 값은 **True** (기본값) 및 **False**입니다. 자세한 내용은 [Previewing Reports](../../reporting-services/reports/previewing-reports.md)를 참조하세요.|  
|**Render**|미리 보기를 위해 보고서 디자이너에서 사용할 수 있는 렌더링 확장 프로그램을 열거합니다. 미리 보기에 사용된 렌더링 확장 프로그램 집합은 보고서 서버와 함께 설치된 렌더링 확장 프로그램과 동일해야 합니다.<br /><br /> **Name** 은 렌더링 확장 프로그램을 지정합니다. 코드를 통해 렌더링 확장 프로그램을 호출하는 경우 이 값을 사용하여 특정 확장 프로그램을 호출합니다.<br /><br /> **Type** 은 확장 프로그램 클래스의 정규화된 클래스 이름과 라이브러리 이름을 쉼표로 구분하여 지정합니다.<br /><br /> **Visible** 은 사용자 인터페이스에 이름을 표시할지 여부를 지정합니다. 이 값은 **True** (기본값)이거나 **False**입니다. **True**이면 사용자 인터페이스에 이름이 나타납니다.|  
|**Data**|보고서에 데이터를 제공하는 데이터 원본에 연결하기 위해 보고서 디자이너에서 사용할 수 있는 데이터 처리 확장 프로그램을 열거합니다. 보고서 디자이너에 사용된 데이터 처리 확장 프로그램 집합은 보고서 서버와 함께 설치된 데이터 처리 확장 프로그램과 동일해야 합니다. 사용자 지정 확장 프로그램을 추가 또는 제거하려면 [Deploying a Data Processing Extension](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)을 참조하십시오.<br /><br /> **Name** 은 데이터 처리 확장 프로그램을 지정합니다.<br /><br /> **Type** 은 확장 프로그램 클래스의 정규화된 클래스 이름과 라이브러리 이름을 쉼표로 구분하여 지정합니다.|  
|**Designer**|보고서 디자이너에서 사용할 수 있는 쿼리 작성기를 열거합니다. 쿼리 작성기는 보고서에 사용된 데이터를 검색하는 쿼리를 구성할 사용자 인터페이스를 제공합니다. 쿼리 작성기는 데이터 처리 확장 프로그램마다 다를 수 있습니다. 기본적으로 Reporting Services는 제품에 포함된 모든 데이터 처리 확장 프로그램용으로 하나의 시각적 데이터 도구 사용자 인터페이스를 제공합니다. 그러나 타사의 데이터 처리 확장 프로그램을 작성하거나 사용 중이면 다른 쿼리 작성기 인터페이스를 사용할 수 있습니다.|  
|**PreviewProcessingServiceStartupTimeoutSeconds**|오류 메시지를 표시하기 전에 미리 보기 처리 서비스가 시작될 때까지 기다릴 시간을 지정합니다. 기본값은 15초입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services 구성 파일](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [쿼리 디자인 도구&#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)  
  
  
