---
title: 저장 프로시저 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7beb77adf595b055a6c1e4a7543b428a06ce7640
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62703086"
---
# <a name="creating-stored-procedures"></a>저장 프로시저 만들기
  모든 저장 프로시저는 CLR(공용 언어 런타임) 또는 COM(구성 요소 개체 모델) 클래스와 연결되어야 사용할 수 있습니다. 이 클래스는 일반적으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ACTIVEX® DLL (동적 연결 라이브러리) 형식으로 서버에 설치 되 고 서버나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 어셈블리로 등록 되어야 합니다.  
  
 저장 프로시저는 서버나 데이터베이스에 등록됩니다. 서버 저장 프로시저는 모든 쿼리 컨텍스트에서 호출할 수 있지만 데이터베이스 저장 프로시저는 데이터베이스 컨텍스트가 저장 프로시저가 정의되어 있는 데이터베이스인 경우에만 액세스할 수 있습니다. 한 어셈블리의 함수에서 다른 어셈블리의 함수를 호출하는 경우 두 어셈블리를 모두 동일한 컨텍스트(서버 또는 데이터베이스)에 등록해야 합니다. 서버 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에 배포 된 데이터베이스의 경우를 사용 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 하 여 어셈블리를 등록할 수 있습니다. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 디자이너를 사용하여 프로젝트에 어셈블리를 등록할 수 있습니다.  
  
> [!IMPORTANT]  
>  COM 어셈블리는 보안 위험을 내포할 수 있습니다. 이러한 위험 및 기타 고려 사항으로 인해 COM 어셈블리는 [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]에서 더 이상 사용되지 않습니다. COM 어셈블리는 후속 릴리스에서 지원되지 않을 수 있습니다.  
  
## <a name="registering-a-server-assembly"></a>서버 어셈블리 등록  
 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 서버 어셈블리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 아래의 어셈블리 폴더에 나열됩니다. 서버 어셈블리는 .NET(CLR) 어셈블리와 COM 라이브러리를 모두 포함할 수 있습니다.  
  
### <a name="to-create-a-server-assembly"></a>서버 어셈블리를 만들려면  
  
1.  개체 탐색기 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 인스턴스를 확장 하 고 **어셈블리** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새 어셈블리**를 클릭 합니다. 그러면 **서버 어셈블리 등록** 대화 상자가 표시 됩니다.  
  
2.  **유형** 에 대해 어셈블리 유형을 지정 합니다.  
  
    -   관리 코드(CLR) DLL의 경우 .NET 어셈블리를 지정합니다.  
  
    -   네이티브 코드(COM) DLL의 경우 COM DLL을 지정합니다.  
  
3.  **파일 이름**에 저장 프로시저를 포함 하는 DLL을 지정 합니다.  
  
4.  **어셈블리 이름**에 어셈블리의 이름을 지정 합니다.  
  
5.  저장 프로시저를 디버깅 하는 데 사용 하려는 라이브러리의 디버그 빌드 인 경우 **디버그 정보 포함** 확인란을 선택 합니다. 저장 프로시저를 디버깅 하는 방법에 대 한 자세한 내용은 [저장 프로시저 디버깅](debugging-stored-procedures.md)을 참조 하십시오.  
  
6.  **확인** 을 클릭 하 여 어셈블리를 즉시 등록 하거나 대화 상자 도구 모음에서 **스크립트** 메뉴의 명령을 클릭 하 여 등록 작업을 쿼리 창, 파일 또는 클립보드에 스크립팅할 수 있습니다.  
  
 서버 어셈블리를 등록 한 후 개체 탐색기에서 어셈블리를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 하 여 서버 어셈블리를 구성할 수 있습니다.  
  
## <a name="registering-a-database-assembly-on-the-server"></a>서버에서 데이터베이스 어셈블리 등록  
 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 데이터베이스 어셈블리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 아래의 어셈블리 폴더에 나열됩니다. 데이터베이스 어셈블리는 .NET(CLR) 어셈블리와 COM 라이브러리를 모두 포함할 수 있습니다.  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>서버에서 데이터베이스 어셈블리를 등록하려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 인스턴스를 확장 하 고 **어셈블리** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새 어셈블리**를 클릭 합니다. **데이터베이스 어셈블리 등록** 대화 상자가 표시 됩니다.  
  
2.  **유형** 에 대해 어셈블리 유형을 지정 합니다.  
  
    -   관리 코드(CLR) DLL의 경우 .NET 어셈블리를 지정합니다.  
  
    -   네이티브 코드(COM) DLL의 경우 COM DLL을 지정합니다.  
  
3.  **파일 이름**에 저장 프로시저를 포함 하는 DLL을 지정 합니다.  
  
4.  **어셈블리 이름**에 어셈블리의 이름을 지정 합니다.  
  
5.  저장 프로시저를 디버깅 하는 데 사용 하려는 라이브러리의 디버그 빌드 인 경우 **디버그 정보 포함** 확인란을 선택 합니다. 저장 프로시저를 디버깅 하는 방법에 대 한 자세한 내용은 [저장 프로시저 디버깅](debugging-stored-procedures.md)을 참조 하십시오.  
  
6.  **확인** 을 클릭 하 여 어셈블리를 즉시 등록 하거나 대화 상자 도구 모음에서 **스크립트** 메뉴의 명령을 클릭 하 여 등록 작업을 쿼리 창, 파일 또는 클립보드에 스크립팅할 수 있습니다.  
  
 데이터베이스 어셈블리를 등록 한 후 개체 탐색기에서 어셈블리를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 하 여 데이터베이스 어셈블리를 구성할 수 있습니다.  
  
## <a name="registering-a-database-assembly-in-a-project"></a>프로젝트에 데이터베이스 어셈블리 등록  
 
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 데이터베이스 어셈블리는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 아래의 어셈블리 폴더에 나열됩니다. 데이터베이스 어셈블리는 .NET(CLR) 어셈블리와 COM 라이브러리를 모두 포함할 수 있습니다.  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>Analysis Service 프로젝트에서 데이터베이스 어셈블리를 만들려면  
  
1.  개체 탐색기에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 인스턴스를 확장 하 고 **어셈블리** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새 어셈블리 참조**를 클릭 합니다. **참조 추가** 대화 상자가 표시 됩니다. **참조 추가** 대화 상자의 **.net** 탭에는 기존 .net (CLR) 어셈블리가 나열 되 고 **프로젝트** 탭에는 프로젝트가 나열 됩니다.  
  
2.  기존 구성 요소나 프로젝트를 클릭 한 다음 **추가** 를 클릭 하 여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 추가할 수 있습니다. COM DLL에 대 한 참조를 추가 하려면 **찾아보기** 탭을 클릭 하 여 파일을 찾습니다. **선택한 프로젝트 및 구성 요소** 목록에는 프로젝트에 추가할 각 구성 요소의 이름, 유형, 버전 및 위치가 표시 됩니다.  
  
3.  추가할 구성 요소를 모두 선택 했으면 **확인** 을 클릭 하 여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 추가 합니다.  
  
## <a name="script-format-for-an-assembly"></a>어셈블리 스크립트 형식  
 .NET 어셈블리 등록 과정은 매우 단순합니다. .NET 어셈블리는 다음 형식을 사용하여 이진 형식으로 데이터베이스에 추가됩니다.  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>참고 항목  
 [다차원 모델 어셈블리 관리](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [저장 프로시저 정의](defining-stored-procedures.md)  
  
  
