---
title: Integration Services 프로젝트 변환 마법사 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.migrationwizard.f1
ms.assetid: a192b094-4d0f-4c21-b911-460ec844a49f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9c077fdb85612c5e3f574d9d0236b07f149b9c3a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057983"
---
# <a name="integration-services-project-conversion-wizard"></a>Integration Services 프로젝트 변환 마법사
  **Integration Services 프로젝트 변환 마법사** 는 프로젝트를 프로젝트 배포 모델로 변환합니다.  
  
> [!NOTE]  
>  프로젝트에 하나 이상의 데이터 원본이 포함된 경우 프로젝트 변환이 완료되면 데이터 원본이 제거됩니다. 프로젝트의 패키지에서 공유할 수 있는 데이터 원본에 대한 연결을 만들려면 프로젝트 수준에서 연결 관리자를 추가합니다. 자세한 내용은 [패키지에서 연결 관리자 추가, 삭제 또는 공유](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)을 참조하세요.  
  
 **수행 작업**  
  
-   [Integration Services 프로젝트 변환 마법사 열기](#open_dialog)  
  
-   [패키지 찾기 페이지에서 옵션 설정](#locate)  
  
-   [패키지 선택 페이지에서 옵션 설정](#selectPackages)  
  
-   [대상 선택 페이지에서 옵션 설정](#destination)  
  
-   [프로젝트 속성 지정 페이지에서 옵션 설정](#projectProperties)  
  
-   [패키지 실행 태스크 업데이트 페이지에서 옵션 설정](#executePackage)  
  
-   [구성 선택 페이지에서 옵션 설정](#configurations)  
  
-   [매개 변수 만들기 페이지에서 옵션 설정](#createParameters)  
  
-   [매개 변수 구성 페이지에서 옵션 설정](#configureParameters)  
  
-   [검토 페이지에서 옵션 설정](#review)  
  
-   [변환 수행에서 옵션 설정](#conversion)  
  
##  <a name="open_dialog"></a> Integration Services 프로젝트 변환 마법사 열기  
 다음 중 하나를 수행하여 **Integration Services 프로젝트 변환** 마법사를 엽니다.  
  
-   [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에서 프로젝트를 열고 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **프로젝트 배포 모델로 변환**을 클릭합니다.  
  
-   [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]의 개체 탐색기에서 **프로젝트** 노드를 마우스 오른쪽 단추로 클릭하고 **패키지 가져오기**를 선택합니다.  
  
 **Integration Services 프로젝트 변환 마법사** 를 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 에서 실행하는지 아니면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 실행하는지에 따라 수행되는 변환 태스크가 다릅니다. 자세한 내용은 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)을 참조하세요.  
  
##  <a name="locate"></a> 패키지 찾기 페이지에서 옵션 설정  
  
> [!NOTE]  
>  **패키지 찾기** 페이지는 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서 마법사를 실행할 때만 사용할 수 있습니다.  
  
 **원본** 드롭다운 목록에서 **파일 시스템** 을 선택하면 페이지에 다음 옵션이 표시됩니다. 패키지가 파일 시스템에 있으면 이 옵션을 선택합니다.  
  
 **Folder**  
 패키지 경로를 입력하거나 **찾아보기**를 클릭하여 패키지로 이동합니다.  
  
 **원본** 드롭다운 목록에서 **SSIS 패키지 저장소**를 선택하면 페이지에 다음 옵션이 표시됩니다. 패키지 저장소에 대한 자세한 내용은 [패키지 관리&#40;SSIS 서비스&#41;](service/package-management-ssis-service.md)를 참조하세요.  
  
 **Server**  
 서버 이름을 입력하거나 서버를 선택합니다.  
  
 **Folder**  
 패키지 경로를 입력하거나 **찾아보기**를 클릭하여 패키지로 이동합니다.  
  
 **원본** 드롭다운 목록에서 **Microsoft SQL Server** 를 선택하면 페이지에 다음 옵션이 표시됩니다. 패키지가 Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 있으면 이 옵션을 선택합니다.  
  
 **Server**  
 서버 이름을 입력하거나 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 Microsoft Windows 인증 모드에서는 사용자가 Windows 사용자 계정을 통해 연결할 수 있습니다. Windows 인증을 사용하면 사용자 이름 또는 암호를 제공할 필요가 없습니다.  
  
 **SQL Server 인증 사용**  
 사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인 계정이 설정되었는지와 지정한 암호가 이전에 기록한 암호와 일치하는지를 확인하여 연결을 인증합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에 로그인 계정이 설정되어 있지 않으면 인증이 실패하고 오류 메시지가 나타납니다.  
  
 **사용자 이름**  
 SQL Server 인증을 사용할 경우 사용자 이름을 지정합니다.  
  
 **암호**  
 SQL Server 인증을 사용할 경우 암호를 제공합니다.  
  
 **Folder**  
 패키지 경로를 입력하거나 **찾아보기**를 클릭하여 패키지로 이동합니다.  
  
##  <a name="selectPackages"></a> 패키지 선택 페이지에서 옵션 설정  
 **패키지 이름**  
 패키지 파일을 나열합니다.  
  
 **상태**  
 패키지를 프로젝트 배포 모델로 변환할 준비가 되었는지를 나타냅니다.  
  
 **메시지**  
 패키지와 연결된 메시지를 표시합니다.  
  
 **암호**  
 패키지와 연결된 암호를 표시합니다. 암호 텍스트는 숨겨져 있습니다.  
  
 **선택 항목에 적용**  
 **암호** 입력란의 암호를 선택한 패키지에 적용하려면 클릭합니다.  
  
 **새로 고침**  
 패키지 목록을 새로 고칩니다.  
  
##  <a name="destination"></a> 대상 선택 페이지에서 옵션 설정  
 이 페이지에서 새 프로젝트 배포 파일(.ispac)의 이름과 경로를 지정하거나 기존 파일을 선택합니다.  
  
> [!NOTE]  
>  **대상 선택** 페이지는 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서 마법사를 실행할 때만 사용할 수 있습니다.  
  
 **출력 경로**  
 배포 파일에 대한 경로를 입력하거나 **찾아보기**를 클릭하여 해당 파일로 이동합니다.  
  
 **프로젝트 이름**  
 프로젝트 이름을 입력합니다.  
  
 **보호 수준**  
 보호 수준을 선택합니다. 자세한 내용은 [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md)을 참조하세요.  
  
 **프로젝트 설명**  
 프로젝트에 대한 선택적 설명을 입력합니다.  
  
##  <a name="projectProperties"></a> 프로젝트 속성 지정 페이지에서 옵션 설정  
  
> [!NOTE]  
>  **프로젝트 속성 지정** 페이지는 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에서 마법사를 실행할 때만 사용할 수 있습니다.  
  
 **프로젝트 이름**  
 프로젝트 이름을 나열합니다.  
  
 **보호 수준**  
 프로젝트에 포함된 패키지에 대한 보호 수준을 선택합니다. 보호 수준에 대한 자세한 내용은 [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md)를 참조하십시오.  
  
 **프로젝트 설명**  
 선택적인 프로젝트 설명을 입력합니다.  
  
##  <a name="executePackage"></a> 패키지 실행 태스크 업데이트 페이지에서 옵션 설정  
 프로젝트 기반 참조를 사용할 수 있도록 패키지 실행 태스크 업데이트가 패키지에 포함되었습니다. 자세한 내용은 [Execute Package Task Editor](../../2014/integration-services/execute-package-task-editor.md)을 참조하세요.  
  
 **부모 패키지**  
 패키지 실행 태스크를 사용하여 자식 패키지를 실행하는 패키지의 이름을 나열합니다.  
  
 **태스크 이름**  
 패키지 실행 태스크의 이름을 나열합니다.  
  
 **원래 참조**  
 자식 패키지의 현재 경로를 나열합니다.  
  
 **참조 할당**  
 프로젝트에 저장된 자식 패키지를 선택합니다.  
  
##  <a name="configurations"></a> 구성 선택 페이지에서 옵션 설정  
 매개 변수로 대체하려고 하는 패키지 구성을 선택합니다.  
  
 **패키지**  
 패키지 파일을 나열합니다.  
  
 **형식**  
 XML 구성과 같은 구성 유형을 나열합니다.  
  
 **구성 문자열**  
 구성 파일의 경로를 나열합니다.  
  
 **상태**  
 구성에 대한 상태 메시지를 표시합니다. 전체 메시지 텍스트를 보려면 메시지를 클릭합니다.  
  
 **구성 추가**  
 다른 프로젝트에 포함된 패키지 구성을 매개 변수로 바꾸려는 사용 가능한 구성 목록에 추가합니다. 파일 시스템 또는 SQL Server에 저장된 구성을 선택할 수 있습니다.  
  
 **새로 고침**  
 구성 목록을 새로 고치려면 클릭합니다.  
  
 **변환 후 구성을 모든 패키지에서 제거**  
 이 옵션을 선택하여 프로젝트에서 모든 구성을 제거하는 것이 좋습니다.  
  
 이 옵션을 선택하지 않으면 매개 변수로 바꾸려고 선택한 구성만 제거됩니다.  
  
##  <a name="createParameters"></a> 매개 변수 만들기 페이지에서 옵션 설정  
 각 구성 속성에 대한 매개 변수 이름과 범위를 선택합니다.  
  
 **패키지**  
 패키지 파일을 나열합니다.  
  
 **매개 변수 이름**  
 매개 변수 이름을 나열합니다.  
  
 **범위**  
 패키지 또는 프로젝트 중에서 매개 변수 범위를 선택합니다.  
  
##  <a name="configureParameters"></a> 매개 변수 구성 페이지에서 옵션 설정  
 **이름**  
 매개 변수 이름을 나열합니다.  
  
 **범위**  
 매개 변수의 범위를 나열합니다.  
  
 **Value**  
 매개 변수 값을 나열합니다.  
  
 매개 변수 속성을 구성하려면 값 필드 옆에 있는 줄임표 단추를 클릭합니다.  
  
 **매개 변수 정보 설정** 대화 상자에서 매개 변수 값을 편집할 수 있습니다. 패키지를 실행할 때 매개 변수 값을 제공해야 하는지 여부를 지정할 수도 있습니다.  
  
 매개 변수 옆에 있는 찾아보기 단추를 클릭하여 **에서** 구성 **대화 상자의** 매개 변수 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]페이지에 있는 값을 수정할 수 있습니다. **매개 변수 값 설정** 대화 상자가 표시됩니다.  
  
 **매개 변수 정보 설정** 대화 상자에는 매개 변수 값의 데이터 형식 및 매개 변수의 원본도 나열됩니다.  
  
##  <a name="review"></a> 검토 페이지에서 옵션 설정  
 **검토** 페이지를 사용하여 프로젝트 변환을 위해 선택한 옵션을 확인합니다.  
  
 **이전**  
 옵션을 변경하려면 클릭합니다.  
  
 **변환**  
 프로젝트를 프로젝트 배포 모델로 변환하려면 클릭합니다.  
  
##  <a name="conversion"></a> 변환 수행에서 옵션 설정  
 변환 수행 페이지에는 프로젝트 변환 상태가 표시됩니다.  
  
 **동작**  
 특정 변환 단계를 나열합니다.  
  
 **결과**  
 각 변환 단계의 상태를 나열합니다. 자세한 내용을 보려면 상태 메시지를 클릭하십시오.  
  
 프로젝트 변환은 프로젝트가 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에 저장될 때까지 저장되지 않습니다.  
  
 **보고서 저장**  
 프로젝트 변환 요약을 .xml 파일로 저장하려면 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Deploy Projects to Integration Services Server](../../2014/integration-services/deploy-projects-to-integration-services-server.md)  
  
  
