---
title: 레거시 패키지 배포(SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.packageconfigurationorganizer.f1
- sql13.dts.configwizard.finishdtsconfiguration.f1
- sql13.dts.configwizard.selectobjects.f1
- sql13.dts.configwizard.selecconfigtype.f1
- sql13.dts.configwizard.welcome.f1
- sql13.dts.deploymentwizard.welcome.f1
- sql13.dts.deploymentwizard.confirminstallation.f1
- sql13.dts.deploymentwizard.deploydtspackages.f1
- sql13.dts.deploymentwizard.finish.f1
- sql13.dts.deploymentwizard.configurepackages.f1
- sql13.dts.deploymentwizard.selectinstfolder.f1
- sql13.dts.deploymentwizard.packagevalidation.f1
- sql13.dts.deploymentwizard.specifytargetsqlserver.f1
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1ce860d112f171e4cc341c2b2e2b03149720e6b9
ms.sourcegitcommit: 4b775a3ce453b757c7435cc2a4c9b35d0c5a8a9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87472509"
---
# <a name="legacy-package-deployment-ssis"></a>레거시 패키지 배포(SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에는 패키지를 배포 컴퓨터에서 프로덕션 서버나 다른 컴퓨터로 손쉽게 배포할 수 있는 도구와 마법사가 포함되어 있습니다.  
  
 패키지 배포 과정은 다음 네 단계로 구성됩니다.  
  
1.  첫 번째 단계는 선택 사항입니다. 이 단계에서는 런타임에 패키지 요소의 속성을 업데이트하는 패키지 구성을 만듭니다. 구성은 패키지를 배포할 때 자동으로 포함됩니다.  
  
2.  두 번째 단계는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 빌드하여 패키지 배포 유틸리티를 만드는 것입니다. 프로젝트의 배포 유틸리티에는 배포할 패키지가 포함됩니다.  
  
3.  세 번째 단계는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 빌드할 때 생성된 배포 폴더를 대상 컴퓨터로 복사하는 것입니다.  
  
4.  네 번째 단계는 대상 컴퓨터에서 패키지 설치 마법사를 실행하여 파일 시스템이나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 패키지를 설치하는 것입니다.  

## <a name="package-configurations"></a>패키지 구성
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 런타임에 속성 값을 업데이트하는 데 사용할 수 있는 패키지 구성을 제공합니다.  
  
> **참고:** 구성은 패키지 배포 모델에 사용할 수 있습니다. 매개 변수는 프로젝트 배포 모델에 대한 구성 대신 사용됩니다. 프로젝트 배포 모델을 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)를 참조하십시오.   
  
 구성은 완성된 패키지에 추가하는 속성/값 쌍입니다. 일반적으로 패키지 개발 과정에서 패키지 개체의 패키지 집합 속성을 만든 다음 해당 패키지에 구성을 추가합니다. 패키지가 실행될 때는 구성의 새 속성 값이 사용됩니다. 예를 들어 구성을 사용하여 연결 관리자의 연결 문자열을 변경하거나 변수 값을 업데이트할 수 있습니다.  
  
 패키지 구성을 사용하면 다음과 같은 이점이 있습니다.  
  
-   구성을 사용하면 개발 환경에서 프로덕션 환경으로 패키지를 쉽게 이동할 수 있습니다. 예를 들어 구성으로 원본 파일의 경로를 업데이트하거나 데이터베이스 또는 서버의 이름을 변경할 수 있습니다.  
  
-   구성은 패키지를 여러 다른 서버로 배포할 때 유용합니다. 예를 들어 배포된 각 패키지 구성의 변수가 다른 디스크 공간 값을 포함할 수 있으며 사용 가능한 디스크 공간이 이 값을 충족하지 않을 경우 패키지가 실행되지 않습니다.  
  
-   구성은 패키지를 좀 더 융통성 있게 만듭니다. 예를 들어 구성으로 속성 식에서 사용되는 변수의 값을 업데이트할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 XML 파일, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 테이블, 환경 변수 및 패키지 변수와 같은 여러 가지 패키지 구성 저장 방식을 지원합니다.  
  
 각 구성은 한 개의 속성/값 쌍입니다. XML 구성 파일 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 유형은 여러 구성을 포함할 수 있습니다.  
  
 패키지 설치를 위한 패키지 배포 유틸리티를 만드는 경우 구성이 포함됩니다. 패키지를 설치하는 경우 패키지 설치 단계의 하나로 구성이 업데이트됩니다.  
  
### <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>런타임에 패키지 구성이 적용되는 방법 이해  
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
  
 이러한 옵션에 대한 자세한 내용과 이러한 옵션의 동작이 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 및 이전 버전 간에 어떻게 다른지에 대한 자세한 내용은 [SQL Server 2016 Integration Services 기능의 동작 변경](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)을 참조하세요.  
  
### <a name="package-configuration-types"></a>패키지 구성 유형  
 다음 표에서는 패키지 구성 유형에 대해 설명합니다.  
  
|Type|Description|  
|----------|-----------------|  
|XML 구성 파일|구성을 포함하는 XML 파일입니다. XML 파일은 여러 구성을 포함할 수 있습니다.|  
|환경 변수|환경 변수는 구성을 포함합니다.|  
|레지스트리 항목|레지스트리 항목은 구성을 포함합니다.|  
|부모 패키지 변수|패키지 변수는 구성을 포함합니다. 이 구성 유형은 일반적으로 자식 패키지에서 속성을 업데이트하기 위해 사용됩니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블|구성을 포함하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블입니다. 테이블은 여러 구성을 포함할 수 있습니다.|  
  
#### <a name="xml-configuration-files"></a>XML 구성 파일  
 **XML 구성 파일** 의 구성 유형을 선택한 경우 새 구성 파일을 만들고 기존의 파일을 다시 사용하면서 새 구성을 추가하거나 또는 기존의 파일을 다시 사용하지만 기존의 파일 내용을 덮어쓸 수 있습니다.  
  
 XML 구성 파일은 두 개의 부분으로 이루어집니다.  
  
-   제목은 구성 파일 자체에 대한 정보를 포함합니다. 이 요소는 파일을 만든 시각과 같은 특성 및 파일을 만든 사람의 이름을 포함합니다.  
  
-   구성 요소는 각 구성에 대한 정보를 포함합니다. 이 요소는 속성 경로 및 속성의 구성 값과 같은 특성을 포함합니다.  
  
 다음 XML 코드에서는 XML 구성 파일의 구문을 보여 줍니다. 이 예에서는 `MyVar`라는 정수 변수의 Value 속성에 대한 구성을 보여 줍니다.  
  
```xml
\<?xml version="1.0"?>  
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
  
#### <a name="registry-entry"></a>레지스트리 항목  
 레지스트리 항목을 사용하여 구성을 저장하려면 기존 키를 사용하거나 HKEY_CURRENT_USER에서 새 키를 만들 수 있습니다. **Value**값이 있는 레지스트리 키를 사용해야 합니다. 값은 DWORD 또는 문자열이 될 수 있습니다.  
  
 **레지스트리 항목** 구성 유형을 선택할 경우 레지스트리 항목 상자에 레지스트리 키의 이름을 입력합니다. 형식은 \<registry key>입니다. HKEY_CURRENT_USER의 루트에 없는 레지스트리 키를 사용하려면 \<Registry key\registry key\\...> 형식을 사용하여 키를 식별합니다. 예를 들어 SSISPackages에 있는 MyPackage 키를 사용하려면 **SSISPackages\MyPackage**를 입력합니다.  
  
#### <a name="sql-server"></a>SQL Server  
 **SQL Server** 구성 유형을 선택한 경우 구성을 저장할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 연결을 지정하십시오. 기존 테이블에 구성을 저장하거나 지정한 데이터베이스에 새 테이블을 만들 수 있습니다.  
  
 다음 SQL 문에서는 패키지 구성 마법사가 제공하는 기본 CREATE TABLE 문을 보여 줍니다.  
  
```sql
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 구성에 지정한 이름은 **ConfigurationFilter** 열에 저장된 값입니다.  
  
### <a name="direct-and-indirect-configurations"></a>직접 및 간접 구성  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 직접 및 간접 구성을 제공합니다. 구성을 직접으로 지정한 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 구성 항목 및 패키지 개체 속성 간에 직접 연결을 만듭니다. 직접 구성은 원본의 위치가 변경되지 않는 경우에 적합합니다. 예를 들어 패키지의 모든 배포가 동일한 파일 경로를 사용하는 경우 XML 구성 파일을 지정할 수 있습니다.  
  
 간접 구성은 환경 변수를 사용합니다. 구성 설정을 직접 지정하는 대신 구성이 구성 값을 포함하는 환경 변수를 가리킵니다. 간접 구성은 각 패키지의 배포에 대해 구성 위치가 변경될 수 있는 경우에 적합합니다.  

## <a name="create-package-configurations"></a>패키지 구성 만들기
  **패키지 구성 도우미** 대화 상자 및 패키지 구성 마법사를 사용하여 패키지 구성을 만듭니다. 이 도구에 액세스하려면 **의** SSIS **메뉴에서** 패키지 구성 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]을 클릭합니다.  
  
  
 **참고:**
> **구성** 속성 옆에 있는 줄임표 단추를 클릭하여 **패키지 구성 도우미** 에 액세스할 수도 있습니다. 구성 속성은 패키지의 속성 창에 나타납니다.  
> 
> 구성은 패키지 배포 모델에 사용할 수 있습니다. 매개 변수는 프로젝트 배포 모델에 대한 구성 대신 사용됩니다. 프로젝트 배포 모델을 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)를 참조하십시오.    
> 
> **패키지 구성 도우미** 대화 상자에서는 구성을 사용하도록 패키지를 활성화하고 구성을 추가 및 삭제하며 구성이 로드되는 기본 순서를 설정할 수 있습니다. 
> 
> 패키지 구성이 기본 순서로 로드되는 경우 **패키지 구성 도우미** 대화 상자에 표시된 목록의 맨 위에서 맨 아래까지의 구성이 로드됩니다. 그러나 런타임 시 패키지 구성이 기본 순서로 로드되지 않을 수 있습니다. 특히 부모 패키지 구성은 다른 유형의 구성보다 뒤에 로드됩니다.  
> 
> 여러 구성이 동일한 개체 속성을 설정하는 경우 마지막으로 로드된 값이 런타임에 사용됩니다.  
  
 **패키지 구성 도우미** 대화 상자에서는 구성을 만드는 단계를 안내하는 패키지 구성 마법사를 실행할 수 있습니다. 패키지 구성 마법사를 실행하려면 **패키지 구성 도우미** 대화 상자에서 새 구성을 추가하거나 기존 구성을 편집합니다. 마법사 페이지에서 구성 유형을 선택하고 사용자가 구성에 직접 액세스할 것인지 또는 환경 변수를 사용할지 선택한 다음 구성에 저장할 속성을 선택하십시오.  
  
 다음 예에서는 패키지 구성 마법사의 마법사 완료 페이지에 표시되는 변수와 패키지의 대상 속성을 보여 줍니다.  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 이 예에서는 구성이 다음과 같은 속성을 업데이트합니다.  
  
-   사용자 정의 변수의 RaiseChangedEvent 속성, `TodaysDate`입니다.  
  
-   패키지의 MaximumErrorCount, LoggingMode 및 LocaleID 속성입니다.  
  
-   내 SQL 태스크 범위에 있는 사용자 정의 변수 `varTableName`의 Value 속성  
  
 "\Package"는 루트를 나타내며 구성에서 업데이트하는 속성에 대한 경로를 정의하는 개체를 구분하는 데 마침표(.)가 사용됩니다. 변수 및 속성의 이름은 대괄호로 묶여 있습니다. 구성에서는 패키지 이름과 상관없이 패키지라는 용어가 사용되지만 경로 내의 다른 모든 개체는 자체 사용자 정의 이름을 사용합니다.  
  
 마법사를 완료하면 **패키지 구성 도우미** 대화 상자의 구성 목록에 새 구성이 추가됩니다.  
  
> **참고:** 패키지 구성 마법사의 마지막 페이지인 마법사 완료 페이지에는 구성의 대상 속성이 나열됩니다. **dtexec** 명령 프롬프트 유틸리티를 사용하여 패키지를 실행할 때 속성을 업데이트하려면 패키지 구성 마법사를 실행하여 속성 경로를 나타내는 문자열을 생성한 다음 복사하여 **dtexec**의 설정 옵션으로 사용할 수 있게 명령 프롬프트 창에 붙여넣습니다.  
  
 다음 표에서는 **패키지 구성 도우미** 대화 상자 구성 목록의 열에 대해 설명합니다.  
  
|열|Description|  
|------------|-----------------|  
|**구성 이름**|구성의 이름입니다.|  
|**구성 유형**|구성의 유형입니다.|  
|**구성 문자열**|구성의 위치입니다. 위치는 경로, 환경 변수, 레지스트리 키, 부모 패키지 변수 이름 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 테이블일 수 있습니다.|  
|**대상 개체**|구성이 있는 속성을 가진 개체의 이름입니다. 구성이 XML 구성 파일이면 여러 개체를 업데이트할 수 있으므로 열이 비어 있습니다.|  
|**대상 속성**|속성의 이름입니다. 구성에서 XML 구성 파일 또는 SQL Server 테이블에 쓰면 여러 개체를 업데이트할 수 있으므로 열이 비어 있습니다.|  
  
### <a name="to-create-a-package-configuration"></a>패키지 구성을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 **제어 흐름**, **데이터 흐름**, **이벤트 처리기**또는 **패키지 탐색기** 탭을 차례로 클릭합니다.  
  
4.  **SSIS** 메뉴에서 **패키지 구성**을 클릭합니다.  
  
5.  **패키지 구성 도우미** 대화 상자에서 **패키지 구성 설정**을 선택하고 **추가**를 클릭합니다.  
  
6.  패키지 구성 마법사 시작 페이지에서 **다음**을 클릭합니다.  
  
7.  구성 유형 선택 페이지에서 구성 유형을 지정하고 구성 유형과 관련된 속성을 설정합니다. 자세한 내용은 [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md)을 참조하세요.  
  
8.  내보낼 속성 선택 페이지에서 구성에 포함할 패키지 개체의 속성을 선택합니다. 구성 유형이 하나의 속성만 지원할 경우 이 마법사 페이지의 제목은 대상 속성 선택입니다. 자세한 내용은 [Package Configuration Wizard UI Reference](../../integration-services/packages/package-configuration-wizard-ui-reference.md)을 참조하세요.  
  
    > **참고:** 한 개의 구성에 여러 속성을 포함하는 기능은 **XML 구성 파일** 및 **SQL Server** 구성 유형만 지원합니다.  
  
9. 마법사 완료 페이지에 구성 이름을 입력하고 **마침**을 클릭합니다.  
  
10. **패키지 구성 도우미** 대화 상자에서 구성을 확인합니다.  
  
11. **닫기**를 클릭합니다.  

## <a name="package-configurations-organizer"></a>패키지 구성 도우미
  **패키지 구성 도우미** 대화 상자를 사용하여 패키지 구성을 설정하고, 현재 패키지에 대한 구성 목록을 보고, 구성을 로드해야 하는 기본 순서를 지정할 수 있습니다.  
  
> **참고:** 구성은 패키지 배포 모델에 사용할 수 있습니다. 매개 변수는 프로젝트 배포 모델에 대한 구성 대신 사용됩니다. 프로젝트 배포 모델을 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)를 참조하십시오.    
  
 여러 구성에서 동일한 속성을 업데이트하는 경우 구성 목록에서 더 아래에 있는 구성의 값이 목록에서 위에 있는 구성의 값을 대체합니다. 패키지를 실행하면 마지막으로 속성에 로드된 값이 사용됩니다. 또한 패키지가 XML 구성 파일 등의 직접 구성과 환경 변수 등의 간접 구성을 조합해서 사용하는 경우 직접 구성의 위치를 가리키는 간접 구성이 목록에서 더 위에 있어야 합니다.  
  
> **참고:** 패키지 구성이 기본 순서로 로드되는 경우 **패키지 구성 도우미** 대화 상자에 표시된 목록의 맨 위에서 맨 아래까지의 구성이 로드됩니다. 그러나 런타임 시 패키지 구성이 기본 순서로 로드되지 않을 수 있습니다. 특히 부모 패키지 구성은 다른 유형의 구성보다 뒤에 로드됩니다.  
  
 패키지 구성은 런타임 시 패키지 개체의 속성 값을 업데이트합니다. 패키지가 로드되면 구성의 값이 패키지 개발 시 설정한 값을 대체합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 여러 가지 구성 유형을 지원합니다. 예를 들어 여러 구성이 포함될 수 있는 XML 파일이나 단일 구성이 포함되는 환경 변수를 사용할 수 있습니다. 자세한 내용은 [Package Configurations](../../integration-services/packages/package-configurations.md)을 참조하세요.  
  
### <a name="options"></a>옵션  
 **패키지 구성 설정**  
 패키지에 구성을 사용하려면 선택합니다.  
  
 **구성 이름**  
 구성의 이름을 봅니다.  
  
 **구성 유형**  
 구성이 저장된 위치의 유형을 봅니다.  
  
 **구성 문자열**  
 구성 값이 저장된 위치를 봅니다. 위치는 파일 경로, 환경 변수 이름, 부모 패키지 변수 이름, 레지스트리 키 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 이름일 수 있습니다.  
  
 **대상 개체**  
 구성에서 업데이트하는 개체의 이름을 봅니다. 구성이 XML 구성 파일이나 SQL Server 테이블인 경우 여러 개체를 포함할 수 있으므로 열이 비어 있습니다.  
  
 **대상 속성**  
 구성에서 수정하는 속성의 이름을 봅니다. 구성 유형에서 여러 구성을 지원하는 경우 이 열은 비어 있습니다.  
  
 **추가**  
 패키지 구성 마법사를 사용하여 구성을 추가합니다.  
  
 **편집**  
 패키지 구성 마법사를 다시 실행하여 기존 구성을 편집합니다.  
  
 **제거**  
 구성을 선택한 다음 **제거**를 클릭합니다.  
  
 **화살표**  
 구성을 선택하고 위로 화살표 및 아래로 화살표를 사용하여 해당 구성을 목록에서 위 또는 아래로 이동합니다. 구성은 목록에 나타나는 순서대로 로드됩니다.  

## <a name="package-configuration-wizard-ui-reference"></a>패키지 구성 마법사 UI 참조
  **패키지 구성 마법사** 를 사용하여 런타임에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 및 패키지 개체의 속성을 업데이트하는 구성을 만들 수 있습니다. 이 마법사는 **패키지 구성 도우미** 대화 상자에서 기존 구성을 수정하거나 새 구성을 추가하는 경우 실행됩니다. **패키지 구성 도우미** 대화 상자를 열려면 **의** SSIS **메뉴에서** 패키지 구성 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]을 선택합니다. 자세한 내용은 [패키지 구성 만들기](../../integration-services/packages/create-package-configurations.md)를 참조하세요.  
  
> **참고:** 구성은 패키지 배포 모델에 사용할 수 있습니다. 매개 변수는 프로젝트 배포 모델에 대한 구성 대신 사용됩니다. 프로젝트 배포 모델을 사용하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. 배포 모델에 대한 자세한 내용은 [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx)를 참조하십시오.  
  
 다음 섹션에서는 마법사의 페이지에 대해 설명합니다.  
  
### <a name="welcome-to-the-package-configuration-wizard-page"></a>패키지 구성 마법사 시작 페이지  
 **SSIS 구성 마법사** 를 사용하여 런타임에 패키지 및 패키지 개체의 속성을 업데이트하는 구성을 만들 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **이 페이지를 다시 표시 안 함**  
 다음에 마법사를 열 때 시작 페이지를 표시하지 않습니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
### <a name="select-configuration-type-page"></a>구성 유형 선택 페이지  
 **구성 유형 선택** 페이지를 사용하여 만들 구성 유형을 지정할 수 있습니다.  
  
 사용할 구성 유형을 결정하는 데 추가 정보가 필요한 경우 [Package Configurations](../../integration-services/packages/package-configurations.md)을 참조하십시오.  
  
#### <a name="static-options"></a>정적 옵션  
 **구성 유형**  
 다음 옵션을 사용하여 구성을 저장할 원본 유형을 선택합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**XML 구성 파일**|구성을 XML 파일로 저장합니다. 이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**환경 변수**|환경 변수 중 하나에 구성을 저장합니다. 이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**레지스트리 항목**|레지스트리에 구성을 저장합니다. 이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**부모 패키지 변수**|태스크를 포함하는 패키지의 변수로 구성을 저장합니다.  이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
|**SQL Server**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 테이블에 구성을 저장합니다. 이 값을 선택하면 **구성 유형**섹션에 설명된 동적 옵션이 표시됩니다.|  
  
 **다음**  
 마법사 시퀀스에서 다음 페이지를 표시합니다.  
  
#### <a name="dynamic-options"></a>동적 옵션  
  
##### <a name="configuration-type-option--xml-configuration-file"></a>구성 유형 옵션 = XML 구성 파일  
 **구성 설정을 직접 지정**  
 설정을 직접 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**구성 파일 이름**|마법사에서 생성하는 구성 파일의 경로를 입력합니다.|  
|**찾아보기**|**구성 파일 위치 선택** 대화 상자를 사용하여 마법사에서 생성하는 구성 파일의 경로를 지정할 수 있습니다. 파일이 없으면 마법사에서 새 파일을 생성합니다.|  
  
 **구성 위치가 환경 변수에 저장됨**  
 구성이 저장되는 환경 변수를 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**환경 변수**|목록에서 환경 변수를 선택합니다.|  
  
##### <a name="configuration-type-option--environment-variable"></a>구성 유형 옵션 = 환경 변수  
 **환경 변수**  
 구성 정보를 포함하는 환경 변수를 선택합니다.  
  
##### <a name="configuration-type-option--registry-entry"></a>구성 유형 옵션 = 레지스트리 항목  
 **구성 설정을 직접 지정**  
 설정을 직접 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**레지스트리 항목**|구성 정보를 포함하는 레지스트리 키를 입력합니다. 형식은 \<registry key>입니다.<br /><br /> 레지스트리 키가 HKEY_CURRENT_USER에 이미 있어야 하고 Value라고 지정된 값을 가져야 합니다. 값은 DWORD 또는 문자열이 될 수 있습니다.<br /><br /> HKEY_CURRENT_USER의 루트에 없는 레지스트리 키를 사용하려면 \<Registry key\registry key\\...> 형식을 사용하여 키를 식별합니다.|  
  
 **구성 위치가 환경 변수에 저장됨**  
 구성이 저장되는 환경 변수를 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**환경 변수**|목록에서 환경 변수를 선택합니다.|  
  
##### <a name="configuration-type-option--parent-package-variable"></a>구성 유형 옵션 = 부모 패키지 변수  
 **구성 설정을 직접 지정**  
 설정을 직접 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**부모 변수**|구성 정보를 포함하는 부모 패키지의 변수를 지정합니다.|  
  
 **구성 위치가 환경 변수에 저장됨**  
 구성이 저장되는 환경 변수를 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**환경 변수**|목록에서 환경 변수를 선택합니다.|  
  
##### <a name="configuration-type-options--sql-server"></a>구성 유형 옵션 = SQL Server  
 **구성 설정을 직접 지정**  
 설정을 직접 지정하는 데 사용됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|**연결**|목록에서 연결을 선택하거나 **새로 만들기** 를 클릭하여 새 연결을 만듭니다.|  
|**구성 테이블**|기존 테이블을 선택하거나 **새로 만들기** 를 클릭하여 새 테이블을 만드는 SQL 문을 작성합니다.|  
|**구성 필터**|기존 구성 이름을 선택하거나 새 이름을 입력합니다.<br /><br /> 같은 테이블에 여러 SQL Server 구성을 저장할 수 있으며 각 구성은 여러 구성 항목을 포함할 수 있습니다.<br /><br /> 이 사용자 정의 값은 특정 구성에 속하는 구성 항목을 식별하기 위해 테이블에 저장됩니다.|  
  
 **구성 위치가 환경 변수에 저장됨**  
 구성이 저장되는 환경 변수를 지정하는 데 사용합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**환경 변수**|목록에서 환경 변수를 선택합니다.|  
  
### <a name="select-objects-to-export-page"></a>내보낼 개체 선택 페이지  
 **대상 속성 선택 또는 내보낼 속성 선택** 페이지를 사용하여 구성에 포함할 개체 속성을 지정할 수 있습니다. 여러 속성을 선택하는 기능은 XML 구성 유형을 선택하는 경우에만 사용할 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **개체**  
 패키지 계층을 확장하고 내보낼 속성을 선택합니다.  
  
 **속성 특성**  
 속성의 특성을 봅니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
### <a name="completing-the-wizard-page"></a>마법사 완료 페이지  
 **마법사 완료** 페이지를 사용하여 구성의 이름을 지정하고 마법사에서 구성을 만드는 데 사용하는 설정을 볼 수 있습니다. 마법사를 완료하면 패키지의 모든 구성을 나열하는 **패키지 구성 도우미** 가 표시됩니다.  
  
#### <a name="options"></a>옵션  
 **구성 이름**  
 구성의 이름을 입력합니다.  
  
 **미리 보기**  
 마법사에서 구성을 만드는 데 사용하는 설정을 봅니다.  
  
 **마침**  
 구성을 만든 다음 **패키지 구성 마법사**를 종료합니다.  

## <a name="use-the-values-of-variables-and-parameters-in-a-child-package"></a><a name="child"></a> 자식 패키지에서 변수 및 매개 변수의 값 사용
  이 절차에서는 부모 변수 구성 유형을 사용하는 패키지 구성을 만드는 방법에 대해 설명합니다. 이 구성 유형을 사용하여 부모 패키지에서 실행되는 자식 패키지가 부모 변수에 액세스하도록 설정할 수 있습니다.  
  
> [!NOTE]  
>  또한 부모 패키지 변수나 매개 변수 또는 프로젝트 매개 변수를 자식 패키지 매개 변수에 매핑하도록 패키지 실행 태스크를 구성하여 값을 자식 패키지에 전달할 수 있습니다. 자세한 내용은 [Execute Package Task](../../integration-services/control-flow/execute-package-task.md)을(를) 참조하세요.  
  
 자식 패키지에 패키지 구성을 만들기 전에 부모 패키지에 변수를 만들 필요는 없습니다. 부모 패키지에는 언제든지 변수를 추가할 수 있습니다. 단, 패키지 구성에 정확한 부모 변수의 이름을 사용해야 합니다. 그러나 부모 변수 구성을 만들려면 이 부모 변수 구성을 통해 업데이트할 수 있는 자식 패키지에 기존 변수가 있어야 합니다. 변수 추가 및 구성에 대한 자세한 내용은 [패키지에서 사용자 정의 변수의 범위 추가, 삭제, 변경](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)을 참조하세요.  
  
 부모 변수 구성에 사용되는 부모 패키지의 변수 범위는 패키지 실행 태스크, 태스크가 있는 컨테이너 또는 패키지로 설정할 수 있습니다. 이름이 같은 여러 개의 변수가 패키지에 정의된 경우 패키지 실행 태스크 범위에 가장 가까운 변수가 사용됩니다. 패키지 실행 태스크에 가장 가까운 범위는 작업 자체입니다.  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>부모 패키지에 변수를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 자식 패키지에 전달할 변수를 추가할 패키지가 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  다음 중 하나를 수행하여 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 변수 범위를 정의하십시오.  
  
    -   패키지 범위를 설정하려면 **제어 흐름** 탭의 디자인 화면에서 아무 곳이나 클릭합니다.  
  
    -   범위를 패키지 실행 태스크의 부모 컨테이너로 설정하려면 컨테이너를 클릭합니다.  
  
    -   패키지 실행 태스크의 범위를 설정하려면 태스크를 클릭합니다.  
  
4.  변수를 추가하고 구성합니다.  
  
    > [!NOTE]  
    >  변수가 저장하는 데이터와 호환 가능한 데이터 형식을 선택합니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
### <a name="to-add-a-variable-to-a-child-package"></a>자식 패키지에 변수를 추가하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 부모 변수 구성을 추가할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지 범위를 설정하려면 **제어 흐름** 탭의 디자인 화면에서 아무 곳이나 클릭합니다.  
  
4.  변수를 추가하고 구성합니다.  
  
    > [!NOTE]  
    >  변수가 저장하는 데이터와 호환 가능한 데이터 형식을 선택합니다.  
  
5.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  

## <a name="create-a-deployment-utility"></a>Create a Deployment Utility
  패키지를 배포하는 첫 번째 단계는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트의 배포 유틸리티를 만드는 것입니다. 배포 유틸리티는 다른 서버로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트의 패키지를 배포하는 데 필요한 파일이 포함된 폴더입니다. 배포 유틸리티는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트가 저장된 컴퓨터에 만들어집니다.  
  
 먼저 배포 유틸리티를 만들도록 빌드 프로세스를 구성한 다음 프로젝트를 빌드하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트의 패키지 배포 유틸리티를 만들 수 있습니다. 프로젝트를 빌드할 때 프로젝트의 모든 패키지와 패키지 구성은 자동으로 포함됩니다. 추가 정보 파일 등의 추가 파일을 프로젝트와 함께 배포하려면 해당 파일을 **프로젝트의** 기타 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 폴더에 저장하십시오. 프로젝트가 빌드될 때 이러한 파일도 자동으로 포함됩니다.  
  
 각 프로젝트 배포를 다르게 구성할 수 있습니다. 프로젝트를 빌드하고 패키지 배포 유틸리티를 작성하기 전에 배포 유틸리티의 속성을 설정하여 프로젝트의 패키지를 배포하는 방법을 사용자 지정할 수 있습니다. 예를 들어 프로젝트를 배포할 때 패키지 구성을 업데이트할지 여부를 지정할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트의 속성에 액세스하려면 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
 다음 표에서는 배포 유틸리티 속성을 나열합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|AllowConfigurationChange|배포 도중 구성의 업데이트를 허용할지 여부를 지정하는 값입니다.|  
|CreateDeploymentUtility|프로젝트를 빌드할 때 패키지 배포 유틸리티를 만들지 여부를 지정하는 값입니다. 배포 유틸리티를 만들려면 이 속성을 **True** 로 설정합니다.|  
|DeploymentOutputPath|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트와 관련된 배포 유틸리티의 위치입니다.|  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 빌드하면 매니페스트 파일인 \<project name>.SSISDeploymentManifest.xml이 패키지 종속 관계 및 패키지의 복사본과 함께 프로젝트의 bin\Deployment 폴더 또는 DeploymentOutputPath 속성에서 지정한 위치에 만들어지고 추가됩니다. 매니페스트 파일은 프로젝트의 패키지, 패키지 구성 및 모든 기타 파일을 나열합니다.  
  
 배포 폴더의 내용은 프로젝트를 작성할 때마다 새로 고쳐집니다. 즉, 배포 폴더에 저장되었지만 빌드 프로세스로 폴더에 다시 복사되지 않은 파일은 모두 삭제됩니다. 예를 들어 배포 폴더에 저장된 패키지 구성 파일은 삭제되지 않습니다.  
  
### <a name="to-create-a-package-deployment-utility"></a>패키지 배포 유틸리티를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지 배포 유틸리티를 만들 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트가 들어 있는 솔루션을 엽니다.  
  
2.  프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **\<project name> 속성 페이지** 대화 상자에서 **배포 유틸리티**를 클릭합니다.  
  
4.  패키지를 배포할 때 패키지 구성을 업데이트하려면 **AllowConfigurationChanges** 를 **True**로 설정합니다.  
  
5.  **CreateDeploymentUtility** 를 **True**로 설정합니다.  
  
6.  필요에 따라 **DeploymentOutputPath** 속성을 수정하여 배포 유틸리티의 위치를 업데이트합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **빌드**를 클릭합니다.  
  
9. **출력** 창에서 빌드 과정 및 빌드 오류를 확인합니다.  

## <a name="deploy-packages-by-using-the-deployment-utility"></a>배포 유틸리티를 사용한 패키지 배포
  다른 컴퓨터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에 패키지를 설치하기 위해 배포 유틸리티를 빌드한 다음에는 먼저 대상 컴퓨터에 배포 폴더를 복사해야 합니다.  
  
 배포 폴더의 경로는 배포 유틸리티를 만든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트의 DeploymentOutputPath 속성에 지정됩니다. 기본 경로는 bin\Deployment이며 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에 상대적입니다. 자세한 내용은 [Create a Deployment Utility](../../integration-services/packages/create-a-deployment-utility.md)를 참조하세요.  
  
 패키지 설치 마법사를 사용하여 패키지를 설치합니다. 마법사를 시작하려면 배포 폴더를 서버로 복사한 다음 배포 유틸리티 파일을 두 번 클릭합니다. 이 파일의 이름은 \<project name>.SSISDeploymentManifest이며 대상 컴퓨터의 배포 폴더에 있습니다.  
  
> [!NOTE]  
>  배포하는 패키지의 버전에 따라 여러 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 함께 설치할 경우 오류가 발생할 수 있습니다. 이 오류는 .SSISDeploymentManifest 파일 이름 확장명이 모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]버전에서 동일하기 때문에 발생할 수 있습니다. 파일을 두 번 클릭하면 가장 최근에 설치된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]버전의 설치 관리자가 호출되며 이 버전이 배포 유틸리티 파일과 동일한 버전이 아닐 수 있습니다. 이 문제를 해결하려면 명령줄에서 정확한 버전의 dtsinstall.exe를 실행한 후 배포 유틸리티 파일의 경로를 입력합니다.  
  
 패키지 설치 마법사는 파일 시스템 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 패키지를 설치하는 단계를 안내합니다. 다음과 같은 방법으로 설치를 구성할 수 있습니다.  
  
-   패키지를 설치할 위치 유형 및 위치 선택  
  
-   패키지 종속 파일을 설치할 위치 선택  
  
-   대상 서버에 패키지 설치 후 패키지의 유효성 검사  
  
 패키지의 파일 기반 종속성은 항상 파일 시스템에 설치됩니다. 파일 시스템에 패키지를 설치한 경우 패키지에 지정한 것과 동일한 폴더에 종속성이 설치됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 패키지를 설치하는 경우 파일 기반 종속성을 저장할 폴더를 지정할 수 있습니다.  
  
 패키지에 대상 컴퓨터에서 사용하기 위해 수정할 구성이 포함된 경우 마법사를 사용하여 속성 값을 업데이트할 수 있습니다.  
  
 패키지 설치 마법사를 사용하여 패키지를 설치하는 방법 이외에도 **dtutil** 명령 프롬프트 유틸리티를 사용하여 패키지를 복사 및 이동할 수 있습니다. 자세한 내용은 [dtutil Utility](../../integration-services/dtutil-utility.md)를 참조하세요.  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>SQL Server 인스턴스에 패키지를 배포하려면  
  
1.  대상 컴퓨터에서 배포 폴더를 엽니다.  
  
2.  매니페스트 파일 \<project name>.SSISDeploymentManifest를 두 번 클릭하여 패키지 설치 마법사를 시작합니다.  
  
3.  **SSIS 패키지 배포** 페이지에서 **SQL Server 배포** 옵션을 선택합니다.  
  
4.  필요에 따라 **설치 후 패키지 유효성 검사** 를 선택하여 대상 서버에 패키지를 설치한 후 패키지의 유효성을 검사합니다.  
  
5.  **대상 SQL Server 지정** 페이지에서 패키지를 설치할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 지정하고 인증 모드를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 선택하는 경우 사용자 이름 및 암호를 지정해야 합니다.  
  
6.  **설치 폴더 선택** 페이지에서 패키지 종속성에 의해 설치될 파일 시스템 내의 폴더를 지정합니다.  
  
7.  패키지가 구성을 포함하는 경우 구성 패키지 페이지에서 **값** 목록의 값을 업데이트하여 구성을 편집할 수 있습니다.  
  
8.  설치 후에 패키지의 유효성 검사를 수행하도록 선택한 경우 배포된 패키지의 유효성 검사 결과를 확인합니다.  

## <a name="redeployment-of-packages"></a>패키지 재배포
  프로젝트를 배포한 후 패키지 기능을 업데이트하거나 확장한 다음 업데이트된 패키지를 포함하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 다시 배포해야 할 수 있습니다. 패키지 재배포 과정의 일부로 배포 유틸리티에 포함된 구성 속성을 검토하십시오. 예를 들어 패키지를 재배포한 후 구성을 변경할 수 없도록 하기를 원할 수 있습니다.  
  
### <a name="process-for-redeployment"></a>재배치 프로세스  
 패키지 업데이트를 완료한 다음에는 프로젝트를 다시 빌드하고 대상 컴퓨터에 배포 폴더를 복사한 다음 패키지 설치 마법사를 다시 실행하십시오.  
  
 프로젝트 내의 소수 패키지만 업데이트한 경우 전체 프로젝트를 재배포하고 싶지 않을 수 있습니다. 소수의 패키지만 배포하려면 새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 만들고 업데이트된 패키지를 추가한 다음 프로젝트를 빌드하고 배포하십시오. 다른 프로젝트에 패키지를 추가하는 경우 자동으로 패키지와 함께 패키지 구성이 복사됩니다.  

## <a name="package-installation-wizard-ui-reference"></a>패키지 설치 마법사 UI 참조
  **패키지 설치 마법사** 를 사용하여 프로젝트에 포함된 패키지 및 기타 파일과 모든 패키지 종속 파일을 포함한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 배포할 수 있습니다.  
  
 패키지를 배포하기 전에 구성을 만들어 패키지와 함께 배포할 수 있습니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 는 구성을 사용하여 런타임 시 패키지와 패키지 개체의 속성을 동적으로 업데이트합니다. 예를 들어 연결 문자열이 포함된 속성에 값을 매핑하는 구성을 제공하여 OLE DB 연결의 연결 문자열을 런타임 시 동적으로 설정할 수 있습니다.  
  
 패키지 설치 마법사는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 작성하고 배포 유틸리티를 만든 후에만 실행할 수 있습니다. 자세한 내용은 [Deploy Packages by Using the Deployment Utility](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md)를 참조하세요.  
  
 다음 섹션에서는 마법사의 페이지에 대해 설명합니다.  
  
### <a name="welcome-to-the-package-installation-wizard-page"></a>패키지 설치 마법사 시작 페이지  
 **패키지 설치 마법사** 를 사용하여 패키지 배포 유틸리티를 만든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 배포할 수 있습니다.  
  
 **이 시작 페이지를 다시 표시 안 함**  
 마법사를 다시 실행할 때 시작 페이지를 건너뛰려면 선택합니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
### <a name="configure-packages-page"></a>패키지 구성 페이지  
 **패키지 구성** 페이지를 사용하여 패키지 구성을 편집할 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **구성 파일**  
 목록에서 파일을 선택하여 구성 파일의 내용을 편집합니다.  
  
 **관련 항목:** [패키지 구성 만들기](../../integration-services/packages/create-package-configurations.md)  
  
 **Path**  
 구성할 속성의 경로를 봅니다.  
  
 **형식**  
 속성의 데이터 형식을 봅니다.  
  
 **값**  
 구성의 값을 지정합니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
### <a name="confirm-installation-page"></a>설치 페이지 확인  
 **설치 확인** 페이지를 사용하여 패키지 설치를 시작하고, 상태를 보고, 지정한 프로젝트의 파일을 설치할 때 마법사에서 사용할 정보를 볼 수 있습니다.  
  
 **다음**  
 패키지와 종속 파일을 설치하고 설치가 완료되면 마법사의 다음 페이지로 이동합니다.  
  
 **상태**  
 패키지 설치 진행률을 표시합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 이동합니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
### <a name="deploy-ssis-packages-page"></a>SSIS 패키지 배포 페이지  
 **SSIS 패키지 배포** 페이지를 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 및 해당 종속성을 설치할 위치를 지정할 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **파일 시스템 배포**  
 파일 시스템에서 지정한 폴더에 패키지 및 종속성을 배포합니다.  
  
 **SQL Server 배포**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 패키지 및 종속성을 배포합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 서버 간에 패키지를 공유하는 경우 이 옵션을 사용합니다. 모든 패키지 종속성은 파일 시스템에서 지정한 폴더에 설치됩니다.  
  
 **설치 후 패키지 유효성 검사**  
 설치 후 패키지 유효성 검사 여부를 나타냅니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
### <a name="packages-validation-page"></a>패키지 유효성 검사 페이지  
 **패키지 유효성 검사** 페이지를 사용하여 패키지 유효성 검사의 진행률 및 결과를 볼 수 있습니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
### <a name="select-installation-folder-page"></a>설치 폴더 선택 페이지  
 **설치 폴더 선택** 페이지를 사용하여 패키지 및 패키지의 종속성을 설치할 파일 시스템 폴더를 지정할 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **폴더**  
 패키지 및 해당 패키지의 종속성을 복사할 경로 및 폴더를 지정합니다.  
  
 **찾아보기**  
 **폴더 찾아보기** 대화 상자를 사용하여 대상 폴더를 찾습니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
### <a name="specify-target-sql-server-page"></a>대상 SQL Server 지정 페이지  
 **대상 SQL Server 지정** 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 패키지를 배포할 수 있는 옵션을 지정할 수 있습니다.  
  
#### <a name="options"></a>옵션  
 **서버 이름**  
 패키지를 배포할 서버의 이름을 지정합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하여 서버에 로그온하도록 할지 여부를 지정합니다. 보안을 강화하려면 Windows 인증을 사용하는 것이 좋습니다.  
  
 **SQL Server 인증 사용**  
 패키지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 로그온하도록 할지 여부를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **사용자 이름**  
 사용자 이름을 지정합니다.  
  
 **암호**  
 암호를 지정합니다.  
  
 **패키지 경로**  
 논리적 폴더의 이름을 지정하거나 "/"를 입력하여 기본 폴더를 사용합니다.  
  
 **SSIS 패키지** 대화 상자에서 폴더를 선택하려면 찾아보기(...)를 클릭합니다. 그러나 이 대화 상자에서는 기본 폴더를 선택할 수 없습니다. 기본 폴더를 사용하려면 입력란에 "/"를 입력해야 합니다.  
  
> [!NOTE]  
>  유효한 패키지 경로를 입력하지 않으면 "인수 중 하나가 올바르지 않습니다"라는 오류 메시지가 나타납니다.  
  
 **암호화에 서버 스토리지 사용**  
 패키지를 보호하기 위해 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 보안 기능을 사용하려면 선택합니다.  
  
 **다음**  
 마법사의 다음 페이지로 이동합니다.  
  
 **마침**  
 패키지 설치 마법사 마침 페이지로 건너뜁니다. 마법사 페이지를 역추적하여 선택 내용을 수정하고 필요한 옵션을 모두 지정한 경우 이 옵션을 사용합니다.  
  
### <a name="finish-the-package-installation-page"></a>패키지 설치 마침 페이지  
 **패키지 설치 마법사 마침** 페이지를 사용하여 패키지 설치 결과에 대한 요약을 볼 수 있습니다. 이 페이지에서는 배포된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트의 이름, 설치한 패키지, 구성 파일 및 설치 위치와 같은 세부 정보를 제공합니다.  
  
 **마침**  
 **마침**을 클릭하여 마법사를 종료합니다.  

