---
title: Reporting Services의 코드 액세스 보안 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services]
- permission sets [Reporting Services]
- evidence [Reporting Services]
- code access security [Reporting Services], about code access security
- named permission sets [Reporting Services]
ms.assetid: 97480368-1fc3-4c32-b1b0-63edfb54e472
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3dd8d60c975efa1e0a230a08cc6b1ab1a9ce149b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62985747"
---
# <a name="code-access-security-in-reporting-services"></a>Reporting Services의 코드 액세스 보안
  코드 액세스 보안은 증명 정보, 코드 그룹 및 명명된 권한 집합 등의 핵심 개념을 기반으로 합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 보고서 관리자, 보고서 디자이너 및 보고서 서버 구성 요소에는 각각 데이터, 배달, 렌더링 및 보안 확장 프로그램뿐만 아니라 사용자 지정 어셈블리에 대한 코드 액세스 보안을 구성하는 정책 파일이 있습니다. 다음 섹션에서는 코드 액세스 보안에 대한 개요를 제공합니다. 이 섹션에서 다루는 항목에 대한 자세한 내용은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 설명서의 “보안 정책 모델”을 참조하십시오.  
  
 보고서 서버가 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 기술을 기반으로 빌드되어도 일반적인 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 응용 프로그램과 보고서 서버는 상당히 다르기 때문에 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]는 코드 액세스 보안을 사용합니다. 일반적인 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 응용 프로그램은 사용자 코드를 실행하지 않습니다. 반면 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 사용자가 보고서 정의 언어의 **Code** 요소를 사용하여 보고서 정의 파일에 대해 프로그래밍 작업을 수행하고 보고서에 사용할 특수화된 기능을 사용자 지정 어셈블리로 개발해 넣을 수 있도록 하는 확장 가능한 개방형 아키텍처를 사용합니다. 또한 개발자는 보고서 서버의 기능을 향상시키는 강력한 확장 프로그램을 설계하고 배포할 수 있습니다. 이러한 기능과 유연성으로 인해 가능한 한 강력한 보호 및 보안을 제공해야 합니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 개발자는 자신의 보고서에 임의의 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 어셈블리를 사용하고 전역 어셈블리 캐시에 배포된 어셈블리의 모든 기능을 기본적으로 호출할 수 있습니다. 보고서 서버에서는 보고서 식 및 로드된 사용자 지정 어셈블리에 대해 부여할 사용 권한만 제어할 수 있습니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 사용자 지정 어셈블리에는 기본적으로 **실행** 전용 권한만 부여됩니다.  
  
## <a name="evidence"></a>증명 정보  
 증명 정보는 CLR(공용 언어 런타임)이 코드 어셈블리에 대한 보안 정책을 확인하기 위해 사용하는 정보입니다. 증명 정보는 코드에 특정한 특징이 있음을 런타임에 알립니다. 증명 정보의 일반적인 형식에는 디지털 서명 및 어셈블리의 위치가 포함됩니다. 응용 프로그램에 의미가 있는 다른 정보를 나타내도록 증명 정보를 사용자 지정 설계할 수도 있습니다.  
  
 어셈블리 및 응용 프로그램 도메인은 모두 증명 정보를 기반으로 사용 권한을 받습니다. 예를 들어 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]가 액세스를 시도하는 어셈블리의 위치는 짧은 이름이 지정된 어셈블리의 일반적인 증명 정보 형식입니다. 이를 URL 증명 정보라고 합니다. 보고서 서버에 배포된 사용자 지정 데이터 처리 확장 프로그램에 대한 URL 증명 정보는 "C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll"일 수 있습니다. 어셈블리의 강력한 이름 또는 디지털 서명은 증명 정보의 다른 일반적인 형식입니다. 이 경우 증명 정보는 어셈블리에 대한 공개 키 정보입니다.  
  
## <a name="code-groups"></a>코드 그룹  
 코드 그룹은 멤버 자격에 대한 조건이 지정되어 있는 논리적 코드 그룹입니다. 멤버 자격 조건을 충족하는 모든 코드는 이 그룹에 포함됩니다. 관리자는 코드 그룹 및 연결된 권한 집합을 관리하여 보안 정책을 구성합니다.  
  
 코드 그룹에 대한 멤버 자격 조건은 증명 정보를 기반으로 합니다. 예를 들어 코드 그룹에 대한 URL 멤버 자격은 URL 증명 정보를 기반으로 합니다. CLR(공용 언어 런타임)은 URL 증명 정보와 같은 식별 특징을 사용하여 코드를 설명하고 그룹의 멤버 자격 조건이 충족되는지 여부를 확인합니다. 예를 들어 코드 그룹의 멤버 자격 조건이 "어셈블리 C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll의 코드"인 경우 런타임은 증명 정보를 통해 코드가 해당 위치에서 발생되는지 여부를 확인합니다. 이 유형의 코드 그룹에 대한 구성 항목 예는 다음과 같습니다.  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="FullTrust"  
   Name="MyCodeGroup"  
   Description="Code group for my data processing extension">  
      <IMembershipCondition class="UrlMembershipCondition"  
         version="1"  
         Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll"  
       />  
</CodeGroup>  
```  
  
 시스템 관리자 또는 응용 프로그램 배포 전문가와 협력하여 사용자 지정 어셈블리 또는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 확장 프로그램에 필요한 유형의 코드 액세스 보안 및 코드 그룹을 확인해야 합니다.  
  
## <a name="named-permission-sets"></a>명명된 권한 집합  
 명명된 권한 집합은 관리자가 코드 그룹에 연결할 수 있는 권한 집합입니다. 대부분의 명명된 권한 집합은 하나 이상의 권한, 이름 및 해당 권한 집합에 대한 설명으로 구성됩니다. 관리자는 명명된 권한 집합을 사용하여 코드 그룹에 대한 보안 정책을 설정하거나 수정할 수 있습니다. 둘 이상의 코드 그룹을 이름이 같은 명명된 권한 집합에 연결할 수 있습니다. CLR은 **Nothing**, **Execution**, **Internet**, **LocalIntranet**, **Everything** 및 **FullTrust** 등의 명명된 기본 제공 권한 집합을 제공합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 사용자 지정 데이터, 배달, 렌더링 및 보안 확장 프로그램은 **FullTrust** 권한 집합으로 실행해야 합니다. 시스템 관리자와 협력하여 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 확장 프로그램에 적합한 코드 그룹 및 멤버 자격 조건을 추가하십시오.  
  
 사용하는 사용자 지정 어셈블리에 대한 고유한 사용자 지정 권한 수준을 보고서에 연결할 수 있습니다. 예를 들어 어셈블리가 특정 파일에 액세스할 수 있도록 하려면 특정 파일 I/O 액세스 권한으로 명명된 권한 집합을 새로 만든 다음 코드 그룹에 이 권한 집합을 할당할 수 있습니다. 다음 권한 집합은 파일 MyFile.xml에 읽기 전용 액세스 권한을 부여합니다.  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="MyNewFilePermissionSet"  
   Description="A special permission set that grants read access to my file.">  
    <IPermission class="FileIOPermission"  
       version="1"  
       Read="C:\MyFile.xml"/>  
    <IPermission class="SecurityPermission"  
       version="1"  
       Flags="Assertion, Execution"/>  
</PermissionSet>  
```  
  
 이 권한 집합을 부여하는 코드 그룹은 다음과 같습니다.  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="MyNewFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\MyCustomAssembly.dll"/>  
</CodeGroup>  
```  
  
## <a name="see-also"></a>관련 항목  
 [안전한 개발&#40;Reporting Services&#41;](secure-development-reporting-services.md)  
  
  
