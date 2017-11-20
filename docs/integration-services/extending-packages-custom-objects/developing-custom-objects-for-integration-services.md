---
title: "Integration Services에 대 한 사용자 지정 개체 개발 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom user interface [Integration Services]
- custom objects [Integration Services]
ms.assetid: ca1929a6-0ae6-47d7-b65f-08173b143720
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6bbb7ccd5d65caa4b5c8cc8f28383b8100e09cd6
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="developing-custom-objects-for-integration-services"></a>Integration Services용 사용자 지정 개체 개발
  제어 흐름 및 데이터 흐름 개체에 포함 되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 요구 사항을 완전히 충족 되지 않으면, 직접 포함 시키는 다양 한 유형의 사용자 지정 개체를 개발할 수 있습니다.  
  
-   **사용자 지정 작업**합니다.  
  
-   **사용자 지정 연결 관리자입니다.** 현재 지원 되지 않는 외부 데이터 원본에 연결 합니다.  
  
-   **사용자 지정 로그 공급자입니다.** 현재 지원 되지 않는 형식으로 패키지 이벤트를 기록 합니다.  
  
-   **사용자 지정 열거자입니다.** 현재 지원 되지 않는 개체 또는 값 형식 집합에 대 한 반복을 지원 합니다.  
  
-   **사용자 지정 데이터 흐름 구성 요소입니다.** 원본, 변환 또는 대상으로 구성할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델을 사용하면 사용자 지정 구현을 위한 일관되고 안정적인 프레임워크를 제공하는 기본 클래스를 통해 이러한 사용자 지정 개발을 쉽게 할 수 있습니다.  
  
 사용자 지정 기능을 여러 패키지에서 다시 사용할 필요가 없는 경우 스크립트 태스크 및 스크립트 구성 요소를 사용하면 매우 적은 양의 인프라 코드로도 관리되는 프로그래밍 언어의 강력한 기능을 사용할 수 있습니다. 자세한 내용은 참조 [스크립팅 솔루션 비교 및 사용자 지정 개체](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)합니다.  
  
## <a name="steps-in-developing-a-custom-object-for-integration-services"></a>Integration Services용 사용자 지정 개체 개발 단계  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 사용할 사용자 지정 개체를 개발하는 경우 디자인 타임과 런타임에 SSIS 디자이너에서 로드하고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에서 로드할 클래스 라이브러리(DLL)를 개발합니다. 구현해야 하는 가장 중요한 메서드는 개발자가 작성하는 코드에서 호출하는 메서드가 아니라 런타임에서 적절한 때에 구성 요소를 초기화하고 구성 요소의 유효성을 검사하고 해당 기능을 실행하기 위해 호출하는 메서드입니다.  
  
 사용자 지정 개체를 개발할 때 따라야 하는 단계는 다음과 같습니다.  
  
1.  관리되는 프로그래밍 언어로 형식 클래스 라이브러리의 새 프로젝트를 만듭니다.  
  
2.  다음 표와 같이 적절한 기본 클래스에서 상속합니다.  
  
3.  다음 표와 같이 새 클래스에 적절한 특성을 적용합니다.  
  
4.  기본 클래스의 메서드를 필요한 대로 재정의하고 개체의 사용자 지정 기능에 대한 코드를 작성합니다.  
  
5.  필요에 따라 구성 요소의 사용자 지정 사용자 인터페이스를 빌드합니다. 쉽게 배포할 수 있도록 사용자 인터페이스를 동일한 솔루션 내에 별도의 프로젝트로 개발하고 이를 별도의 어셈블리로 빌드할 수 있습니다.  
  
6.  필요에 따라 샘플 및 도움말 콘텐츠에 사용자 지정 개체에 대 한 링크를 표시는 **SSIS 도구 상자**합니다.  
  
7.  빌드, 배포 및에 설명 된 대로 새 사용자 지정 개체를 디버깅할 [건물, Deploying, and 사용자 지정 개체 디버깅](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)합니다.  
  
## <a name="base-classes-attributes-and-important-methods"></a>기본 클래스, 특성 및 주요 메서드  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 개발 가능한 각 사용자 지정 개체 유형의 가장 중요한 요소에 대한 참조를 제공합니다.  
  
|사용자 지정 개체|기본 클래스|Attribute|주요 메서드|  
|-------------------|----------------|---------------|-----------------------|  
|태스크|<xref:Microsoft.SqlServer.Dts.Runtime.Task>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>|  
|ODBC 대상 편집기|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>|  
|로그 공급자|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>|  
|Enumerator|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>|  
|데이터 흐름 구성 요소|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>|<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>|  
  
## <a name="providing-links-to-samples-and-help-content"></a>샘플 및 도움말 콘텐츠에 대한 링크 제공  
 에 링크를 표시 하는 **SSIS 도구 상자** 샘플 및 도움말 콘텐츠 관리 코드로 작성 된 사용자 지정 개체에 대 한 다음 속성을 사용 합니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpKeyword%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpKeyword%2A>  
  
 네이티브 코드로 작성된 사용자 지정 개체의 샘플 및 도움말 콘텐츠에 대한 링크를 표시하려면 SamplesTag, HelpKeyword 및 HelpCollection의 레지스트리 스크립트(.rgs) 파일에서 항목을 추가합니다. 다음은 이에 대한 예입니다.  
  
 `val HelpKeyword = s 'sql11.dts.designer.executepackagetask.F1'`  
  
 `val SamplesTag = s 'ExecutePackageTask'`  
  
## <a name="providing-a-custom-user-interface"></a>사용자 지정 사용자 인터페이스 제공  
 사용자 지정 개체의 사용자가 해당 개체의 속성을 구성할 수 있도록 하려면 사용자 지정 사용자 인터페이스도 개발해야 합니다. 사용자 지정 사용자 인터페이스가 반드시 필요하지는 않은 경우라도 기본 편집기보다 더 사용자에게 친숙한 인터페이스를 제공하기 위해 사용자 지정 사용자 인터페이스를 만들 수 있습니다.  
  
 사용자 지정 사용자 인터페이스 프로젝트 또는 어셈블리에는 일반적으로 두 개의 클래스가 포함됩니다. 하나는 특정 사용자 지정 개체 유형의 사용자 인터페이스에 대한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인터페이스를 구현하는 클래스이고 다른 하나는 이 클래스에서 사용자로부터 정보를 수집하기 위해 표시하는 Windows Form입니다. 구현하는 인터페이스에는 단 몇 개의 메서드만 포함되므로 사용자 지정 사용자 인터페이스는 어렵지 않게 개발할 수 있습니다.  
  
> [!NOTE]  
>  많은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 로그 공급자가 구현 하는 사용자 지정 사용자 인터페이스 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> 하 고 대체 된 **구성** 사용 가능한 연결 관리자의 필터링 된 드롭다운 목록 사용 하 여 텍스트 상자. 그러나 사용자 지정 로그 공급자의 사용자 지정 사용자 인터페이스는 이 릴리스의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 구현되어 있지 않습니다. 따라서 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 속성 값을 지정해도 아무 영향이 없습니다.  
  
 다음 표에서는 각 사용자 지정 개체 유형의 사용자 지정 사용자 인터페이스를 개발할 때 구현해야 하는 인터페이스에 대한 참조를 제공합니다. 에 대해서도 설명 표시 개체에 대 한 사용자 지정 사용자 인터페이스를 개발 하지 않으려는 경우 또는 사용자 개체를 사용 하 여 해당 사용자 인터페이스를 연결 하려면 실패 한 경우는 **UITypeName** 개체의 특성에는 속성입니다. 데이터 흐름 구성 요소의 경우 강력한 고급 편집기로 충분할 수도 있지만 태스크 및 연결 관리자의 경우 속성 창은 사용자에게는 덜 친숙한 솔루션이며 사용자 지정 ForEach 열거자의 경우는 사용자 지정 폼을 사용하지 않고는 전혀 구성할 수 없습니다.  
  
|사용자 지정 개체|사용자 인터페이스의 기본 클래스|사용자 지정 사용자 인터페이스가 제공되지 않을 경우의 기본 편집 동작|  
|-------------------|-----------------------------------|----------------------------------------------------------------------|  
|태스크|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|속성 창만 표시|  
|ODBC 대상 편집기|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>|속성 창만 표시|  
|로그 공급자|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI><br /><br /> [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 구현되지 않음|텍스트 상자에 **구성** 열|  
|Enumerator|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>|속성 창만 표시. 편집기의 열거자 구성 영역은 비어 있음|  
|데이터 흐름 구성 요소|<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>|고급 편집기|  
  
## <a name="external-resources"></a>외부 리소스  
  
-   블로그 항목- [SSIS 참조 때문에.NET Framework 어셈블리에 대 한 간접 종속성 경고를 제공 하는 Visual Studio 솔루션 빌드 프로세스](http://go.microsoft.com/fwlink/?LinkId=215662), blogs.msdn.com에서 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 개체 지속](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [사용자 지정 개체 빌드, 배포 및 디버그](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
  
  

