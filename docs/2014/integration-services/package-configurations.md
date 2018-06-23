---
title: 패키지 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- package configuration syntax [Integration Services]
- SQL Server Integration Services packages, configurations
- SSIS packages, configurations
- XML [Integration Services]
- Integration Services packages, configurations
- configuration syntax [Integration Services]
- indirect configurations [Integration Services]
- configurations [Integration Services]
- direct configurations [Integration Services]
- packages [Integration Services], configurations
ms.assetid: d20e0311-1fc9-4ddc-a381-6d127cf11b69
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b3b80e197cedae2b8a9902b8e3de4f9066fab374
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36082324"
---
# <a name="package-configurations"></a>패키지 구성
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 런타임 시 속성의 값을 업데이트 하는 데 사용할 수 있는 패키지 구성을 제공 합니다.  
  
> [!NOTE]  
>  구성은 패키지 배포 모델에 사용할 수 있습니다. 매개 변수는 프로젝트 배포 모델에 대한 구성 대신 사용됩니다. 프로젝트 배포 모델을 사용하면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하십시오.  
  
 구성은 완성된 패키지에 추가하는 속성/값 쌍입니다. 일반적으로 패키지 개발 과정에서 패키지 개체의 패키지 집합 속성을 만든 다음 해당 패키지에 구성을 추가합니다. 패키지가 실행될 때는 구성의 새 속성 값이 사용됩니다. 예를 들어 구성을 사용하여 연결 관리자의 연결 문자열을 변경하거나 변수 값을 업데이트할 수 있습니다.  
  
 패키지 구성을 사용하면 다음과 같은 이점이 있습니다.  
  
-   구성을 사용하면 개발 환경에서 프로덕션 환경으로 패키지를 쉽게 이동할 수 있습니다. 예를 들어 구성으로 원본 파일의 경로를 업데이트하거나 데이터베이스 또는 서버의 이름을 변경할 수 있습니다.  
  
-   구성은 패키지를 여러 다른 서버로 배포할 때 유용합니다. 예를 들어 배포된 각 패키지 구성의 변수가 다른 디스크 공간 값을 포함할 수 있으며 사용 가능한 디스크 공간이 이 값을 충족하지 않을 경우 패키지가 실행되지 않습니다.  
  
-   구성은 패키지를 좀 더 융통성 있게 만듭니다. 예를 들어 구성으로 속성 식에서 사용되는 변수의 값을 업데이트할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] XML 파일과 같은 패키지 구성 저장의 여러 가지 방법을 지원, 테이블에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 및 환경 및 패키지 변수입니다.  
  
 각 구성은 한 개의 속성/값 쌍입니다. XML 구성 파일 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 유형은 여러 구성을 포함할 수 있습니다.  
  
 패키지 설치를 위한 패키지 배포 유틸리티를 만드는 경우 구성이 포함됩니다. 패키지를 설치하는 경우 패키지 설치 단계의 하나로 구성이 업데이트됩니다.  
  
## <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>런타임에 패키지 구성이 적용되는 방법 이해  
 **dtexec** 명령 프롬프트 유틸리티(dtexec.exe)를 사용하여 배포된 패키지를 실행할 때 유틸리티에서는 패키지 구성을 두 번 적용합니다. 즉, 명령줄에서 지정한 옵션을 적용하기 전과 후 모두에 구성을 적용합니다.  
  
 유틸리티에서 패키지를 로드 및 실행할 때 이벤트가 다음과 같은 순서로 발생됩니다.  
  
1.  **dtexec** 유틸리티가 패키지를 로드합니다.  
  
2.  유틸리티가 패키지에서 디자인 타임에 지정한 구성을 패키지에 지정된 순서로 적용합니다. 부모 패키지 변수 구성만은 예외적으로 프로세스의 후반에 한 번만 적용됩니다.  
  
3.  그런 다음 명령줄에서 지정한 옵션을 유틸리티가 적용합니다.  
  
4.  그런 다음 유틸리티가 패키지에서 디자인 타임에 지정한 구성을 패키지에 지정된 순서로 다시 로드합니다. 마찬가지로 부모 패키지 변수 구성만은 예외적으로 이 규칙을 따르지 않습니다. 유틸리티는 명령줄에서 지정한 명령줄 옵션을 사용하여 구성을 다시 로드합니다. 따라서 다른 위치에서 다른 값이 다시 로드될 수 있습니다.  
  
5.  유틸리티가 부모 패키지 변수 구성을 적용합니다.  
  
6.  유틸리티가 패키지를 실행합니다.  
  
 **dtexec** 유틸리티가 구성을 적용하는 방법은 다음과 같은 명령줄 옵션에 영향을 줍니다.  
  
-   런타임에 **/Connection** 또는 **/Set** 옵션을 사용하면 디자인 타임에 지정한 위치와 다른 위치에서 패키지 구성을 로드할 수 있습니다.  
  
-   **/ConfigFile** 옵션을 사용하면 디자인 타임에 지정하지 않은 추가 구성을 로드할 수 있습니다.  
  
 그러나 이러한 명령줄 옵션에는 몇 가지 제한 사항이 있습니다.  
  
-   **/Set** 또는 **/Connection** 옵션을 사용하여 구성에서도 설정된 단일 값을 재정의할 수는 없습니다.  
  
-   **/ConfigFile** 옵션을 사용하여 디자인 타임에 지정한 구성을 대체하는 구성을 로드할 수는 없습니다.  
  
 이러한 옵션과 이러한 옵션의 동작이 간에 어떻게 다른 지에 대 한 자세한 내용은 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 이전 버전에서는 참조 및 [SQL Server 2014에서 Integration Services 기능의 동작 변경 내용](../../2014/integration-services/behavior-changes-to-integration-services-features-in-sql-server-2014.md)합니다.  
  
## <a name="package-configuration-types"></a>패키지 구성 유형  
 다음 표에서는 패키지 구성 유형에 대해 설명합니다.  
  
|형식|Description|  
|----------|-----------------|  
|XML 구성 파일|구성을 포함하는 XML 파일입니다. XML 파일은 여러 구성을 포함할 수 있습니다.|  
|환경 변수|환경 변수는 구성을 포함합니다.|  
|레지스트리 항목|레지스트리 항목은 구성을 포함합니다.|  
|부모 패키지 변수|패키지 변수는 구성을 포함합니다. 이 구성 유형은 일반적으로 자식 패키지에서 속성을 업데이트하기 위해 사용됩니다.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블|구성을 포함하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 테이블입니다. 테이블은 여러 구성을 포함할 수 있습니다.|  
  
### <a name="xml-configuration-files"></a>XML 구성 파일  
 **XML 구성 파일** 의 구성 유형을 선택한 경우 새 구성 파일을 만들고 기존의 파일을 다시 사용하면서 새 구성을 추가하거나 또는 기존의 파일을 다시 사용하지만 기존의 파일 내용을 덮어쓸 수 있습니다.  
  
 XML 구성 파일은 두 개의 부분으로 이루어집니다.  
  
-   제목은 구성 파일 자체에 대한 정보를 포함합니다. 이 요소는 파일을 만든 시각과 같은 특성 및 파일을 만든 사람의 이름을 포함합니다.  
  
-   구성 요소는 각 구성에 대한 정보를 포함합니다. 이 요소는 속성 경로 및 속성의 구성 값과 같은 특성을 포함합니다.  
  
 다음 XML 코드에서는 XML 구성 파일의 구문을 보여 줍니다. 이 예에서는 `MyVar`라는 정수 변수의 Value 속성에 대한 구성을 보여 줍니다.  
  
```  
<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
### <a name="registry-entry"></a>레지스트리 항목  
 레지스트리 항목을 사용하여 구성을 저장하려면 기존 키를 사용하거나 HKEY_CURRENT_USER에서 새 키를 만들 수 있습니다. 레지스트리 키를 사용 하면 명명 된 값이 있어야 합니다. `Value`합니다. 값은 DWORD 또는 문자열이 될 수 있습니다.  
  
 **레지스트리 항목** 구성 유형을 선택할 경우 레지스트리 항목 상자에 레지스트리 키의 이름을 입력합니다. 형식은 \<레지스트리 키>입니다. HKEY_CURRENT_USER의 루트에 없는 레지스트리 키를 사용하려면 \<레지스트리 키\레지스트리 키\\...> 형식을 사용하여 키를 식별합니다. 예를 들어 SSISPackages에 있는 MyPackage 키를 사용 하려면 입력 `SSISPackages\MyPackage`합니다.  
  
### <a name="sql-server"></a>SQL Server  
 **SQL Server** 구성 유형을 선택한 경우 구성을 저장할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결을 지정하십시오. 기존 테이블에 구성을 저장하거나 지정한 데이터베이스에 새 테이블을 만들 수 있습니다.  
  
 다음 SQL 문에서는 패키지 구성 마법사가 제공하는 기본 CREATE TABLE 문을 보여 줍니다.  
  
```  
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 구성에 지정한 이름은 **ConfigurationFilter** 열에 저장된 값입니다.  
  
## <a name="direct-and-indirect-configurations"></a>직접 및 간접 구성  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 직접 및 간접 구성을 제공합니다. 구성을 직접으로 지정한 경우 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 구성 항목 및 패키지 개체 속성 간에 직접 연결을 만듭니다. 직접 구성은 원본의 위치가 변경되지 않는 경우에 적합합니다. 예를 들어 패키지의 모든 배포가 동일한 파일 경로를 사용하는 경우 XML 구성 파일을 지정할 수 있습니다.  
  
 간접 구성은 환경 변수를 사용합니다. 구성 설정을 직접 지정하는 대신 구성이 구성 값을 포함하는 환경 변수를 가리킵니다. 간접 구성은 각 패키지의 배포에 대해 구성 위치가 변경될 수 있는 경우에 적합합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [패키지 구성 만들기](../../2014/integration-services/create-package-configurations.md)  
  
## <a name="related-content"></a>관련 내용  
  
-   msdn.microsoft.com의 기술 문서 - [Integration Services 패키지 구성 이해](http://go.microsoft.com/fwlink/?LinkId=165643)   
  
-   www.sqlis.com의 블로그 항목, [코드에 패키지 만들기 – 패키지 구성](http://go.microsoft.com/fwlink/?LinkId=217663)  
  
-   blogs.msdn.com의 블로그 항목 - [API 예제 – 구성 파일을 패키지에 프로그래밍 방식으로 추가](http://go.microsoft.com/fwlink/?LinkId=217664)  
  
  