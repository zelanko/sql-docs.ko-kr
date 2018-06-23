---
title: SQL Server 2014 서비스 업데이트 설치 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c7601914ed32def54b153282a90b51629b1380b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185450"
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
  
 설치 프로그램에서 최신 버전의 적용 가능한 업데이트를 찾으면 이를 다운로드하고 현재의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로세스와 통합합니다. 제품 업데이트에는 누적 업데이트, 서비스 팩 또는 서비스 팩과 누적 업데이트가 포함될 수 있습니다. 제품 업데이트 기능은의 확장 언어는 [통합 설치 기능](http://go.microsoft.com/fwlink/?LinkId=219945) 에서 제공 했던 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] p c u 1입니다.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>설치 후 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 용 업데이트 설치  
 인스턴스가 설치 된 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 사용 가능한 모든 업데이트를 적용 하는 것이 좋습니다: 일반 배포 릴리스 (GDR-/ 중요 보안 업데이트)으로 서비스 팩 (SP)의 최신 사용 가능한 CU (누적 업데이트) 합니다.  
  
 릴리스 서비스의 유형에 따라 SQL Server 업데이트는 Microsoft Update (MU), Microsoft 다운로드 센터 및/또는 고객 지원 서비스 핫픽스 서버를 통해 제공 됩니다. SQL Server에 대 한 보안 및 중요 업데이트 (이러한 업데이트에 참여 하는 Windows Update를 통해 MU를 제어판에서 필요한 볼 수)를 Microsoft 업데이트에 의해 자동으로 제공 됩니다. 서비스 팩은 다운로드 센터 뿐만 아니라 선택 사항/중요 다운로드로 MU에서 사용할 수 있습니다. 누적 업데이트는 CU 기술 자료 문서에 제공 된 Microsoft 핫픽스 다운로드 서버에서 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [설치 마법사에서 SQL Server 2014 설치 &#40;설치&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [SQL server 2014 인스턴스에 기능 추가 &#40;설치&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [SQL Server 2014 설치 삭제](repair-a-failed-sql-server-installation.md)  
  
  