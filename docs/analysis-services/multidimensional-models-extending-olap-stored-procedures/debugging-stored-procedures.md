---
title: 저장된 프로시저를 디버깅 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d37eebfad3f8a3e89dc65ad9602f4b5d61b5072e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="debugging-stored-procedures"></a>저장 프로시저 디버깅
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 저장 프로시저는 실제로 C#이나 다른 CLR 또는 COM 언어로 작성되는 CLR 또는 COM 라이브러리(대개 DLL)입니다. 따라서 저장 프로시저를 디버깅하는 것은 Visual Studio 디버깅 환경에서 다른 응용 프로그램을 디버깅하는 것과 매우 유사합니다. 통합된 디버깅 기능을 사용하여 Visual Studio 개발 환경에서 저장 프로시저를 디버깅합니다. 이를 통해 프로시저 위치에서 중지하고 메모리와 레지스터 값을 검사하고 변수를 변경하고 메시지 트래픽을 관찰하고 코드 작동 방식을 자세히 살펴볼 수 있습니다.  
  
### <a name="to-debug-a-stored-procedure"></a>저장 프로시저를 디버깅하려면  
  
1.  Visual Studio에서 DLL을 만드는 데 사용되는 프로젝트를 엽니다.  
  
2.  디버깅할 프로시저에 해당하는 메서드나 함수에 중단점을 만듭니다.  
  
3.  Visual Studio를 사용하여 저장 프로시저 DLL의 디버그 빌드를 만듭니다.  
  
4.  서버에 DLL을 배포합니다. 서버에 DLL을 배포 하는 방법에 대 한 자세한 내용은 참조 [저장 프로시저 만들기](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/creating-stored-procedures.md)합니다.  
  
5.  테스트할 저장 프로시저를 호출하는 응용 프로그램이 필요합니다. 이러한 응용 프로그램이 없는 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 MDX 쿼리 편집기를 사용하여 테스트할 저장 프로시저를 호출하는 MDX 쿼리를 만들 수 있습니다.  
  
6.  Visual Studio에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로세스(Msmdsrv.exe)에 연결합니다.  
  
    1.  **디버그** 메뉴 선택 **프로세스 toProcess**합니다.  
  
    2.  에 **프로세스 toProcess** 대화 상자에서 **모든 사용자의 프로세스 표시**합니다.  
  
    3.  에 **사용 가능한 프로세스** 목록에서 **프로세스** 열을 클릭 하 여 **Msmdsrv.exe**합니다. 서버에서 실행 중인 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 여러 개인 경우 사용할 인스턴스의 ID로 프로세스를 식별해야 합니다.  
  
    4.  에 **연결할** 텍스트 상자에서 적절 한 프로그램 유형을 선택 되어 있는지 확인 합니다. CLR DLL에 대 한 클릭 **선택**, 클릭 **다음 코드 형식 디버깅**, 클릭 **관리**, 클릭 **확인**합니다. COM DLL에 대 한 클릭 **선택**, 클릭 **다음 코드 형식 디버깅**, 클릭 **네이티브**, 클릭 **확인**합니다.  
  
    5.  클릭 **연결**합니다.  
  
7.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 저장 프로시저를 호출하는 MDX 스크립트나 프로그램을 실행합니다. 중단점이 있는 행에 도달하면 디버거가 중단됩니다. 조사식 창에서 변수를 평가하고 로컬을 보고 코드를 단계별로 실행할 수 있습니다.  
  
 라이브러리를 디버깅하는 데 문제가 있는 경우 해당 프로그램 데이터베이스(PDB) 파일이 서버의 배포 위치로 복사되었는지 확인합니다. 등록이나 배포 과정에서 이 파일이 복사되지 않은 경우에는 DLL과 동일한 위치로 직접 파일을 복사해야 합니다. 네이티브 코드(COM DLL)의 경우 PDB 파일은 \debug 하위 디렉터리에 있습니다. 관리 코드(CLR DLL)의 경우 이 파일은 \WINDEBUG 하위 디렉터리에 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델 어셈블리 관리](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [저장된 프로시저 정의](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
