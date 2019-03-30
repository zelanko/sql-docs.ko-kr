---
title: SQL Server 2014 서비스 업데이트 설치 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07f438f86a22b866351a0b83ee7634338f3ad2cd
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58657847"
---
# <a name="install-sql-server-2014-servicing-updates"></a>SQL Server 2014 서비스 업데이트 설치
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]용 업데이트 설치에 대한 정보를 제공합니다. 이 섹션에서는 다음과 같은 정보를 제공합니다.  
  
-   새로 설치하는 동안 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 용 업데이트 설치  
  
-   설치 후 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 용 업데이트 설치.  
  
 시스템이 최신 보안 업데이트로 업데이트되도록 고객이 적절한 시기에 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트를 확인하고 설치하는 것이 좋습니다.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-during-a-new-installation"></a>새로 설치하는 동안 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 용 업데이트 설치  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 최신 제품 업데이트를 주 제품 설치와 통합하여 주 제품과 해당 업데이트가 동시에 설치되게 할 수 있습니다. 제품 업데이트는 다음 위치에서 적용 가능한 업데이트를 검색할 수 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   WSUS(Windows Server Update Services)  
  
-   로컬 폴더  
  
-   네트워크 공유  
  
 설치 프로그램에서 최신 버전의 적용 가능한 업데이트를 찾으면 이를 다운로드하고 현재의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로세스와 통합합니다. 제품 업데이트에는 누적 업데이트, 서비스 팩 또는 서비스 팩과 누적 업데이트가 포함될 수 있습니다. 제품 업데이트 기능을 확장 합니다 [통합 설치 기능](https://go.microsoft.com/fwlink/?LinkId=219945) 에서 제공 했던 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1 합니다.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>설치 후 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 용 업데이트 설치  
 설치 된 인스턴스의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 모든 사용 가능한 업데이트를 적용 하는 것이 좋습니다. 일반 배포 릴리스 (GDR-중요/보안 업데이트)는 최신 사용 가능한 CU (누적 업데이트) 뿐만 아니라 서비스 팩 (SP).  
  
 릴리스를 서비스의 유형에 따라 SQL Server 업데이트가 Microsoft Update (MU), Microsoft 다운로드 센터 및/또는 고객 지원 서비스 핫픽스 서버를 통해 제공 됩니다. SQL Server에 대 한 보안 및 중요 업데이트 (해야 옵트인 Windows Update를 통해 MU를 제어판에서 이러한 업데이트를 볼 수)를 Microsoft 업데이트에서 자동으로 제공 됩니다. 서비스 팩은 선택 사항/중요 다운로드 다운로드 센터와 MU에서 사용할 수 있습니다. 누적 업데이트 CU 기술 자료 문서에 제공 된 Microsoft 핫픽스 다운로드 서버에서 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [설치 마법사에서 SQL Server 2014를 설치 &#40;설치&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [명령 프롬프트에서 업데이트를 설치](installing-updates-from-the-command-prompt.md) [는 인스턴스에 SQL Server 2014의 기능 추가 &#40;설치&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [SQL Server 2014 설치 삭제](repair-a-failed-sql-server-installation.md)  
  
  
