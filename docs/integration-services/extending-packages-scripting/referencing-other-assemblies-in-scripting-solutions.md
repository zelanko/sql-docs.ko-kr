---
title: "스크립팅 솔루션에서 다른 어셈블리 참조 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3deb13c7e3aeb2e974ac6e6582555a617346a298
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>스크립팅 솔루션에서 다른 어셈블리 참조
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스 라이브러리에 사용자 지정 기능을 구현 하기 위한 강력한 여러 도구와 스크립트 개발자는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 합니다. 스크립트 태스크와 스크립트 구성 요소에서는 관리되는 사용자 지정 어셈블리도 사용할 수 있습니다.  
  
> [!NOTE]  
>  개체 및 웹 서비스에서 메서드를 사용 하 여 패키지를 사용 하려면 사용 된 **웹 참조 추가** 명령에서 사용할 수 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA Tools for Applications (). 이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 웹 서비스를 사용하려면 프록시 클래스를 생성해야 했습니다.  
  
## <a name="using-a-managed-assembly"></a>관리되는 어셈블리 사용  
 에 대 한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 디자인 타임에 관리 되는 어셈블리를 찾으려면 다음 단계를 수행 해야 합니다.  
  
1.  컴퓨터의 임의 폴더에 관리되는 어셈블리를 저장합니다.  
  
    > [!NOTE]  
    >  이전 버전의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서는 %windir%\Microsoft.NET\Framework\vx.x.xxxxx 폴더나 %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies 폴더에 저장된 관리되는 어셈블리에 대한 참조만 추가할 수 있었습니다.  
  
2.  관리되는 어셈블리에 대한 참조를 추가합니다.  
  
     VSTA에서 참조를 추가 하는 **참조 추가** 대화 상자의 **찾아보기** 탭을 찾아서 관리 되는 어셈블리를 추가 합니다.  
  
 런타임에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 관리되는 어셈블리를 찾을 수 있게 하려면 다음 단계를 수행해야 합니다.  
  
1.  강력한 이름으로 관리되는 어셈블리에 서명합니다.  
  
2.  패키지가 실행되는 컴퓨터의 전역 어셈블리 캐시에 어셈블리를 설치합니다.  
  
     자세한 내용은 참조 [건물, Deploying, and Debugging Custom Objects](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)합니다.  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Microsoft .NET Framework 클래스 라이브러리 사용  
 스크립트 태스크와 스크립트 구성 요소에서는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스 라이브러리에서 제공하는 다른 모든 개체와 기능을 사용할 수 있습니다. 예를 들어 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 사용하여 사용자 환경에 대한 정보를 검색하고 패키지를 실행하는 컴퓨터와 상호 작용할 수 있습니다.  
  
 다음 목록에서는 자주 사용되는 몇 가지 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스에 대해 설명합니다.  
  
-   **System.Data** ADO.NET 아키텍처를 포함 합니다.  
  
-   **System.IO** 파일 시스템 및 스트림에 대 한 인터페이스를 제공 합니다.  
  
-   **System.Windows.Forms** 폼을 만들 합니다.  
  
-   **System.Text.RegularExpressions** 정규식 작업을 위한 클래스를 제공 합니다.  
  
-   **System.Environment** 로컬 컴퓨터, 현재 사용자 및 컴퓨터 및 사용자 설정에 대 한 정보를 반환 합니다.  
  
-   **System.Net** 네트워크 통신을 제공 합니다.  
  
-   **System.DirectoryServices** Active Directory를 제공 합니다.  
  
-   **System.Drawing** 광범위 한 이미지 조작 라이브러리를 제공 합니다.  
  
-   **System.Threading** 다중 스레드 프로그래밍을 사용 하도록 설정 합니다.  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에 대한 자세한 내용은 MSDN Library를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅을 사용한 패키지 확장](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  

