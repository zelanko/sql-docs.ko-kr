---
title: 스크립팅 솔루션에서 다른 어셈블리 참조 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa693a941ed5f6d56952c4e720aba7dc318600e0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71286271"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>스크립팅 솔루션에서 다른 어셈블리 참조

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스 라이브러리는 스크립트 개발자가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용자 지정 기능을 구현하는 데 사용할 수 있는 강력한 도구 세트를 제공합니다. 스크립트 태스크와 스크립트 구성 요소에서는 관리되는 사용자 지정 어셈블리도 사용할 수 있습니다.  
  
> [!NOTE]
>  패키지에서 웹 서비스의 개체와 메서드를 사용할 수 있도록 설정하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA(Tools for Applications)에서 사용할 수 있는 **웹 참조 추가** 명령을 사용하세요. 이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 웹 서비스를 사용하려면 프록시 클래스를 생성해야 했습니다.  
  
## <a name="using-a-managed-assembly"></a>관리되는 어셈블리 사용  
 디자인 타임에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 관리되는 어셈블리를 찾을 수 있게 하려면 다음 단계를 수행해야 합니다.  
  
1.  컴퓨터의 임의 폴더에 관리되는 어셈블리를 저장합니다.  
  
    > [!NOTE]  
    >  이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 %windir%\Microsoft.NET\Framework\vx.x.xxxxx 폴더나 %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies 폴더에 저장된 관리되는 어셈블리에 대한 참조만 추가할 수 있었습니다.  
  
2.  관리되는 어셈블리에 대한 참조를 추가합니다.  
  
     참조를 추가하려면 VSTA의 **참조 추가** 대화 상자에 있는 **찾아보기** 탭에서 관리되는 어셈블리를 찾아 추가합니다.  
  
 런타임에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 관리되는 어셈블리를 찾을 수 있게 하려면 다음 단계를 수행해야 합니다.  
  
1.  강력한 이름으로 관리되는 어셈블리에 서명합니다.  
  
2.  패키지가 실행되는 컴퓨터의 전역 어셈블리 캐시에 어셈블리를 설치합니다.  
  
     자세한 내용은 [사용자 지정 개체 빌드, 배포 및 디버그](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)를 참조하세요.  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Microsoft .NET Framework 클래스 라이브러리 사용  
 스크립트 태스크와 스크립트 구성 요소에서는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스 라이브러리에서 제공하는 다른 모든 개체와 기능을 사용할 수 있습니다. 예를 들어 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 사용하여 사용자 환경에 대한 정보를 검색하고 패키지를 실행하는 컴퓨터와 상호 작용할 수 있습니다.  
  
 다음 목록에서는 자주 사용되는 몇 가지 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스에 대해 설명합니다.  
  
-   **System.Data**는 ADO.NET 아키텍처를 포함합니다.  
  
-   **System.IO**는 파일 시스템 및 스트림에 대한 인터페이스를 제공합니다.  
  
-   **System.Windows.Forms**는 폼 만들기 기능을 제공합니다.  
  
-   **System.Text.RegularExpressions**는 정규식 작업을 위한 클래스를 제공합니다.  
  
-   **System.Environment**는 로컬 컴퓨터, 현재 사용자, 컴퓨터 및 사용자 설정에 대한 정보를 반환합니다.  
  
-   **System.Net**은 네트워크 통신을 제공합니다.  
  
-   **System.DirectoryServices**는 Active Directory를 공개합니다.  
  
-   **System.Drawing**은 광범위한 이미지 조작 라이브러리를 제공합니다.  
  
-   **System.Threading**은 다중 스레드 프로그래밍을 사용할 수 있도록 합니다.  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에 대한 자세한 내용은 MSDN Library를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [스크립팅을 사용한 패키지 확장](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
