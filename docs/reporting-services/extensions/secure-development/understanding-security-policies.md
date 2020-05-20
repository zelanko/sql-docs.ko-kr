---
title: 보안 정책 이해 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services], security policies
- Execution permission set
- custom assemblies [Reporting Services], security
- permission sets [Reporting Services]
- expressions [Reporting Services], security
- evidence [Reporting Services]
- FullTrust permission set
- security policies [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: a9bf043a-139a-4929-9a58-244815323df0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6649017002fb3dd5df2dc3ee68a0d759ded24887
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "63193395"
---
# <a name="understanding-security-policies"></a>보안 정책 이해
  보고서 서버에 의해 실행되는 모든 코드는 특정 코드 액세스 보안 정책의 일부여야 합니다. 이러한 보안 정책은 증명 정보를 일련의 명명된 권한 집합에 매핑하는 코드 그룹으로 구성됩니다. 코드 그룹은 해당 그룹의 코드에 대해 허용 가능한 권한을 지정하는 명명된 권한 집합과 연결되어 있는 경우가 많습니다. 런타임은 신뢰할 수 있는 호스트 또는 로더가 제공하는 증명 정보를 사용하여 코드가 속하는 코드 그룹을 결정하고 이에 따라 코드에 부여할 권한을 결정합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)에 의해 정의된 대로 이 보안 정책 아키텍처를 따릅니다. 다음 섹션에서는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 다양한 코드 유형 및 이와 연결된 정책 규칙에 대해 설명합니다.  
  
## <a name="report-server-assemblies"></a>보고서 서버 어셈블리  
 보고서 서버 어셈블리는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 제품의 일부인 코드를 포함하는 어셈블리입니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]는 관리 코드 어셈블리를 사용하여 작성됩니다. 이러한 모든 어셈블리에는 강력한 이름이 지정(디지털로 서명)됩니다. 이러한 어셈블리에 대한 코드 그룹은 어셈블리의 강력한 이름에 대한 공개 키 정보를 기반으로 증명 정보를 제공하는 **StrongNameMembershipCondition**을 사용하여 정의됩니다. 코드 그룹에는 **FullTrust** 권한 집합이 부여됩니다.  
  
## <a name="report-server-extensions-rendering-data-delivery-and-security"></a>보고서 서버 확장 프로그램(렌더링, 데이터, 배달 및 보안)  
 보고서 서버 확장 프로그램은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 기능을 확장하기 위해 만드는 사용자 지정 데이터, 배달, 렌더링 및 보안 확장 프로그램입니다. 확장하는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 구성 요소와 연결된 정책 구성 파일에서 이러한 확장 프로그램 또는 어셈블리 코드에 **FullTrust**를 부여해야 합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 일부로 제공되는 확장 프로그램은 보고서 서버 공개 키로 서명되며 **FullTrust** 권한 집합을 받습니다.  
  
> [!IMPORTANT]  
>  타사 확장 프로그램에 대해 **FullTrust**를 허용하려면 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 정책 구성 파일을 수정해야 합니다. 사용자 지정 확장 프로그램에 대해 **FullTrust**가 있는 코드 그룹을 추가하지 않으면 해당 확장 프로그램을 보고서 서버에서 사용할 수 없습니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 정책 구성 파일에 대한 자세한 내용은 [Reporting Services 보안 정책 파일 사용](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)을 참조하세요.  
  
## <a name="expressions-used-in-reports"></a>보고서에 사용되는 식  
 보고서 식은 보고서 정의 언어 파일의 **Code** 요소 내에 포함된 인라인 코드 식 또는 사용자 정의 메서드입니다. 기본적으로 **Execution** 권한 집합을 이러한 식에 부여하는 코드 그룹이 정책 파일에 이미 구성되어 있습니다. 코드 그룹은 다음과 같습니다.  
  
```  
<CodeGroup  
   class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="Execution"  
   Name="Report_Expressions_Default_Permissions"  
   Description="This code group grants default permissions for code in report expressions and Code element. ">  
    <IMembershipCondition  
       class="StrongNameMembershipCondition"  
       version="1"  
       PublicKeyBlob="002400..."  
    />  
</CodeGroup>  
```  
  
 **Execution** 권한을 사용하면 코드를 실행할 수 있지만 보호된 리소스는 사용할 수 없습니다. 보고서 내의 모든 식은 컴파일된 보고서의 일부로 저장되는 어셈블리("식 호스트" 어셈블리)로 컴파일됩니다. 보고서가 실행되면 보고서 서버는 식 호스트 어셈블리를 로드하고 해당 어셈블리를 호출하여 식을 실행합니다. 식 호스트 어셈블리는 모든 식 호스트에 대한 코드 그룹을 정의하는 데 사용되는 특정 키로 서명됩니다.  
  
 보고서 식은 보고서 개체 모델 컬렉션(필드, 매개 변수 등)을 참조하고 산술 및 문자열 연산과 같은 간단한 태스크를 수행합니다. 이러한 간단한 연산을 수행하는 코드에는 **Execution** 권한만 필요합니다. 기본적으로 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 **Code** 요소의 사용자 정의 메서드 및 모든 사용자 지정 어셈블리에는 **Execution** 권한이 부여됩니다. 따라서 대부분의 식에서는 현재 구성에서 보안 정책 파일을 수정하지 않아도 됩니다. 식 호스트 어셈블리에 추가 권한을 부여하려면 관리자가 보고서 서버 및 보고서 디자이너의 정책 구성 파일을 수정하고 보고서 식 코드 그룹을 변경해야 합니다. 이는 전역 설정이므로 식 호스트에 대한 기본 권한을 변경하면 모든 보고서가 영향을 받습니다. 이러한 이유로 추가 보안이 필요한 모든 코드를 사용자 지정 어셈블리에 저장하는 것이 좋습니다. 그러면 이 어셈블리에만 사용자에게 필요한 권한이 부여됩니다.  
  
> [!IMPORTANT]  
>  외부 어셈블리 또는 보호된 리소스를 호출하는 코드는 보고서에서 사용할 수 있도록 사용자 지정 어셈블리에 통합되어야 합니다. 이렇게 하면 코드에 의해 요청 및 어설션되는 권한을 보다 자세히 제어할 수 있습니다. **Code** 요소 내에서는 보안 메서드를 호출하지 않아야 합니다. 이렇게 하려면 보고서 식 호스트에 **FullTrust**를 부여하고 모든 사용자 지정 코드에 CLR에 대한 모든 액세스 권한을 부여해야 합니다.  
  
> [!CAUTION]  
>  보고서 식 호스트에 대한 코드 그룹에 **FullTrust**를 부여하지 마십시오. 이렇게 하면 모든 보고서 식이 보호된 시스템 호출을 수행할 수 있게 됩니다.  
  
## <a name="custom-assemblies-referenced-in-reports"></a>보고서에서 참조되는 사용자 지정 어셈블리  
 일부 보고서 식은 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 사용자 지정 어셈블리라고도 하는 타사 코드 어셈블리를 호출할 수 있습니다. 보고서 서버는 정책 구성 파일에서 이러한 어셈블리에 **Execution** 권한 이상이 있을 것이라고 예상합니다. 기본적으로 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]와 함께 제공되는 정책 파일은 ‘내 컴퓨터’ 영역에서 시작하는 모든 어셈블리에 **Execution** 권한을 부여합니다. 필요에 따라 사용자 지정 어셈블리에 추가 권한을 부여할 수 있습니다.  
  
 보고서 식에서 특정 코드 권한이 필요한 작업을 수행해야 하는 경우도 있습니다. 일반적으로 이는 보고서 식이 보안된 CLR 라이브러리 메서드(예: 파일 또는 시스템 레지스트리에 액세스하는 메서드)를 호출해야 함을 의미합니다. 이러한 보안 호출을 실행하는 데 필요한 코드 권한은 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 설명서에 나와 있습니다. 호출을 실행하려면 호출 코드에 이러한 특정 보안 권한을 부여해야 합니다. 보고서 식 또는 **Code** 식에서 호출하는 경우에는 식 호스트 어셈블리에 적절한 권한을 부여해야 합니다. 그러나 식 호스트에 권한을 부여하면 보고서의 모든 식에서 실행되는 모든 코드에 해당 권한이 부여됩니다. 그러므로 사용자 지정 어셈블리에서 호출하여 해당 사용자 지정 어셈블리에 특정 권한을 부여하는 것이 훨씬 더 안전합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 코드 액세스 보안](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)   
 [안전한 개발&#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
