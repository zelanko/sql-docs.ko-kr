---
title: 패키지 관리 옵션 선택 (SSIS 패키지 업그레이드 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectpackagemgtoptions.f1
ms.assetid: 810fc020-51cd-43ed-9f35-af99b4f35947
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c71f254b0d0fb79e3ee8135c10d2d9ed715d3437
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66056025"
---
# <a name="select-package-management-options-ssis-package-upgrade-wizard"></a>패키지 관리 옵션 선택(SSIS 패키지 업그레이드 마법사)
  **패키지 관리 옵션 선택** 페이지를 사용하여 패키지 업그레이드 옵션을 지정할 수 있습니다.  
  
 **SSIS 패키지 업그레이드 마법사를 실행하려면**  
  
-   [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="options"></a>옵션  
 **새 공급자 이름을 사용하도록 연결 문자열 업데이트**  
 연결 문자열이 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]현재 버전의 다음 공급자에 대해 다음 이름을 사용하도록 업데이트합니다.  
  
-   OLE DB Provider for [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 업그레이드 마법사는 연결 관리자에 저장된 연결 문자열만 업데이트하며 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 식 언어 또는 스크립트 태스크의 코드를 사용하여 동적으로 생성된 연결 문자열은 업데이트하지 않습니다.  
  
 **업그레이드 패키지 유효성 검사**  
 업그레이드 패키지의 유효성을 검사하고 유효성 검사를 통과한 업그레이드 패키지만 저장합니다.  
  
 이 옵션을 선택하지 않으면 마법사는 업그레이드 패키지의 유효성을 검사하지 않습니다. 따라서 마법사는 패키지의 유효성 여부와 관계없이 모든 업그레이드 패키지를 저장합니다. 마법사는 마법사의 **대상 위치 선택** 페이지에서 지정한 대상에 업그레이드 패키지를 저장합니다.  
  
 유효성 검사로 인해 업그레이드 프로세스의 소요 시간이 늘어납니다. 성공적으로 업그레이드될 가능성이 높은 큰 패키지의 경우에는 이 옵션을 선택하지 않는 것이 좋습니다.  
  
 **새 패키지 ID 만들기**  
 업그레이드 패키지의 새 패키지 ID를 만듭니다.  
  
 **패키지 업그레이드 실패 시 업그레이드 프로세스 계속**  
 특정 패키지를 업그레이드할 수 없는 경우 [!INCLUDE[ssIS](../includes/ssis-md.md)] 패키지 업그레이드 마법사가 나머지 패키지를 계속 업그레이드하도록 지정합니다.  
  
 **패키지 이름 충돌**  
 마법사가 동일한 이름의 패키지를 처리하는 방법을 지정합니다. 이 옵션에는 다음 표에 나열된 값이 있습니다.  
  
 **기존 패키지 파일 덮어쓰기**  
 기존 패키지를 동일한 이름의 업그레이드 패키지로 바꿉니다.  
  
 **업그레이드 패키지 이름에 숫자 접미사 추가**  
 업그레이드 패키지의 이름에 숫자 접미사를 추가합니다.  
  
 **패키지 업그레이드 안 함**  
 패키지가 업그레이드되지 않도록 하고 마법사 완료 시 오류를 표시합니다.  
  
 이러한 옵션은 마법사의 **대상 위치 선택** 페이지에서 **원본 위치에 저장** 옵션을 선택한 경우 사용할 수 없습니다.  
  
 **구성 무시**  
 패키지 업그레이드를 사용 하는 동안 패키지 구성을 로드하지 않습니다. 이 옵션을 선택하면 패키지를 업그레이드 하는 데 필요한 시간이 줄어듭니다.  
  
 **원래 패키지 백업**  
 마법사가 **SSISBackupFolder** 폴더에 원래 패키지를 백업하도록 합니다. 마법사는 원래 패키지 및 업그레이드된 패키지가 포함된 폴더에 하위 폴더로 **SSISBackupFolder** 폴더를 만듭니다.  
  
> [!NOTE]  
>  이 옵션은 원래 패키지 및 업그레이드된 패키지가 파일 시스템의 동일한 폴더에 저장되도록 지정한 경우에만 사용할 수 있습니다.  
  
 자세한 내용은 [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 패키지 업그레이드](install-windows/upgrade-integration-services-packages.md)  
  
  
