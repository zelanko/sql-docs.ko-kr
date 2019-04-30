---
title: '방법: 사용자 지정 어셈블리 디버깅 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 64a61e044c7ff6efe051eb316cb9f653f0993b68
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63265056"
---
# <a name="how-to-debug-custom-assemblies"></a>방법: 사용자 지정 어셈블리 디버깅
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]는 사용자 지정 어셈블리 코드를 분석하고 오류를 찾는 데 유용한 디버깅 도구를 다수 제공합니다. 사용하기에 가장 좋은 도구는 수행하려는 작업에 따라 달라집니다. 이 예에서는 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]를 사용합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대한 사용자 지정 어셈블리 디자인, 개발 및 테스트를 위해 권장되는 방법은 테스트 보고서와 사용자 지정 어셈블리가 모두 포함된 솔루션을 만드는 것입니다.  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>단일 인스턴스의 Visual Studio를 사용하여 어셈블리를 디버깅하려면  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 사용하여 새 보고서 프로젝트를 만듭니다.  
  
     보고서 프로젝트를 만들 때 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서는 보고서 프로젝트를 포함할 솔루션이 만들어집니다.  
  
2.  새 클래스 라이브러리 프로젝트를 기존 솔루션에 추가합니다. 보고서 프로젝트가 시작 프로젝트로 설정되었는지 확인합니다. 이를 수행하는 방법은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설명서를 참조하십시오.  
  
3.  솔루션 탐색기에서 솔루션을 선택합니다.  
  
4.  **보기** 메뉴에서 **속성 페이지**를 클릭합니다.  
  
     **솔루션 속성 페이지** 대화 상자가 열립니다.  
  
5.  왼쪽 창에서 필요한 경우 **공용 속성**을 확장한 다음 **프로젝트 종속성**을 클릭합니다. **프로젝트** 드롭다운 목록에서 보고서 프로젝트를 선택합니다. **다음에 종속** 목록에서 어셈블리 프로젝트를 선택합니다.  
  
6.  **확인**을 클릭하여 변경 내용을 저장하고 **속성 페이지** 대화 상자를 닫습니다.  
  
7.  솔루션 탐색기에서 사용자 지정 어셈블리 프로젝트를 선택합니다.  
  
8.  **보기** 메뉴에서 **속성 페이지**를 클릭합니다.  
  
     **프로젝트 속성 페이지** 대화 상자가 열립니다.  
  
9. C# 프로젝트의 경우 **빌드** 탭을 클릭하고 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 프로젝트의 경우 **컴파일** 탭을 클릭합니다.  
  
10. **빌드**/**컴파일** 페이지에서 보고서 디자이너 폴더 경로를 입력합니다. 기본적으로 이 경로는 **출력 경로** 입력란에 C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE로 표시됩니다. 그러면 보고서가 실행되기 전에 업데이트된 버전의 사용자 지정 어셈블리가 빌드되어 보고서 디자이너에 직접 배포됩니다.  
  
11. 보고서를 디자인하고 사용자 지정 어셈블리를 개발했으면 사용자 지정 어셈블리 코드에서 중단점을 설정합니다.  
  
12. F5 키를 눌러 **DebugLocal** 모드에서 보고서를 실행합니다. 보고서가 팝업 미리 보기 창에서 실행되면 디버거는 어셈블리의 실행 코드에 해당하는 중단점에서 멈춥니다. F11 키를 사용하여 사용자 지정 어셈블리 코드를 단계별로 분석합니다.  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>두 인스턴스의 Visual Studio를 사용하여 어셈블리를 디버깅하려면  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 시작하고 사용자 지정 어셈블리 프로젝트를 엽니다.  
  
2.  프로젝트를 빌드하고 사용자 지정 어셈블리 및 해당하는 .pdb 파일을 보고서 디자이너에 배포합니다. 배포에 대한 자세한 내용은 [사용자 지정 어셈블리 배포](deploying-a-custom-assembly.md)를 참조하세요.  
  
3.  사용자 지정 어셈블리 코드를 별도의 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 인스턴스에서 열어 둔 상태로 사용자 지정 어셈블리가 사용된 보고서 프로젝트를 엽니다.  
  
4.  사용자 지정 어셈블리 프로젝트를 포함하는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 인스턴스로 이동하고 코드에서 중단점을 설정합니다.  
  
5.  사용자 지정 어셈블리 프로젝트를 활성 창 상태로 두고 **디버그** 메뉴에서 **프로세스에 연결**을 클릭합니다.  
  
     **프로세스에 연결** 대화 상자가 열립니다.  
  
6.  프로세스 목록에서 보고서 프로젝트에 해당하는 devenv.exe 프로세스를 선택하고 **연결**을 클릭합니다.  
  
7.  사용자 지정 어셈블리의 보고서에서 사용할 식을 정의하고 보고서를 디자인합니다.  
  
8.  보고서 디자인을 마쳤으면 **미리 보기** 탭을 클릭합니다.  
  
     보고서가 실행되며 사용자 지정 어셈블리 코드는 미리 정의된 중단점에서 멈추게 됩니다.  
  
    > [!NOTE]  
    >  **미리 보기** 탭을 사용할 경우 어셈블리에 대한 코드 권한이 적용되지 않습니다. 코드 액세스 보안 오류를 포함한 전체 테스트의 경우 **DebugLocal** 구성 설정에서 보고서 프로젝트를 시작합니다.  
  
9. F11 키를 사용하여 코드를 단계별로 실행합니다. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 사용하여 디버깅하는 방법은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설명서를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [보고서에서 사용자 지정 어셈블리 사용](using-custom-assemblies-with-reports.md)  
  
  
