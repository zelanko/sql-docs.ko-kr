---
title: 대상 위치 (SSIS 패키지 업그레이드 마법사)를 선택 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectdestinationlocation.f1
ms.assetid: 89274a71-0ffe-4889-84df-f5a7d78459ef
caps.latest.revision: 19
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4754420ad4058e44e2bc07d3e68a18d076108c1e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287539"
---
# <a name="select-destination-location-ssis-package-upgrade-wizard"></a>대상 위치 선택(SSIS 패키지 업그레이드 마법사)
  **대상 위치 선택** 페이지를 사용하여 업그레이드된 패키지를 저장할 대상을 지정할 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 또는 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 패키지 업그레이드 마법사를 실행한 경우에만 사용할 수 있습니다.  
  
 **SSIS 패키지 업그레이드 마법사를 실행하려면**  
  
-   [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>정적 옵션  
 **원본 위치에 저장**  
 업그레이드된 패키지를 마법사의 **원본 위치 선택** 페이지에서 지정한 것과 동일한 위치에 저장합니다.  
  
 원래 패키지가 파일 시스템에 저장되는 상태에서 마법사가 이러한 패키지를 백업하도록 하려면 **원본 위치에 저장** 옵션을 선택합니다. 자세한 내용은 [SSIS 패키지 업그레이드 마법사를 사용하여 Integration Services 패키지 업그레이드](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)를 참조하세요.  
  
 **새 대상 위치 선택**  
 업그레이드된 패키지를 이 페이지에서 지정한 대상 위치에 저장합니다.  
  
 **패키지 원본**  
 업그레이드 패키지를 저장할 위치를 지정합니다. 이 옵션에는 다음 표에 나열된 값이 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**파일 시스템**|업그레이드된 패키지를 로컬 컴퓨터의 폴더에 저장함을 나타냅니다.|  
|**SSIS 패키지 저장소**|업그레이드된 패키지를 Integration Services 패키지 저장소에 저장함을 나타냅니다. 패키지 저장소는 Integration Services 서비스에서 관리하는 파일 시스템 폴더 집합으로 구성됩니다. 자세한 내용은 [패키지 관리&#40;SSIS 서비스&#41;](service/package-management-ssis-service.md)를 참조하세요.<br /><br /> 이 값을 선택하면 해당 **패키지 원본** 동적 옵션이 표시됩니다.|  
|**Microsoft SQL Server**|업그레이드된 패키지를 기존 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 저장함을 나타냅니다.<br /><br /> 이 값을 선택하면 해당 **패키지 원본** 동적 옵션이 표시됩니다.|  
  
 **Folder**  
 업그레이드된 패키지를 저장할 폴더의 이름을 입력하거나 **찾아보기** 를 클릭하여 폴더를 찾습니다.  
  
 **찾아보기**  
 업그레이드된 패키지를 저장할 폴더를 찾습니다.  
  
## <a name="package-source-dynamic-options"></a>패키지 원본 동적 옵션  
  
### <a name="package-source--ssis-package-store"></a>패키지 원본 = SSIS 패키지 저장소  
 **Server**  
 업그레이드 패키지를 저장할 서버의 이름을 입력하거나 목록에서 서버를 선택합니다.  
  
### <a name="package-source--microsoft-sql-server"></a>패키지 원본 = Microsoft SQL Server  
 **Server**  
 업그레이드 패키지를 저장할 서버의 이름을 입력하거나 목록에서 이 서버를 선택합니다.  
  
 **Windows 인증 사용**  
 Windows 인증을 사용하여 서버에 연결하려면 선택합니다.  
  
 **SQL Server 인증 사용**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 연결하려면 선택합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우 사용자 이름과 암호를 입력해야 합니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 연결할 때 사용할 사용자 이름을 입력합니다.  
  
 **암호**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 서버에 연결할 때 사용할 암호를 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 패키지 업그레이드](install-windows/upgrade-integration-services-packages.md)  
  
  
