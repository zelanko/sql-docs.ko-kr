---
title: 실행 패키지 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageexecute.f1
- sql12.ssis.ssms.executepackage.f1
ms.assetid: 4f7a806d-4867-4d1f-bc65-b00c1caee7b6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 715bcfdda978801bac28e59246aeddc9ab76851e
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52418654"
---
# <a name="execute-package-dialog-box"></a>Execute Package Dialog Box
  **패키지 실행** 대화 상자를 사용하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 저장된 패키지를 실행할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지는 환경 변수에 값이 저장된 매개 변수를 포함할 수 있습니다. 이러한 패키지를 실행하려면 먼저 환경 변수 값을 제공하는 데 사용할 환경을 지정해야 합니다. 프로젝트에 여러 환경을 포함할 수는 있지만 실행할 때는 하나의 환경만 사용하여 환경 변수 값을 바인딩할 수 있습니다. 패키지에 사용되는 환경 변수가 없는 경우에는 환경이 필요하지 않습니다.  
  
 수행할 작업  
  
-   [패키지 실행 대화 상자 열기](#open_dialog)  
  
-   [일반 페이지에서 옵션 설정](#general)  
  
-   [매개 변수 탭에서 옵션 설정](#parameters)  
  
-   [연결 관리자 탭에서 옵션 설정](#connection)  
  
-   [고급 탭에서 옵션 설정](#advanced)  
  
-   [패키지 실행 대화 상자의 옵션 스크립팅](#script)  
  
##  <a name="open_dialog"></a> 패키지 실행 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     SSISDB 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **SSISDB** 노드를 확장합니다.  
  
4.  실행할 패키지가 들어 있는 폴더를 확장합니다.  
  
5.  패키지를 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.  
  
##  <a name="general"></a> 일반 페이지에서 옵션 설정  
 **환경** 을 선택하여 패키지 실행 시 적용할 환경을 지정합니다.  
  
##  <a name="parameters"></a> 매개 변수 탭에서 옵션 설정  
 **매개 변수** 탭에서 패키지 실행 시 사용되는 매개 변수 값을 수정합니다.  
  
##  <a name="connection"></a> 연결 관리자 탭에서 옵션 설정  
 연결 관리자 탭에서 패키지 연결 관리자 속성을 설정합니다.  
  
##  <a name="advanced"></a> 고급 탭에서 옵션 설정  
 고급 탭에서 속성 및 기타 패키지 설정을 관리합니다.  
  
 **추가**, **편집**, **제거**  
 속성을 추가, 편집 또는 제거하려면 클릭합니다.  
  
 **로깅 수준**  
 패키지 실행에 대한 로깅 수준을 선택합니다. 자세한 내용은 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)를 참조하세요.  
  
 **오류 덤프**  
 패키지 실행 시 오류가 발생할 경우 덤프 파일을 생성할지 여부를 지정합니다. 자세한 내용은 [Generating Dump Files for Package Execution](troubleshooting/generating-dump-files-for-package-execution.md)을 참조하세요.  
  
 **32비트 런타임**  
 패키지가 32비트 시스템에서 실행되도록 지정합니다.  
  
##  <a name="script"></a> 패키지 실행 대화 상자의 옵션 스크립팅  
 **패키지 실행** 대화 상자에 있는 동안 도구 모음의 **스크립트** 단추를 사용하여 [!INCLUDE[tsql](../includes/tsql-md.md)] 코드를 작성할 수도 있습니다. 생성된 스크립트는 **패키지 실행** 대화 상자에서 선택한 것과 동일한 옵션으로 [catalog.start_execution&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) 저장 프로시저를 호출합니다. 이 스크립트는 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]의 새 스크립트 창에 표시됩니다.  
  
  
