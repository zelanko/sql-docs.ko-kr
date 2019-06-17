---
title: 배포 유틸리티를 사용 하 여 패키지 배포 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], installing
- installing packages
- dependencies [Integration Services]
- deploying packages [Integration Services], installing
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 73b71e83f3b0f0f895b2cc5b8fd3495fb4893a32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059619"
---
# <a name="deploy-packages-by-using-the-deployment-utility"></a>배포 유틸리티를 사용한 패키지 배포
  다른 컴퓨터에 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 패키지를 설치하기 위해 배포 유틸리티를 빌드한 다음에는 먼저 대상 컴퓨터에 배포 폴더를 복사해야 합니다.  
  
 배포 폴더의 경로는 배포 유틸리티를 만든 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트의 DeploymentOutputPath 속성에 지정됩니다. 기본 경로는 bin\Deployment이며 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트에 상대적입니다. 자세한 내용은 [Create a Deployment Utility](../../2014/integration-services/create-a-deployment-utility.md)를 참조하세요.  
  
 패키지 설치 마법사를 사용하여 패키지를 설치합니다. 마법사를 시작하려면 배포 폴더를 서버로 복사한 다음 배포 유틸리티 파일을 두 번 클릭합니다. 이 파일의 이름은 \<프로젝트 이름>.SSISDeploymentManifest이며 대상 컴퓨터의 배포 폴더에 있습니다.  
  
> [!NOTE]  
>  배포하는 패키지의 버전에 따라 여러 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 함께 설치할 경우 오류가 발생할 수 있습니다. 이 오류는 .SSISDeploymentManifest 파일 이름 확장명이 모든 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]버전에서 동일하기 때문에 발생할 수 있습니다. 파일을 두 번 클릭하면 가장 최근에 설치된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]버전의 설치 관리자가 호출되며 이 버전이 배포 유틸리티 파일과 동일한 버전이 아닐 수 있습니다. 이 문제를 해결하려면 명령줄에서 정확한 버전의 dtsinstall.exe를 실행한 후 배포 유틸리티 파일의 경로를 입력합니다.  
  
 패키지 설치 마법사는 파일 시스템 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 패키지를 설치하는 단계를 안내합니다. 다음과 같은 방법으로 설치를 구성할 수 있습니다.  
  
-   패키지를 설치할 위치 유형 및 위치 선택  
  
-   패키지 종속 파일을 설치할 위치 선택  
  
-   대상 서버에 패키지 설치 후 패키지의 유효성 검사  
  
 패키지의 파일 기반 종속성은 항상 파일 시스템에 설치됩니다. 파일 시스템에 패키지를 설치한 경우 패키지에 지정한 것과 동일한 폴더에 종속성이 설치됩니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 패키지를 설치하는 경우 파일 기반 종속성을 저장할 폴더를 지정할 수 있습니다.  
  
 패키지에 대상 컴퓨터에서 사용하기 위해 수정할 구성이 포함된 경우 마법사를 사용하여 속성 값을 업데이트할 수 있습니다.  
  
 패키지 설치 마법사를 사용하여 패키지를 설치하는 방법 이외에도 **dtutil** 명령 프롬프트 유틸리티를 사용하여 패키지를 복사 및 이동할 수 있습니다. 자세한 내용은 [dtutil Utility](dtutil-utility.md)를 참조하세요.  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>SQL Server 인스턴스에 패키지를 배포하려면  
  
1.  대상 컴퓨터에서 배포 폴더를 엽니다.  
  
2.  매니페스트 파일 \<프로젝트 이름>.SSISDeploymentManifest를 두 번 클릭하여 패키지 설치 마법사를 시작합니다.  
  
3.  **SSIS 패키지 배포** 페이지에서 **SQL Server 배포** 옵션을 선택합니다.  
  
4.  필요에 따라 **설치 후 패키지 유효성 검사** 를 선택하여 대상 서버에 패키지를 설치한 후 패키지의 유효성을 검사합니다.  
  
5.  **대상 SQL Server 지정** 페이지에서 패키지를 설치할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 지정하고 인증 모드를 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 선택하는 경우 사용자 이름 및 암호를 지정해야 합니다.  
  
6.  **설치 폴더 선택** 페이지에서 패키지 종속성에 의해 설치될 파일 시스템 내의 폴더를 지정합니다.  
  
7.  패키지가 구성을 포함하는 경우 구성 패키지 페이지에서 **값** 목록의 값을 업데이트하여 구성을 편집할 수 있습니다.  
  
8.  설치 후에 패키지의 유효성 검사를 수행하도록 선택한 경우 배포된 패키지의 유효성 검사 결과를 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [배포 패키지 &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
