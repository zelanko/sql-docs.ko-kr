---
title: "Integration Services 프로그래밍 개요 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services, programming
- architecture [Integration Services]
- assemblies [Integration Services]
- SSIS, programming
- SQL Server Integration Services, programming
- run-time engine [Integration Services]
- packages [Integration Services], programming
- data flow engine [Integration Services]
- languages [Integration Services]
ms.assetid: 262babc6-eea5-4609-bc65-07d64cbcfee9
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 47cb31613e30199902335d891b9f5777757feed3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-programming-overview"></a>Integration Services 프로그래밍 개요
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 데이터 이동 및 변환을 패키지 제어 흐름 및 관리를 구분 하는 아키텍처가 있습니다. 또한 이 아키텍처를 정의하며 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 프로그래밍할 때 자동화하고 확장할 수 있는 두 가지 엔진이 있습니다. 런타임 엔진은 개발자가 실행 흐름을 제어하고 로깅, 이벤트 처리기 및 변수에 대한 옵션을 설정할 수 있게 해 주는 제어 흐름 및 패키지 관리 인프라를 구현합니다. 데이터 흐름 엔진은 데이터 추출, 변환 및 로드에만 사용되는 특수한 고성능 엔진입니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 프로그래밍할 때 실제 프로그래밍 작업은 이러한 두 엔진에 대해 수행됩니다.  
  
 다음 그림에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 아키텍처를 보여 줍니다.  
  
 ![Integration Services 아키텍처](../integration-services/media/mw-dts-01.gif "Integration Services 아키텍처")  
  
## <a name="integration-services-run-time-engine"></a>Integration Services 런타임 엔진  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 런타임 엔진은 실행 순서, 로깅, 변수 및 이벤트 처리를 사용할 수 있게 해 주는 인프라를 구현하여 패키지의 관리와 실행을 제어합니다. 개발자는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 런타임 엔진을 프로그래밍하여 패키지 만들기, 구성 및 실행을 자동화하고 사용자 지정 태스크와 기타 확장 프로그램을 만들 수 있습니다.  
  
 자세한 내용은 참조 [the Package with the Script](../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md), [사용자 지정 태스크를 개발](../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md), 및 [Building Packages Programmatically](../integration-services/building-packages-programmatically/building-packages-programmatically.md)합니다.  
  
## <a name="integration-services-data-flow-engine"></a>Integration Services 데이터 흐름 엔진  
 데이터 흐름 엔진은 다른 원본의 데이터를 이동하고 변환하는 데만 사용되는 특수한 고성능 태스크인 데이터 흐름 태스크를 관리합니다. 다른 태스크와 달리 데이터 흐름 태스크에는 원본, 변환 또는 대상으로 구성할 수 있는 데이터 흐름 구성 요소라는 추가 개체가 있습니다. 이러한 구성 요소는 태스크의 핵심 이동 부분으로서, 데이터의 이동 및 변환을 정의합니다. 개발자는 데이터 흐름 엔진을 프로그래밍하여 데이터 흐름 태스크의 구성 요소 만들기 및 구성을 자동화하고 사용자 지정 구성 요소를 만들 수 있습니다.  
  
 자세한 내용은 참조 [Extending the Data Flow with the Script](../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md), [사용자 지정 데이터 흐름 구성 요소 개발](../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), 및 [Building Packages Programmatically](../integration-services/building-packages-programmatically/building-packages-programmatically.md)합니다.  
  
## <a name="supported-languages"></a>지원되는 언어  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]완벽 하 게 지원는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]합니다. 따라서 개발자는 선택한 .NET 호환 언어로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 프로그래밍할 수 있습니다. 런타임 엔진과 데이터 흐름 엔진은 모두 네이티브 코드로 작성되지만 두 엔진 모두 완전하게 관리되는 개체 모델을 통해 사용할 수 있습니다.  
  
 프로그래밍할 수 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지, 사용자 지정 태스크 및 구성 요소에 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 또는 다른 코드 또는 텍스트 편집기에서. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에서는 코딩, 디버깅 및 테스트 등의 반복되는 주기를 간소화하고 신속하게 처리하기 위한 여러 가지 도구와 기능을 제공합니다. 또한 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]를 사용하면 배포가 간편해집니다. 그러나 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 코드 프로젝트를 컴파일하고 빌드하는 데는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]가 필요하지 않습니다. [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK에는 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 및 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 컴파일러와 관련 도구가 포함되어 있습니다.  
  
> [!IMPORTANT]  
>  기본적으로 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]와 함께 설치되지만 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK는 설치되지 않습니다. 컴퓨터에 SDK가 설치되지 않아 SDK 설명서가 온라인 설명서 컬렉션에 포함되어 있지 않을 경우 이 섹션의 SDK 내용에 대한 링크가 작동하지 않습니다. 설치 후의 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK를 추가할 수 있습니다 SDK 설명서는 온라인 설명서 컬렉션과 목차에 지침에 따라 [추가 / SQL Server 제품 설명서를 제거](http://msdn.microsoft.com/library/ef798cc8-87cf-4d60-a7bf-9e061bdd0052)합니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 스크립트 태스크 및 스크립트 구성 요소 사용 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 도구에 대 한 응용 프로그램으로 VSTA ()는 포함 된 스크립팅 환경입니다. VSTA는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic 및 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#을 지원합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 응용 프로그래밍 인터페이스는 VBScript 같은 COM 기반 스크립팅 언어와 호환되지 않습니다.  
  
## <a name="locating-assemblies"></a>어셈블리 찾기  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 어셈블리는 .NET 4.0으로 업그레이드되었습니다. .NET 4에에 대 한 별도 전역 어셈블리 캐시가 * \<드라이브 >*: \Windows\Microsoft.NET\assembly 합니다. 이 경로, 주로 GAC_MSIL 폴더에서 모든 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 어셈블리를 찾을 수 있습니다.  
  
 이전 버전의와 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], 핵심 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 확장성.dll 파일에도 있습니다 * \<드라이브 >*: files\microsoft SQL Server\100\SDK\Assemblies 합니다.  
  
## <a name="commonly-used-assemblies"></a>일반적으로 사용되는 어셈블리  
 다음 표에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 사용하여 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]를 프로그래밍할 때 자주 사용되는 어셈블리에 대해 설명합니다.  
  
|어셈블리|Description|  
|--------------|-----------------|  
|Microsoft.SqlServer.ManagedDTS.dll|관리되는 런타임 엔진을 포함합니다.|  
|Microsoft.SqlServer.RuntimeWrapper.dll|네이티브 런타임 엔진에 대한 PIA(주 interop 어셈블리) 또는 래퍼를 포함합니다.|  
|Microsoft.SqlServer.PipelineHost.dll|관리되는 데이터 흐름 엔진을 포함합니다.|  
|Microsoft.SqlServer.PipelineWrapper.dll|네이티브 데이터 흐름 엔진에 대한 PIA(주 interop 어셈블리) 또는 래퍼를 포함합니다.|  
  
  
