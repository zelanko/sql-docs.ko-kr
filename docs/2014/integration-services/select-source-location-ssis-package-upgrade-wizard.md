---
title: 원본 위치 (SSIS 패키지 업그레이드 마법사)를 선택 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectsourcelocation.f1
ms.assetid: 429f146e-edb4-4401-a225-f2c8468971c5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7d553bd07dd72ec136c5ec449f67b84dea2d6c57
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48228545"
---
# <a name="select-source-location-ssis-package-upgrade-wizard"></a>원본 위치 선택(SSIS 패키지 업그레이드 마법사)
  **원본 위치 선택** 페이지를 사용하여 패키지를 업그레이드할 원본을 지정할 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 또는 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 패키지 업그레이드 마법사를 실행한 경우에만 사용할 수 있습니다.  
  
 **SSIS 패키지 업그레이드 마법사를 실행하려면**  
  
-   [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>정적 옵션  
 **패키지 원본**  
 업그레이드할 패키지를 포함하는 저장소 위치를 선택합니다. 이 옵션에는 다음 표에 나열된 값이 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 시스템**|업그레이드할 패키지가 로컬 컴퓨터의 폴더에 있음을 나타냅니다.<br /><br /> 이러한 패키지를 업그레이드하기 전에 마법사가 원래 패키지를 백업하도록 하려면 원래 패키지를 파일 시스템에 저장해야 합니다. 자세한 내용은 방법 도움말 항목을 참조하십시오.|  
|**SSIS 패키지 저장소**|업그레이드할 패키지가 패키지 저장소에 있음을 나타냅니다. 패키지 저장소는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 관리하는 파일 시스템 폴더 집합으로 구성됩니다. 자세한 내용은 [패키지 관리&#40;SSIS 서비스&#41;](service/package-management-ssis-service.md)를 참조하세요.<br /><br /> 이 값을 선택하면 해당 **패키지 원본** 동적 옵션이 표시됩니다.|  
|**Microsoft SQL Server**|업그레이드할 패키지가 기존 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 있음을 나타냅니다.<br /><br /> 이 값을 선택하면 해당 **패키지 원본** 동적 옵션이 표시됩니다.|  
  
 **Folder**  
 업그레이드할 패키지를 포함하는 폴더의 이름을 입력하거나 **찾아보기** 를 클릭하여 폴더를 찾습니다.  
  
 **찾아보기**  
 업그레이드할 패키지를 포함하는 폴더를 찾습니다.  
  
## <a name="package-source-dynamic-options"></a>패키지 원본 동적 옵션  
  
### <a name="package-source--ssis-package-store"></a>패키지 원본 = SSIS 패키지 저장소  
 **Server**  
 업그레이드할 패키지가 있는 서버의 이름을 입력하거나 목록에서 이 서버를 선택합니다.  
  
### <a name="package-source--microsoft-sql-server"></a>패키지 원본 = Microsoft SQL Server  
 **Server**  
 업그레이드할 패키지가 있는 서버의 이름을 입력하거나 목록에서 이 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하여 서버에 연결하려면 선택합니다.  
  
 **SQL Server 인증 사용**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 연결하려면 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **사용자 이름**  
 서버에 연결할 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증에 사용할 사용자 이름을 입력합니다.  
  
 **암호**  
 서버에 연결할 때 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증에 사용할 암호를 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 패키지 업그레이드](install-windows/upgrade-integration-services-packages.md)  
  
  
