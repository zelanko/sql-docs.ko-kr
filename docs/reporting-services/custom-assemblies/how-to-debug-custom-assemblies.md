---
title: "방법: 사용자 지정 어셈블리 디버깅 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
caps.latest.revision: 44
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e33f560106e99062e89ec10bbe84de65a360118f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="how-to-debug-custom-assemblies"></a>방법: 사용자 지정 어셈블리 디버깅
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 수 있는 몇 가지 디버깅 도구는 사용자 지정 어셈블리 코드를 분석 하 고 오류를 찾는 제공 합니다. 사용하기에 가장 좋은 도구는 수행하려는 작업에 따라 달라집니다. 이 예에서는 [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]를 사용합니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 대한 사용자 지정 어셈블리 디자인, 개발 및 테스트를 위해 권장되는 방법은 테스트 보고서와 사용자 지정 어셈블리가 모두 포함된 솔루션을 만드는 것입니다.  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>단일 인스턴스의 Visual Studio를 사용하여 어셈블리를 디버깅하려면  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 사용하여 새 보고서 프로젝트를 만듭니다.  
  
     보고서 프로젝트를 만들 때 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]에서는 보고서 프로젝트를 포함할 솔루션이 만들어집니다.  
  
2.  새 클래스 라이브러리 프로젝트를 기존 솔루션에 추가합니다. 보고서 프로젝트가 시작 프로젝트로 설정되었는지 확인합니다. 이를 수행하는 방법은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설명서를 참조하십시오.  
  
3.  솔루션 탐색기에서 솔루션을 선택합니다.  
  
4.  에 **보기** 메뉴를 클릭 하 여 **속성 페이지**합니다.  
  
     **솔루션 속성 페이지** 대화 상자가 열립니다.  
  
5.  왼쪽된 창에서 확장 **공용 속성** 필요에 따라 클릭 **프로젝트 종속성**합니다. 보고서 프로젝트를 선택는 **프로젝트** 드롭 다운 목록입니다. 어셈블리 프로젝트를 선택는 **에 종속** 목록입니다.  
  
6.  클릭 **확인** 변경 내용을 저장 하 고 닫습니다는 **속성 페이지** 대화 상자.  
  
7.  솔루션 탐색기에서 사용자 지정 어셈블리 프로젝트를 선택합니다.  
  
8.  에 **보기** 메뉴를 클릭 하 여 **속성 페이지**합니다.  
  
     **프로젝트 속성 페이지** 대화 상자가 열립니다.  
  
9. 클릭는 **빌드** C# 프로젝트에 있는 경우 탭 또는 **컴파일** 탭에 있는 경우는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 프로젝트.  
  
10. 에 **빌드**/**컴파일** 페이지, 보고서 디자이너 폴더의 경로를 입력 합니다. 기본적으로 C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE 이것이)에 **출력 경로** 입력란. 그러면 보고서가 실행되기 전에 업데이트된 버전의 사용자 지정 어셈블리가 빌드되어 보고서 디자이너에 직접 배포됩니다.  
  
11. 보고서를 디자인하고 사용자 지정 어셈블리를 개발했으면 사용자 지정 어셈블리 코드에서 중단점을 설정합니다.  
  
12. 보고서를 실행 **DebugLocal** F5 키를 눌러 모드입니다. 보고서가 팝업 미리 보기 창에서 실행되면 디버거는 어셈블리의 실행 코드에 해당하는 중단점에서 멈춥니다. F11 키를 사용하여 사용자 지정 어셈블리 코드를 단계별로 분석합니다.  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>두 인스턴스의 Visual Studio를 사용하여 어셈블리를 디버깅하려면  
  
1.  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 시작하고 사용자 지정 어셈블리 프로젝트를 엽니다.  
  
2.  프로젝트를 빌드하고 사용자 지정 어셈블리 및 해당하는 .pdb 파일을 보고서 디자이너에 배포합니다. 배포에 대 한 자세한 내용은 참조 [사용자 지정 어셈블리 배포](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)합니다.  
  
3.  사용자 지정 어셈블리 코드를 별도의 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 인스턴스에서 열어 둔 상태로 사용자 지정 어셈블리가 사용된 보고서 프로젝트를 엽니다.  
  
4.  사용자 지정 어셈블리 프로젝트를 포함하는 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 인스턴스로 이동하고 코드에서 중단점을 설정합니다.  
  
5.  사용자 지정 어셈블리 프로젝트를 활성 창 상태로 클릭 **프로세스에 연결** 에 **디버그** 메뉴.  
  
     **프로세스에 연결** 대화 상자가 열립니다.  
  
6.  프로세스 목록에서 보고서 프로젝트에 해당 하는 devenv.exe 프로세스를 선택 하 고 클릭 **연결**합니다.  
  
7.  사용자 지정 어셈블리의 보고서에서 사용할 식을 정의하고 보고서를 디자인합니다.  
  
8.  보고서 디자인을 완료 했으면 클릭는 **미리 보기** 탭 합니다.  
  
     보고서가 실행되며 사용자 지정 어셈블리 코드는 미리 정의된 중단점에서 멈추게 됩니다.  
  
    > [!NOTE]  
    >  사용 하는 **미리 보기** 탭 어셈블리에 대 한 코드 권한을 적용 하지 않습니다. 모든 코드 액세스 보안 오류를 포함 하는 전체 테스트에 대 한 시작에서 보고서 프로젝트는 **DebugLocal** 구성 설정입니다.  
  
9. F11 키를 사용하여 코드를 단계별로 실행합니다. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]를 사용하여 디버깅하는 방법은 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설명서를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [보고서에서 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
