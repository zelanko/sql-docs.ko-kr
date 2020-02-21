---
title: '방법: 데이터 처리 확장 프로그램을 보고서 서버에 배포 | Microsoft Docs'
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: e00dface-70f8-434b-9763-8ebee18737d2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3f0b775b53244cd0a428bb4ce4023906d2f5119
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63194130"
---
# <a name="deploying-a-data-processing-extension-to-a-report-server"></a>보고서 서버에 데이터 처리 확장 프로그램 배포
  보고서 서버는 렌더링된 보고서의 데이터 검색 및 처리를 위해 데이터 처리 확장 프로그램을 사용합니다. 데이터 처리 확장 프로그램 어셈블리를 보고서 서버에 프라이빗 어셈블리로 배포해야 합니다. 또한 보고서 서버 구성 파일 RSReportServer.config에서 항목을 만들어야 합니다.  
  
## <a name="procedures"></a>프로시저  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>데이터 처리 확장 프로그램 어셈블리를 배포하려면  
  
1.  준비 위치에서 데이터 처리 확장 프로그램을 사용할 보고서 서버의 bin 디렉터리로 어셈블리를 복사합니다. 보고서 서버 bin 디렉터리의 기본 위치는 %ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<*Instance Name*>\Reporting Services\ReportServer\bin입니다.  
  
    > [!NOTE]  
    >  이 단계를 수행하면 SQL Server의 최신 인스턴스로 업그레이드할 수 없게 됩니다. 자세한 내용은 [Upgrade and Migrate Reporting Services](../../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하세요.  
  
2.  어셈블리 파일이 복사된 후 RSReportServer.config 파일을 엽니다. RSReportServer.config 파일은 ReportServer 디렉터리에 있습니다. 구성 파일에서 데이터 처리 확장 프로그램 어셈블리 파일에 대한 항목을 만들어야 합니다. 구성 파일은 Visual Studio 또는 메모장과 같은 간단한 텍스트 편집기를 사용하여 열 수 있습니다.  
  
3.  RSReportServer.config 파일에서 **Data** 요소를 찾습니다. 새로 만든 데이터 처리 확장 프로그램에 대한 항목이 다음 위치에 만들어져 있습니다.  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  데이터 처리 확장 프로그램에 대한 항목을 추가합니다. 항목에 **Name** 및 **Type**에 대한 값이 있는 **Extension** 요소가 포함되어야 하며 다음과 같습니다.  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, MyExtensionAssembly" />  
    ```  
  
     **Name**의 값은 데이터 처리 확장 프로그램의 고유한 이름입니다. **Type**의 값은 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 및 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 인터페이스를 구현하는 클래스의 정규화된 네임스페이스에 대한 항목과 그 다음에 어셈블리의 이름(.dll 파일 확장명 포함 안 함)이 따라오는 형태가 포함되며 쉼표로 구분된 목록입니다. 기본적으로 데이터 처리 확장 프로그램은 표시됩니다. 보고서 관리자와 같은 사용자 인터페이스에 확장 프로그램이 표시되지 않도록 숨기려면 **Visible** 특성을 **Extension** 요소에 추가하고 **false**로 설정합니다.  
  
5.  마지막으로 확장 프로그램에 대해 **FullTrust** 권한을 부여하는 사용자 지정 어셈블리에 대한 코드 그룹을 추가합니다. 기본적으로 %ProgramFiles%\Microsoft SQL Server\\<MSRS10_50.\<*Instance Name*>\Reporting Services\ReportServer에 있는 rssrvpolicy.config 파일에 코드 그룹을 추가하여 이 작업을 수행할 수 있습니다. 코드 그룹은 다음과 같습니다.  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<Instance Name>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 멤버 자격은 데이터 처리 확장 프로그램에 대해 선택할 수 있는 다수의 멤버 자격 조건 중 하나일 뿐입니다. [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 코드 액세스 보안에 대한 자세한 내용은 [보안 개발&#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)을 참조하세요.  
  
## <a name="verifying-the-deployment"></a>배포 확인  
 웹 서비스 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 메서드를 사용하여 데이터 처리 확장 프로그램이 보고서 서버에 성공적으로 배포되었는지 여부를 확인할 수 있습니다. 보고서 관리자를 열고 확장 프로그램이 사용 가능한 데이터 원본 목록에 포함되어 있는지 확인할 수도 있습니다. 보고서 관리자 및 데이터 원본에 대한 자세한 내용은 [공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](../../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
