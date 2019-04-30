---
title: 표준 .NET Framework 데이터 공급자 등록(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- .NET Framework data providers for Reporting Services
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
ms.assetid: d92add64-e93c-4598-8508-55d1bc46acf6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 345b508f230fa6d566ae05919af2d4f43105dc8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63219257"
---
# <a name="register-a-standard-net-framework-data-provider-ssrs"></a>표준 .NET Framework 데이터 공급자 등록(SSRS)
  타사 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 사용하여 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 데이터 세트에 대한 데이터를 검색하려면 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자 어셈블리를 보고서 제작 클라이언트와 보고서 서버에 배포하고 등록해야 합니다. 보고서 제작 클라이언트에서 데이터 공급자를 데이터 원본 유형으로 등록하고 쿼리 디자이너와 연결해야 합니다. 그러면 보고서 데이터 세트를 만들 때 이 데이터 공급자를 데이터 원본 유형으로 선택할 수 있습니다. 연결된 쿼리 디자이너가 열려 이 데이터 원본 유형에 대한 쿼리 생성을 도와줍니다. 또한 보고서 서버에서 데이터 공급자를 데이터 원본 유형으로 등록해야 합니다. 그러면 이 데이터 공급자를 사용하여 데이터 원본에서 데이터를 검색하는 게시된 보고서를 처리할 수 있습니다.  
  
 타사 데이터 공급자가 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램에서 사용할 수 있는 모든 기능을 제공하지는 않습니다. 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../create-deploy-and-manage-mobile-and-paginated-reports.md)을 참조하세요. .[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자의 기능을 확장하는 방법은 [데이터 처리 확장 프로그램 구현](../extensions/data-processing/implementing-a-data-processing-extension.md)을 참조하세요.  
  
 데이터 공급자를 설치하고 등록하려면 관리자 자격 증명이 필요합니다.  
  
## <a name="registering-a-net-framework-data-provider-on-the-report-server"></a>보고서 서버에 .NET Framework 데이터 공급자 등록  
 보고서 서버에서 이 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 사용하는 게시된 보고서를 처리하려면 보고서 서버에 어셈블리를 설치해야 합니다. 두 개의 구성 파일을 수정해야 합니다. rsreportserver.config를 수정하여 데이터 공급자를 등록하고 rssrvpolicy.config를 수정하여 어셈블리에 대한 코드 액세스 보안 사용 권한을 부여합니다.  
  
#### <a name="to-install-a-data-provider-assembly-on-the-report-server"></a>보고서 서버에 데이터 공급자 어셈블리를 설치하려면  
  
1.  보고서 서버에서 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 사용할 bin 디렉터리의 기본 위치로 이동합니다. 보고서 서버 bin 디렉터리의 기본 위치는 *\<드라이브>*:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin입니다.  
  
2.  준비 위치에서 보고서 서버의 bin 디렉터리로 어셈블리를 복사합니다. 또는 GAC(전역 어셈블리 캐시)에 어셈블리를 로드할 수 있습니다. 자세한 내용은 MSDN에 있는 [SDK 설명서의](https://go.microsoft.com/fwlink/?linkid=63912) 어셈블리 및 전역 어셈블리 캐시 작업(Working with Assemblies and the Global Assembly Cache) [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 을 참조하십시오.  
  
#### <a name="to-register-a-net-data-provider-on-the-report-server"></a>보고서 서버에 .NET 데이터 공급자를 등록하려면  
  
1.  bin의 ReportServer 부모 디렉터리에 RSReportServer.config 파일의 백업을 만듭니다.  
  
2.  RSReportServer.config를 엽니다. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 메모장과 같은 간단한 텍스트 편집기를 사용하여 이 구성 파일을 열 수 있습니다.  
  
3.  RSReportServer.config 파일에서 `Data` 요소를 찾습니다. 다음 위치에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자에 대한 항목을 만들어야 합니다.  
  
    ```  
    <Extensions>  
       <Data>  
          <Extension Your data provider configuration information goes here />  
       </Data>  
    </Extensions>  
    ```  
  
4.  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자에 대한 항목을 추가합니다.  
  
    |attribute|Description|  
    |---------------|-----------------|  
    |`Name`|데이터 공급자의 고유 이름(예: **MyNETDataProvider**)을 제공합니다. `Name` 특성의 최대 길이는 255자입니다. 이름은 구성 파일의 `Extension` 요소에 있는 모든 항목 중에서 고유해야 합니다. 여기에 포함하는 값은 새 데이터 원본을 만들 때 데이터 원본 유형 드롭다운 목록에 표시됩니다.|  
    |`Type`|<xref:System.Data.IDbConnection> 인터페이스를 구현하는 클래스의 정규화된 네임스페이스 뒤에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자 어셈블리 이름(.dll 파일 확장명 포함 안 함)이 쉼표로 구분되어 결합된 목록을 입력합니다.|  
  
     예를 들어 보고서 서버 bin 디렉터리에 배포되는 DLL의 경우 다음과 같이 입력할 수 있습니다.  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly" />   
    ```  
  
     GAC(전역 어셈블리 캐시)에 어셈블리를 로드하는 경우 강력한 이름 속성을 제공해야 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly,Version=1.0.0.0, Culture=neutral, PublicKeyToken=MyPublicToken"/>  
    ```  
  
#### <a name="to-set-the-code-group-policy-for-a-net-data-provider"></a>.NET 데이터 공급자에 대한 코드 그룹 정책을 설정하려면  
  
1.  bin의 ReportServer 부모 디렉터리에 rssrvpolicy.config 파일의 백업 복사본을 만듭니다.  
  
2.  rssrvpolicy.config를 엽니다. [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 메모장과 같은 간단한 텍스트 편집기를 사용하여 이 구성 파일을 열 수 있습니다.  
  
3.  rssrvpolicy.config 파일에서 `CodeGroup` 요소를 찾습니다.  
  
4.  `FullTrust` 권한을 부여하는 데이터 공급자 어셈블리의 코드 그룹을 추가합니다. 코드 그룹은 다음과 같을 수 있습니다.  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="ThisDataProviderCodeGroup"  
       Description="Code group for the .NET data provider">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url=  
    "C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\DataProviderAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 멤버 자격은 데이터 공급자에 대해 선택할 수 있는 많은 멤버 자격 조건 중 하나일 뿐입니다.  
  
### <a name="verifying-the-deployment-and-registration"></a>배포 및 등록 확인  
 보고서 관리자를 열고 데이터 공급자가 사용 가능한 데이터 원본 목록에 포함되어 있는지 확인하여 데이터 공급자가 보고서 서버에 배포되었는지 확인할 수 있습니다. 보고서 관리자 및 데이터 원본에 대한 자세한 내용은 [공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)를 참조하세요.  
  
## <a name="registering-a-net-framework-data-provider-on-the-report-designer-client"></a>보고서 디자이너 클라이언트에 .NET Framework 데이터 공급자 등록  
 데이터 원본에 대해 이 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 사용하는 보고서를 작성하려면 보고서 디자이너를 실행하는 클라이언트 컴퓨터에 어셈블리를 설치해야 합니다. 두 개의 구성 파일을 수정해야 합니다. RSReportDesigner.config를 수정하여 데이터 공급자를 데이터 원본으로 등록하고 일반 쿼리 디자이너를 사용합니다. 또한 RSPreviewPolicy.config를 수정하여 데이터 공급자 어셈블리에 대한 코드 액세스 보안 사용 권한을 부여합니다.  
  
#### <a name="to-install-a-data-provider-assembly-on-the-report-designer-client"></a>보고서 디자이너 클라이언트에 데이터 공급자 어셈블리를 설치하려면  
  
1.  보고서 디자이너 클라이언트에서 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 사용할 PrivateAssemblies 디렉터리의 기본 위치로 이동합니다. PrivateAssemblies 디렉터리의 기본 위치는 *\<드라이브>*:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies입니다.  
  
2.  준비 위치에서 보고서 디자이너 클라이언트의 PrivateAssemblies 디렉터리로 어셈블리를 복사합니다. 또는 GAC(전역 어셈블리 캐시)에 어셈블리를 로드할 수 있습니다. 자세한 내용은 MSDN에 있는 [SDK 설명서의](https://go.microsoft.com/fwlink/?linkid=63912) 어셈블리 및 전역 어셈블리 캐시 작업(Working with Assemblies and the Global Assembly Cache) [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 을 참조하십시오.  
  
#### <a name="to-register-a-net-data-provider-on-the-report-designer-client"></a>보고서 디자이너 클라이언트에 .NET 데이터 공급자를 등록하려면  
  
1.  PrivateAssemblies 디렉터리에 RSReportDesigner.config 파일의 백업 복사본을 만듭니다.  
  
2.  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 메모장과 같은 간단한 텍스트 편집기를 사용하여 RSReportDesigner.config를 엽니다.  
  
3.  RSReportDesigner.config 파일에서 `Data` 요소를 찾습니다. 다음 위치에 데이터 공급자에 대한 항목을 만들어야 합니다.  
  
    ```  
    <Extensions>  
       <Data>  
          <Extension Your data provider configuration information goes here />  
       </Data>  
    </Extensions>  
    ```  
  
4.  데이터 공급자에 대한 항목을 추가합니다.  
  
    |attribute|Description|  
    |---------------|-----------------|  
    |`Name`|데이터 공급자의 고유 이름(예: **MyNETDataProvider**)을 제공합니다. `Name` 특성의 최대 길이는 255자입니다. 이름은 구성 파일의 `Extension` 요소에 있는 모든 항목 중에서 고유해야 합니다. 여기에 포함하는 값은 새 데이터 원본을 만들 때 데이터 원본 유형 드롭다운 목록에 표시됩니다.|  
    |`Type`|<xref:System.Data.IDbConnection> 인터페이스를 구현하는 클래스의 정규화된 네임스페이스 뒤에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자 어셈블리 이름(.dll 파일 확장명 포함 안 함)이 쉼표로 구분되어 결합된 목록을 입력합니다.|  
  
     예를 들어 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] PrivateAssemblies 디렉터리에 배포되는 DLL의 경우 다음과 같이 입력할 수 있습니다.  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly" />   
    ```  
  
     GAC에 어셈블리를 로드하는 경우 강력한 이름 속성을 제공해야 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly, Version=1.0.0.0, Culture=neutral, PublicKeyToken=MyPublicToken"/>  
    ```  
  
5.  RSReportDesigner.config 파일에서 `Designer` 요소를 찾습니다. 다음 위치에 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자에 대한 항목을 만들어야 합니다.  
  
    ```  
    <Extensions>  
       <Designer>  
          <Your data provider configuration information goes here>  
       </Designer>  
    </Extensions>  
    ```  
  
6.  RSReportDesigner.config 파일의 `Designer` 요소 아래에 다음 항목을 추가합니다. `Name` 특성만 이전 입력에서 제공한 이름으로 바꾸면 됩니다.  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
#### <a name="to-set-the-code-group-policy-for-a-net-data-provider-on-the-report-designer-client"></a>보고서 디자이너 클라이언트에서 .NET 데이터 공급자에 대한 코드 그룹 정책을 설정하려면  
  
1.  PrivateAssemblies 디렉터리에 RSPreviewPolicy.config 파일의 백업 복사본을 만듭니다.  
  
2.  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 메모장과 같은 간단한 텍스트 편집기를 사용하여 RSPreviewPolicy.config를 엽니다.  
  
3.  RSPreviewPolicy.config 파일에서 `CodeGroup` 요소를 찾습니다.  
  
4.  `FullTrust` 권한을 부여하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자 어셈블리의 코드 그룹을 추가합니다. 코드 그룹은 다음과 같을 수 있습니다.  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="ThisDataProviderCodeGroup"  
       Description="Code group for the .NET data provider">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url=  
    " C:\Program Files\Microsoft Visual Studio 9\Common7\IDE\PrivateAssemblies\DataProviderAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 멤버 자격은 데이터 공급자에 대해 선택할 수 있는 많은 멤버 자격 조건 중 하나일 뿐입니다.  
  
### <a name="verifying-the-deployment-and-registration-on-the-report-designer-client"></a>보고서 디자이너 클라이언트에서 배포 및 등록 확인  
 배포를 확인하려면 먼저 로컬 컴퓨터에서 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 인스턴스를 모두 닫아야 합니다. 현재 세션을 모두 종료한 후 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서 새 보고서 프로젝트를 만들어 데이터 공급자가 보고서 디자이너에 배포되었는지 확인할 수 있습니다. 이때 데이터 공급자는 보고서에 대한 새 데이터 집합을 만들 때 사용 가능한 데이터 원본 유형 목록에 포함되어 있어야 합니다.  
  
## <a name="platform-considerations"></a>플랫폼 고려 사항  
 64비트(x64) 플랫폼에서 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]는 32비트 WOW 모드로 실행됩니다. x64 플랫폼에서 보고서를 작성하는 경우 보고서를 미리 보려면 보고서 제작 클라이언트에 32비트 데이터 공급자가 설치되어 있어야 합니다. 동일한 시스템에 보고서를 게시하는 경우 보고서 관리자를 사용하여 보고서를 보려면 x64 데이터 공급자가 필요합니다.  
  
 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]는 [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] 기반 플랫폼에서 지원되지 않습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 와 함께 설치되는 데이터 처리 확장 프로그램은 각 플랫폼에 대해 기본적으로 컴파일되어야 하며 올바른 위치에 설치되어야 합니다. 또한 사용자 지정 데이터 공급자나 표준 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 등록하는 경우 이러한 공급자는 해당 플랫폼에 대해 기본적으로 컴파일되어야 하며 적절한 위치에 설치되어야 합니다. 32비트 플랫폼에서 실행하는 경우 데이터 공급자는 32비트 플랫폼에 대해 컴파일되어야 합니다. 64비트 플랫폼에서 실행하는 경우에는 데이터 공급자가 64비트 플랫폼에 대해 컴파일되어야 합니다. 64비트 인터페이스로 래핑된 32비트 데이터 공급자를 64비트 플랫폼에서 사용할 수는 없습니다. 설치된 플랫폼에서 데이터 공급자가 작동할지 여부에 대한 자세한 내용은 해당 타사 소프트웨어를 참조하십시오. 데이터 공급자 및 플랫폼 지원에 대한 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../create-deploy-and-manage-mobile-and-paginated-reports.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 구성 및 관리&#40;SSRS 기본 모드&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [데이터 처리 확장 프로그램 구현](../extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 구성 파일](../report-server/reporting-services-configuration-files.md)   
 [Reporting Services의 코드 액세스 보안](../extensions/secure-development/code-access-security-in-reporting-services.md)  
  
  
