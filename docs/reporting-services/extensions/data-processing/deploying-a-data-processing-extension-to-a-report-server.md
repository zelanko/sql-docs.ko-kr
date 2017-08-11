---
title: "방법: 보고서 서버에 데이터 처리 확장 프로그램 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: e00dface-70f8-434b-9763-8ebee18737d2
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: a60c685ebdfd9d549e100cf5b5eda0ab056c1c46
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="deploying-a-data-processing-extension-to-a-report-server"></a>보고서 서버에 데이터 처리 확장 프로그램 배포
  보고서 서버는 렌더링된 보고서의 데이터 검색 및 처리를 위해 데이터 처리 확장 프로그램을 사용합니다. 데이터 처리 확장 프로그램 어셈블리를 보고서 서버에 전용 어셈블리로 배포해야 합니다. 또한 보고서 서버 구성 파일 RSReportServer.config에서 항목을 만들어야 합니다.  
  
## <a name="procedures"></a>절차  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>데이터 처리 확장 프로그램 어셈블리를 배포하려면  
  
1.  준비 위치에서 데이터 처리 확장 프로그램을 사용할 보고서 서버의 bin 디렉터리로 어셈블리를 복사합니다. 보고서 서버 bin 디렉터리의 기본 위치는 %ProgramFiles%\Microsoft SQL Server\MSRS10_50입니다. \< *인스턴스 이름을*> services\reportserver\bin입니다.  
  
    > [!NOTE]  
    >  이 단계를 수행하면 SQL Server의 최신 인스턴스로 업그레이드할 수 없게 됩니다. 자세한 내용은 [Upgrade and Migrate Reporting Services](../../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)을 참조하세요.  
  
2.  어셈블리 파일이 복사된 후 RSReportServer.config 파일을 엽니다. RSReportServer.config 파일은 ReportServer 디렉터리에 있습니다. 구성 파일에서 데이터 처리 확장 프로그램 어셈블리 파일에 대한 항목을 만들어야 합니다. Visual Studio 또는 메모장과 같은 간단한 텍스트 편집기와 함께 구성 파일을 열 수 있습니다.  
  
3.  RSReportServer.config 파일에서 **Data** 요소를 찾습니다. 새로 만든 데이터 처리 확장 프로그램에 대한 항목이 다음 위치에 만들어져 있습니다.  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  데이터 처리 확장 프로그램에 대한 항목을 추가합니다. 입력 한 내용을 포함 되어야는 **확장** 에 대 한 값이 있는 요소 **이름** 및 **형식** 하며 다음과 같습니다.  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, MyExtensionAssembly" />  
    ```  
  
     에 대 한 값 **이름** 데이터 처리 확장 프로그램의 고유 이름입니다. 에 대 한 값 **형식** 구현 하는 클래스의 정규화 된 네임 스페이스에 대 한 항목을 포함 하는 쉼표로 구분 된 목록에서 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 및 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 인터페이스, 어셈블리 (.dll 파일 확장명 제외)의 이름이 차례로 나옵니다. 기본적으로 데이터 처리 확장 프로그램은 표시됩니다. 보고서 관리자와 같은 사용자 인터페이스에 확장 프로그램이 표시되지 않도록 숨기려면 **Visible** 특성을 **Extension** 요소에 추가하고 **false**로 설정합니다.  
  
5.  권한을 부여 하는 사용자 지정 어셈블리에 대 한 코드 그룹을 추가 **FullTrust** 확장 프로그램에 대 한 권한이 있습니다. 기본적으로 %ProgramFiles%\Microsoft SQL Server에에서 rssrvpolicy.config 파일에 코드 그룹을 추가 하 여이 작업을 수행\\< MSRS10_50.\< *인스턴스 이름을*> services\reportserver입니다. 코드 그룹은 다음과 같습니다.  
  
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
  
 URL 멤버 자격은 데이터 처리 확장 프로그램에 대해 선택할 수 있는 다수의 멤버 자격 조건 중 하나일 뿐입니다. 코드 액세스 보안에 대 한 자세한 내용은 [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], 참조 [보안 개발 &#40; Reporting services&#41; ](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
## <a name="verifying-the-deployment"></a>배포 확인  
 웹 서비스 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 메서드를 사용하여 데이터 처리 확장 프로그램이 보고서 서버에 성공적으로 배포되었는지 여부를 확인할 수 있습니다. 보고서 관리자를 열고 확장 프로그램이 사용 가능한 데이터 원본 목록에 포함되어 있는지 확인할 수도 있습니다. 보고서 관리자 및 데이터 원본에 대한 자세한 내용은 [공유 데이터 원본 만들기, 수정 및 삭제&#40;SSRS&#41;](../../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
