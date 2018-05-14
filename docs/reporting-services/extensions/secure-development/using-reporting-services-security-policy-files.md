---
title: Reporting Services 보안 정책 파일 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- code groups [Reporting Services]
- CodeGroup elements
- configuration files [Reporting Services]
- code access security [Reporting Services], security policies
- security policies [Reporting Services]
- security configuration files [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: 2280fff6-3de7-44b1-87da-5db0ec975928
caps.latest.revision: 33
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e606f248ba8343ab5bddae2b0968b80d0d7e4cb4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-reporting-services-security-policy-files"></a>Reporting Services 보안 정책 파일 사용
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 설치 중에 파일 시스템으로 복사되는 세 개의 구성 파일에 구성 요소 보안 정책 정보를 저장합니다. 이러한 구성 파일에는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 코드 어셈블리에 대한 내부용 보안 정책과 사용자 정의 보안 정책의 조합이 들어 있을 수 있습니다. 세 개의 구성 파일은 보고서 서버 및 Windows 서비스, 보고서 관리자 웹 응용 프로그램, 보고서 디자이너 미리 보기 창과 같은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 세 개 보안 개체 구성 요소에 해당합니다.  
  
> [!NOTE]  
>  보고서 디자이너에는 보고서 프로젝트를 **DebugLocal** 모드에서 시작할 때 실행되는 팝업 미리 보기 창과 미리 보기 탭이라는 두 개의 미리 보기 모드가 있습니다. **미리 보기** 탭은 보안 개체 구성 요소가 아니며 보안 정책 설정을 적용하지 않습니다. 미리 보기 창은 보고서 서버 기능을 시뮬레이션하기 위한 것이므로 보고서 디자이너에서 사용자 지정 어셈블리 및 사용자 지정 확장 프로그램을 사용하기 위해 사용자나 관리자가 수정해야 하는 정책 구성 파일을 포함합니다.  
  
 보안 정책 구성 파일에는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 어셈블리에 대한 보안 클래스 정보, 기본 명명된 권한 집합 및 코드 그룹이 포함되어 있습니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 정책 구성 파일은 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]의 컴퓨터 및 엔터프라이즈 수준 정책과 관련된 코드 그룹 계층 및 권한 집합을 결정하는 Security.config 파일과 유사합니다. 이 파일의 위치는 C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\CONFIG\security.config입니다.  
  
## <a name="policy-files-in-reporting-services"></a>Reporting Services의 정책 파일  
 다음 표에서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 정책 구성 파일, 해당 위치(기본 설치 가정) 및 해당 기능을 나열합니다.  
  
|파일 이름 |위치(기본 설치)|Description|  
|---------------|---------------------------------------|-----------------|  
|rssrvpolicy.config|C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer|보고서 서버의 정책 구성 파일입니다. 보고서가 보고서 서버에 배포되면 이러한 보안 정책은 주로 보고서 식 및 사용자 지정 어셈블리에 영향을 줍니다. 이 정책 파일은 보고서 서버에 배포된 사용자 지정 데이터, 배달, 렌더링 및 보안 확장 프로그램에도 영향을 줍니다.|  
|rsmgrpolicy.config|C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportManager|보고서 관리자의 정책 구성 파일입니다. 이러한 보안 정책은 사용자 지정 배달을 위한 구독 사용자 인터페이스 확장 프로그램과 같이 보고서 관리자를 확장하는 모든 어셈블리에 영향을 줍니다.|  
|rspreviewpolicy.config|C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies|보고서 디자이너의 독립 실행형 미리 보기 정책 구성 파일입니다. 이러한 보안 정책은 미리 보기 및 개발 중에 보고서에 사용되는 사용자 지정 어셈블리 및 보고서 식에 영향을 줍니다. 이러한 정책은 보고서 디자이너에 배포된 데이터 처리 확장 프로그램과 같은 사용자 지정 확장 프로그램에도 영향을 줍니다.|  
  
## <a name="modifying-configuration-files"></a>구성 파일 수정  
 구성 설정은 XML 요소나 특성으로 지정됩니다. XML과 구성 파일에 대해 이해하고 있으면 텍스트나 코드 편집기를 사용하여 사용자 정의 가능한 설정을 수정할 수 있습니다. 보안 구성 파일에는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 정책 수준과 관련된 코드 그룹 계층 및 권한 집합에 대한 정보가 포함되어 있습니다. 정책 변경 내용이 정책 파일의 올바른 XML 구성 요소에 해당하도록 .NET Framework 구성 유틸리티(Mscorcfg.msc) 또는 코드 액세스 보안 정책 유틸리티(Caspol.exe)를 사용하여 Security.config 파일에서 보안 정책을 먼저 수정하는 것이 좋습니다. 이 작업을 수행한 다음에는 Security.config에서 새 코드 그룹 및 권한 집합을 잘라내어 코드 권한을 추가하는 구성 요소의 정책 파일에 붙여 넣을 수 있습니다.  
  
> [!IMPORTANT]  
>  변경하기 전에 정책 구성 파일을 백업해야 합니다.  
  
 이 방법을 사용하면 두 가지 작업을 수행할 수 있습니다. 첫 번째로, 시각적 도구를 사용하여 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에 대한 코드 그룹 및 권한 집합을 작성할 수 있습니다. 이렇게 하는 것이 완전히 새로 XML 구성 요소를 쓰는 것보다 훨씬 쉽습니다. 두 번째로, 잘못된 XML 요소 및 특성으로 인해 보안 정책 구성 파일이 손상되지 않도록 할 수 있습니다. 코드 액세스 보안 정책 유틸리티에 대한 자세한 내용은 MSDN에서 Reporting Services 보안 정책 파일 사용을 참조하십시오.  
  
 정책 구성 파일을 수정하기 전에 이 섹션 및 관련 항목에 제공된 모든 정보를 읽어 보아야 합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 정책 구성을 수정하면 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 요소가 외부 코드 모듈을 실행하는 방식에 심각한 보안 문제가 발생할 수 있습니다.  
  
## <a name="placement-of-codegroup-elements-for-extensions"></a>확장 프로그램에 대한 CodeGroup 요소 배치  
 보안 정책 파일에서의 CodeGroup 요소 배치는 중요합니다. 개발하는 확장 프로그램 및 사용자 지정 어셈블리에 대해 사용자 지정 코드 그룹을 다음과 같이 URL 멤버 자격 "$CodeGen$/*"의 기존 항목 바로 아래에 배치하는 것이 좋습니다.  
  
```  
<CodeGroup  
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust">  
    <IMembershipCondition   
        class="UrlMembershipCondition"  
        version="1"  
        Url="$CodeGen$/*"  
    />  
</CodeGroup>  
<CodeGroup   
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust"  
    Name="MyCustomCodeGroup"  
    Description="Code group for my custom extension">  
        <IMembershipCondition class="UrlMembershipCondition"  
        version="1"  
        Url="C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer\bin\MyAssembly.dll"  
        />  
</CodeGroup>  
```  
  
 추가 코드 그룹을 차례로 추가할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [보안 정책 이해](../../../reporting-services/extensions/secure-development/understanding-security-policies.md)  
  
  
