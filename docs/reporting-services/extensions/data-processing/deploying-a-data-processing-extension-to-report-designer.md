---
title: "방법: 보고서 디자이너에 데이터 처리 확장 프로그램 배포 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 3614e601-004e-4a16-8388-836ffd67e9dd
caps.latest.revision: 41
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 42974101d21082568442d73d063de1d1b937c428
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="deploying-a-data-processing-extension-to-report-designer"></a>보고서 디자이너에 데이터 처리 확장 프로그램 배포
  보고서 디자이너에서는 보고서를 디자인하는 동안 데이터 검색 및 처리를 위해 데이터 처리 확장 프로그램을 사용합니다. 데이터 처리 확장 프로그램 어셈블리를 보고서 디자이너에 전용 어셈블리로 배포해야 합니다. 또한 보고서 디자이너 구성 파일인 RSReportDesigner.config에서 항목을 만들어야 합니다.  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>데이터 처리 확장 프로그램 어셈블리를 배포하려면  
  
1.  준비 위치에서 보고서 디자이너 디렉터리로 어셈블리를 복사합니다. 보고서 디자이너 디렉터리의 기본 위치는 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies입니다.  
  
2.  어셈블리 파일이 복사된 후 RSReportDesigner.config 파일을 엽니다. RSReportDesigner.config 파일도 보고서 디자이너 디렉터리에 있습니다. 구성 파일에서 데이터 처리 확장 프로그램 어셈블리 파일에 대한 항목을 만들어야 합니다. 구성 파일을 열면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 또는 메모장과 같은 간단한 텍스트 편집기를 사용 합니다.  
  
3.  RSReportDesigner.config 파일에서 **Data** 요소를 찾습니다. 새로 만든 데이터 처리 확장 프로그램에 대한 항목이 다음 위치에 만들어져 있습니다.  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  포함 하는 데이터 처리 확장 프로그램에 대 한 항목을 추가 **확장** 에 대 한 값이 있는 요소는 **이름**, **형식**, 및 **Visible** 특성입니다. 항목은 다음과 같습니다.  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, AssemblyName" />  
    ```  
  
     에 대 한 값 **이름** 데이터 처리 확장 프로그램의 고유 이름입니다. 에 대 한 값 **형식** 구현 하는 클래스의 정규화 된 네임 스페이스에 대 한 항목을 포함 하는 쉼표로 구분 된 목록에서 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 및 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 인터페이스, 어셈블리 (.dll 파일 확장명 제외)의 이름이 차례로 나옵니다. 기본적으로 데이터 처리 확장 프로그램은 표시됩니다. 보고서 디자이너와 같은 사용자 인터페이스에 확장 프로그램을 숨기려면 추가 **Visible** 특성을 **확장** 요소를이 속성을 설정 하 고 **false**합니다.  
  
5.  마지막으로, 권한을 부여 하는 사용자 지정 어셈블리에 대 한 코드 그룹을 추가 **FullTrust** 확장 프로그램에 대 한 권한이 있습니다. 기본 위치가 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies인 rspreviewpolicy.config 파일에 코드 그룹을 추가하면 됩니다. 코드 그룹은 다음과 같습니다.  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 멤버 자격은 데이터 처리 확장 프로그램에 대해 선택할 수 있는 다수의 멤버 자격 조건 중 하나일 뿐입니다. 코드 액세스 보안에 대 한 자세한 내용은 [!INCLUDE[ssRSversion2005](../../../includes/ssrsversion2005-md.md)], 참조 [보안 개발 &#40; Reporting services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
## <a name="generic-query-designer"></a>일반 쿼리 디자이너  
 보고서 디자이너는 사용자 지정 데이터 처리 확장 프로그램에서 사용할 수 있는 일반 쿼리 디자이너를 제공합니다. 이 디자이너는 쿼리 창과 결과 창의 두 창으로 구성되어 있습니다. 일반 디자이너를 사용하여 그래픽 인터페이스에서 지원되지 않는 쿼리를 작성할 수 있습니다. 일반 쿼리 디자이너는 그래픽 쿼리 디자이너와 달리 쿼리 구문을 확인하거나 쿼리를 재구성하지 않습니다.  
  
#### <a name="to-enable-the-generic-query-designer-for-a-custom-extension"></a>사용자 지정 확장 프로그램에 대해 일반 쿼리 디자이너를 사용하려면  
  
-   다음 항목 아래에 있는 RSReportDesigner.config 파일을 추가 **디자이너** 요소를 교체는 **이름** 이전 항목에서 제공 하는 이름 가진 특성입니다.  
  
    ```  
    <Extension Name="ExtensionName" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
## <a name="verifying-the-deployment"></a>배포 확인  
 배포를 확인하려면 먼저 로컬 컴퓨터에서 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 인스턴스를 모두 닫아야 합니다. 현재 세션을 모두 종료한 후 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서 새 보고서 프로젝트를 만들어 데이터 처리 확장 프로그램이 보고서 디자이너에 배포되었는지 확인할 수 있습니다. 이때 확장 프로그램이 보고서에 대한 새 데이터 집합을 만들 때 사용 가능한 데이터 원본 유형 목록에 포함되어 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
