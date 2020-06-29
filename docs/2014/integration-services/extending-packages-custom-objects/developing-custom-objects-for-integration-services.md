---
title: Integration Services용 사용자 지정 개체 개발 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services]
- custom objects [Integration Services]
ms.assetid: ca1929a6-0ae6-47d7-b65f-08173b143720
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6afb7c8bcb0b6873ff0040eccdcf86dd90997851
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85427640"
---
# <a name="developing-custom-objects-for-integration-services"></a>Integration Services용 사용자 지정 개체 개발
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 포함된 제어 흐름 및 데이터 흐름 개체가 요구 사항을 완전히 충족하지 못하는 경우 다음을 비롯한 여러 가지 유형의 사용자 지정 개체를 직접 개발할 수 있습니다.

-   **사용자 지정 태스크**.

-   **사용자 지정 연결 관리자.** 현재 지원되지 않는 외부 데이터 원본에 연결합니다.

-   **사용자 지정 로그 공급자.** 현재 지원되지 않는 형식으로 패키지 이벤트를 로깅합니다.

-   **사용자 지정 열거자.** 현재 지원되지 않는 일련의 개체 또는 값 형식에 대한 반복을 지원합니다.

-   **사용자 지정 데이터 흐름 구성 요소.** 원본, 변환 또는 대상으로 구성할 수 있습니다.

 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델을 사용하면 사용자 지정 구현을 위한 일관되고 안정적인 프레임워크를 제공하는 기본 클래스를 통해 이러한 사용자 지정 개발을 쉽게 할 수 있습니다.

 사용자 지정 기능을 여러 패키지에서 다시 사용할 필요가 없는 경우 스크립트 태스크 및 스크립트 구성 요소를 사용하면 매우 적은 양의 인프라 코드로도 관리되는 프로그래밍 언어의 강력한 기능을 사용할 수 있습니다. 자세한 내용은 [스크립팅 솔루션과 사용자 지정 개체 비교](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)를 참조하세요.

## <a name="steps-in-developing-a-custom-object-for-integration-services"></a>Integration Services용 사용자 지정 개체 개발 단계
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 사용할 사용자 지정 개체를 개발하는 경우 디자인 타임과 런타임에 SSIS 디자이너에서 로드하고 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임에서 로드할 클래스 라이브러리(DLL)를 개발합니다. 구현해야 하는 가장 중요한 메서드는 개발자가 작성하는 코드에서 호출하는 메서드가 아니라 런타임에서 적절한 때에 구성 요소를 초기화하고 구성 요소의 유효성을 검사하고 해당 기능을 실행하기 위해 호출하는 메서드입니다.

 사용자 지정 개체를 개발할 때 따라야 하는 단계는 다음과 같습니다.

1.  관리되는 프로그래밍 언어로 형식 클래스 라이브러리의 새 프로젝트를 만듭니다.

2.  다음 표와 같이 적절한 기본 클래스에서 상속합니다.

3.  다음 표와 같이 새 클래스에 적절한 특성을 적용합니다.

4.  기본 클래스의 메서드를 필요한 대로 재정의하고 개체의 사용자 지정 기능에 대한 코드를 작성합니다.

5.  필요에 따라 구성 요소의 사용자 지정 사용자 인터페이스를 빌드합니다. 쉽게 배포할 수 있도록 사용자 인터페이스를 동일한 솔루션 내에 별도의 프로젝트로 개발하고 이를 별도의 어셈블리로 빌드할 수 있습니다.

6.  필요에 따라 사용자 지정 개체의 샘플 및 도움말 콘텐츠에 대한 링크를 **SSIS 도구 상자**에 표시합니다.

7.  [사용자 지정 개체 빌드, 배포 및 디버그](building-deploying-and-debugging-custom-objects.md)의 설명에 따라 새 사용자 지정 개체를 빌드, 배포 및 디버그합니다.

## <a name="base-classes-attributes-and-important-methods"></a>기본 클래스, 특성 및 주요 메서드
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 개발 가능한 각 사용자 지정 개체 유형의 가장 중요한 요소에 대한 참조를 제공합니다.

|사용자 지정 개체|기본 클래스|attribute|주요 메서드|
|-------------------|----------------|---------------|-----------------------|
|Task|<xref:Microsoft.SqlServer.Dts.Runtime.Task>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>|
|ODBC 대상 편집기|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>|
|로그 공급자|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>|
|Enumerator|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>|
|데이터 흐름 구성 요소|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>|<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>|

## <a name="providing-links-to-samples-and-help-content"></a>샘플 및 도움말 콘텐츠에 대한 링크 제공
 관리 코드로 작성된 사용자 지정 개체의 샘플 및 도움말 콘텐츠에 대한 링크를 **SSIS 도구 상자**에 표시하려면 다음 속성을 사용합니다.

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

 사용자 지정 사용자 인터페이스 프로젝트 또는 어셈블리에는 일반적으로 두 개의 클래스가 있습니다(특정 유형의 사용자 지정 개체의 사용자 인터페이스에 대한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인터페이스를 구현하는 클래스 및 이 클래스에서 사용자로부터 정보를 수집하기 위해 표시하는 Windows Form). 구현하는 인터페이스에는 단 몇 개의 메서드만 포함되므로 사용자 지정 사용자 인터페이스는 어렵지 않게 개발할 수 있습니다.

> [!NOTE]
>  대부분의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 로그 공급자에는 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI>를 구현하며 **구성** 텍스트 상자를 사용 가능한 연결 관리자의 필터링된 드롭다운 목록으로 바꾸는 사용자 지정 사용자 인터페이스가 있습니다. 그러나 사용자 지정 로그 공급자의 사용자 지정 사용자 인터페이스는 이 릴리스의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 구현되어 있지 않습니다. 따라서 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 속성 값을 지정해도 아무 영향이 없습니다.

 다음 표에서는 각 사용자 지정 개체 유형의 사용자 지정 사용자 인터페이스를 개발할 때 구현해야 하는 인터페이스에 대한 참조를 제공합니다. 또한 개체의 사용자 지정 사용자 인터페이스를 개발하지 않을 경우나 개체의 특성에서 `UITypeName` 속성을 사용하여 사용자 인터페이스에 개체를 연결하지 못할 경우 사용자에게 표시되는 내용에 대해 설명합니다. 데이터 흐름 구성 요소의 경우 강력한 고급 편집기로 충분할 수도 있지만 태스크 및 연결 관리자의 경우 속성 창은 사용자에게는 덜 친숙한 솔루션이며 사용자 지정 ForEach 열거자의 경우는 사용자 지정 폼을 사용하지 않고는 전혀 구성할 수 없습니다.

|사용자 지정 개체|사용자 인터페이스의 기본 클래스|사용자 지정 사용자 인터페이스가 제공되지 않을 경우의 기본 편집 동작|
|-------------------|-----------------------------------|----------------------------------------------------------------------|
|Task|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|속성 창만 표시|
|ODBC 대상 편집기|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>|속성 창만 표시|
|로그 공급자|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI><br /><br /> [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 구현되지 않음|**구성** 열의 텍스트 상자|
|Enumerator|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>|속성 창만 표시. 편집기의 열거자 구성 영역은 비어 있음|
|데이터 흐름 구성 요소|<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>|고급 편집기|

## <a name="external-resources"></a>외부 리소스

-   blogs.msdn.com의 블로그 항목 - [Visual Studio 솔루션 빌드 프로세스에서 SSIS 참조 때문에 .NET Framework 어셈블리에 대한 간접 종속성 경고를 제공함](https://go.microsoft.com/fwlink/?LinkId=215662)

![Integration Services 아이콘 (작은 아이콘)](../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.

## <a name="see-also"></a>참고 항목
 사용자 지정 [개체 유지](persisting-custom-objects.md) [, 사용자 지정 개체 빌드, 배포 및 디버깅](building-deploying-and-debugging-custom-objects.md)


