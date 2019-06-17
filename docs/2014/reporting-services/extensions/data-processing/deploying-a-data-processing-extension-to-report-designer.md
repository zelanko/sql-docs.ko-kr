---
title: '방법: 보고서 디자이너에 데이터 처리 확장 프로그램 배포 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: 3614e601-004e-4a16-8388-836ffd67e9dd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 947ad59b8ac20862a8ef6da8ea527e2befb1be57
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63164322"
---
# <a name="how-to-deploy-a-data-processing-extension-to-report-designer"></a>방법: 보고서 디자이너에 데이터 처리 확장 프로그램 배포
  보고서 디자이너에서는 보고서를 디자인하는 동안 데이터 검색 및 처리를 위해 데이터 처리 확장 프로그램을 사용합니다. 데이터 처리 확장 프로그램 어셈블리를 보고서 디자이너에 프라이빗 어셈블리로 배포해야 합니다. 또한 보고서 디자이너 구성 파일인 RSReportDesigner.config에서 항목을 만들어야 합니다.  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>데이터 처리 확장 프로그램 어셈블리를 배포하려면  
  
1.  준비 위치에서 보고서 디자이너 디렉터리로 어셈블리를 복사합니다. 보고서 디자이너 디렉터리의 기본 위치는 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies입니다.  
  
2.  어셈블리 파일이 복사된 후 RSReportDesigner.config 파일을 엽니다. RSReportDesigner.config 파일도 보고서 디자이너 디렉터리에 있습니다. 구성 파일에서 데이터 처리 확장 프로그램 어셈블리 파일에 대한 항목을 만들어야 합니다. 구성 파일은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서 열거나 메모장과 같은 간단한 텍스트 편집기를 사용하여 열 수 있습니다.  
  
3.  RSReportDesigner.config 파일에서 **Data** 요소를 찾습니다. 새로 만든 데이터 처리 확장 프로그램에 대한 항목이 다음 위치에 만들어져 있습니다.  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  포함 하는 데이터 처리 확장 프로그램에 대 한 항목을 추가 **확장** 에 대 한 값이 있는 요소를 `Name`를 `Type`, 및 `Visible` 특성입니다. 항목은 다음과 같습니다.  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, AssemblyName" />  
    ```  
  
     `Name`의 값은 데이터 처리 확장 프로그램의 고유한 이름입니다. `Type`의 값은 <xref:Microsoft.ReportingServices.Interfaces.IExtension> 및 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 인터페이스를 구현하는 클래스의 정규화된 네임스페이스에 대한 항목과 그 다음에 어셈블리의 이름(.dll 파일 확장명 포함 안 함)이 따라오는 형태가 포함되며 쉼표로 구분된 목록입니다. 기본적으로 데이터 처리 확장 프로그램은 표시됩니다. 보고서 디자이너와 같은 사용자 인터페이스에 확장 프로그램을 숨기려면 추가 `Visible` 특성을 합니다 **확장** 요소인으로 설정 `false`.  
  
5.  마지막으로 확장 프로그램에 대해 **FullTrust** 권한을 부여하는 사용자 지정 어셈블리에 대한 코드 그룹을 추가합니다. 기본 위치가 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies인 rspreviewpolicy.config 파일에 코드 그룹을 추가하면 됩니다. 코드 그룹은 다음과 같습니다.  
  
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
  
 URL 멤버 자격은 데이터 처리 확장 프로그램에 대해 선택할 수 있는 다수의 멤버 자격 조건 중 하나일 뿐입니다. [!INCLUDE[ssRSversion2005](../../../includes/ssrsversion2005-md.md)]의 코드 액세스 보안에 대한 자세한 내용은 [보안 개발&#40;Reporting Services&#41;](../secure-development/secure-development-reporting-services.md)을 참조하세요.  
  
## <a name="generic-query-designer"></a>일반 쿼리 디자이너  
 보고서 디자이너는 사용자 지정 데이터 처리 확장 프로그램에서 사용할 수 있는 일반 쿼리 디자이너를 제공합니다. 이 디자이너는 쿼리 창과 결과 창의 두 창으로 구성되어 있습니다. 일반 디자이너를 사용하여 그래픽 인터페이스에서 지원되지 않는 쿼리를 작성할 수 있습니다. 일반 쿼리 디자이너는 그래픽 쿼리 디자이너와 달리 쿼리 구문을 확인하거나 쿼리를 재구성하지 않습니다.  
  
#### <a name="to-enable-the-generic-query-designer-for-a-custom-extension"></a>사용자 지정 확장 프로그램에 대해 일반 쿼리 디자이너를 사용하려면  
  
-   아래에 있는 RSReportDesigner.config 파일에 다음 항목을 추가 합니다 **디자이너** 요소를 대체 합니다 `Name` 이전 항목에서 제공한 이름 사용 하 여 특성.  
  
    ```  
    <Extension Name="ExtensionName" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
## <a name="verifying-the-deployment"></a>배포 확인  
 배포를 확인하려면 먼저 로컬 컴퓨터에서 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 인스턴스를 모두 닫아야 합니다. 현재 세션을 모두 종료한 후 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]에서 새 보고서 프로젝트를 만들어 데이터 처리 확장 프로그램이 보고서 디자이너에 배포되었는지 확인할 수 있습니다. 이때 확장 프로그램이 보고서에 대한 새 데이터 집합을 만들 때 사용 가능한 데이터 원본 유형 목록에 포함되어 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 처리 확장 프로그램 배포](deploying-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램](../reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
