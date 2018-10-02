---
title: SQL Server 설치 계획 | Microsoft 문서
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: quickstart
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 456458c98ddee8115f715839c6e13c3c3680196a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713181"
---
# <a name="planning-a-sql-server-installation"></a>SQL Server 설치 계획
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하려면 다음 단계를 수행하십시오.  
  
-   설치 요구 사항, 시스템 구성 검사 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치를 위한 보안 고려 사항을 검토합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 설치하거나 이후 버전으로 업그레이드합니다. 업그레이드하기 전에 [SQL Server로 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)를 검토합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 구성합니다.  
  
 소프트웨어 사용이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 볼륨 라이선스 계약 또는 공급 업체와의 ISV  또는 OEM  계약과 같은 별도의 계약에 의해 관리되지 않는 한 설치 방법에 상관없이 개인 또는 업체 대표로서 소프트웨어 사용 조건에 대한 동의를 확인해야 합니다.  
  
 사용 조건은 검토 및 동의를 위해 설치 프로그램 사용자 인터페이스에 표시됩니다. 무인 설치(`/Q` 또는 `/QS` 매개 변수 사용)에는 `/IAcceptSQLServerLicenseTerms` 매개 변수가 포함되어야 합니다. [Microsoft SQL Server 사용 조건 및 정보](http://www.microsoft.com/Licensing/product-licensing/sql-server.aspx)에서 사용 조건을 별도로 다운로드하여 검토하세요. 볼륨 라이선스 조건에 대해서는 [Licensing Terms and Documentation](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53)(사용 조건 및 설명서)을 참조하세요. 이전 버전의 SQL Server에 대해서는 [Microsoft 소프트웨어 라이선스 조건](http://go.microsoft.com/fwlink/?LinkID=148209)을 참조하세요.  
  
> [!NOTE]  
>  소프트웨어의 수령 방법(예: [!INCLUDE[msCoName](../../includes/msconame-md.md)] 볼륨 라이선스를 통해 수령)에 따라 사용자의 소프트웨어 사용에 추가 조건이 적용될 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SQL Server 설치의 새로운 기능](../../sql-server/install/what-s-new-in-sql-server-installation.md)  
 이 문서에서는 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 새로운 기능 및 향상된 기능에 대해 자세히 설명합니다.  
  
 [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
 이 문서에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스를 설치 및 실행하기 위한 최소 하드웨어 및 소프트웨어 요구 사항을 나열합니다.  
  
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하기 전과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치한 후에 고려해야 하는 보안 권장 사항에 대해 설명합니다.  
  
 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이 릴리스에서 기본 서비스 구성과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 그리고 설치 후에 설정할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 구성 옵션에 대해 설명합니다.  
  
 [네트워크 프로토콜 및 네트워크 라이브러리](../../sql-server/install/network-protocols-and-network-libraries.md)  
 이 문서에서는 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스의 네트워크 프로토콜 기본 구성과 사용 가능한 구성 옵션에 대해 설명합니다.  
  
 [여러 버전 및 인스턴스의 SQL Server 작업](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 여러 버전 및 인스턴스를 설치할 때 고려해야 할 사항에 대해 설명합니다.  
  
 [SQL Server의 로컬 언어 버전](../../sql-server/install/local-language-versions-in-sql-server.md)  
 이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 지역화된 버전에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 섹션  
 [SQL Server 설치](../../database-engine/install-windows/install-sql-server.md)  
 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치를 위해 필요한 여러 설치 옵션에 대한 개요를 제공합니다.  
  
 [SQL Server Business Intelligence 기능 설치](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 Microsoft BI 플랫폼의 일부인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 설치하는 방법에 대해 설명합니다.  
  
 [SQL Server 업그레이드](../../database-engine/install-windows/upgrade-sql-server.md)  
 이 섹션에서는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 인스턴스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드에 대한 개요를 제공합니다.  
  
 [SQL Server 제거](../../sql-server/install/uninstall-sql-server.md)  
 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] 의 기존 인스턴스를 완전히 제거하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 설치할 수 있도록 시스템을 준비하려면 이 섹션을 참조하십시오.  
  
 [SQL Server 장애 조치(Failover) 클러스터 설치](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 설명서 중 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터를 설치 및 구성하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [고가용성 솔루션&#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [장애 조치(Failover) 클러스터링을 설치하기 전에](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)   
 [설치 마법사를 사용하여 SQL Server 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
