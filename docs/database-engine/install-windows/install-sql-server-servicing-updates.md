---
title: SQL Server 서비스 업데이트 설치 | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.prod_service: install
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1176cab174ca97fd155cf336a643d035d15b3904
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-servicing-updates"></a>SQL Server 서비스 업데이트 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]용 업데이트 설치에 대한 정보를 제공합니다. 이 섹션에서는 다음과 같은 정보를 제공합니다.
  
- 새로 설치하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 용 업데이트 설치  
  
- 설치 후 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 용 업데이트 설치.  
  
시스템이 최신 보안 업데이트를 유지하도록 적절한 시기에 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트를 설치합니다.  
  
## <a name="installing-updates-for-includenoversionincludesssnoversion-mdmd-during-a-new-installation"></a>새로 설치하는 동안 [!INCLUDE[noVersion](../../includes/ssNoVersion-md.md)] 용 업데이트 설치  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 최신 제품 업데이트를 주 제품 설치와 통합하여 주 제품과 해당 업데이트가 동시에 설치되게 할 수 있습니다. 제품 업데이트는 다음 위치에서 적용 가능한 업데이트를 검색할 수 있습니다.  
  
- [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
- WSUS(Windows Server Update Services)  
  
- 로컬 폴더  
  
- 네트워크 공유  
  
설치 프로그램에서 최신 버전의 적용 가능한 업데이트를 찾으면 이를 다운로드하고 현재의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로세스와 통합합니다. 제품 업데이트에는 누적 업데이트, 서비스 팩 또는 서비스 팩과 누적 업데이트가 포함될 수 있습니다.  
  
## <a name="installing-updates-for-includessnoversionincludesssnoversion-mdmd-after-it-has-already-been-installed"></a>설치 후 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] 용 업데이트 설치  
[!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]인스턴스가 설치된 경우 GDR(General Distribution Release), SP(서비스 팩) 및 CU(누적 업데이트)를 포함한 최신 보안 업데이트와 중요 업데이트를 적용하는 것이 좋습니다. 자세한 내용은 [2016년 3월에 발표한 SQL Server ISM(증분 서비스 모델)](http://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/)을 참조하세요.

> [!NOTE]
> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터는 단순화되고 예측 가능한 일반 서비스 주기를 채택하고 있으며 SP(서비스 팩)는 더 이상 제공되지 않습니다. CU(누적 업데이트)만, 필요한 경우 GDR(General Distribution Release)
> 자세한 내용은 [2017년 9월에 발표한 SQL Server에 대한 MSM(Modern Servicing Model)](http://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server/)을 참조하세요.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트는 MU( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update), WSUS(Windows Server Update Services) 및 Microsoft 다운로드 센터를 통해 제공됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 용 보안 및 중요 업데이트는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 통해 제공되며 이러한 업데이트를 보려면 제어판의 Windows Update 애플릿을 통해 MU를 선택해야 합니다.  
  
[!INCLUDE[msCoName](../../includes/msconame-md.md)] Update를 통해 업데이트를 받으면 무인 모드에서 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 최신 버전으로 업데이트합니다. 더 많은 유연성이 필요하거나 인터넷 또는 WSUS에 액세스할 수 없는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Download Center에서 업데이트를 얻어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[설치 마법사에서 SQL Server 설치 &#40;설치&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
[SQL Server 인스턴스에 기능 추가 &#40;Setup&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)
[실패한 SQL Server 설치 복구](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)  

