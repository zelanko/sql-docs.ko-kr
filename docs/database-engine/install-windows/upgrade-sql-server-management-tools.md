---
title: SQL Server 관리 도구 업그레이드 | Microsoft Docs
description: 이 문서에서는 SQL Server 관리 도구 및 SQL Server 에이전트와 같은 관리 구성 요소의 업그레이드와 관련된 지원에 대해 설명합니다.
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- management tools, upgrading
ms.assetid: 1dab50b9-d16c-49a1-9ecc-af72adb6c378
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2c10d77a72ef23616feb2ac59db44589966fe49a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900238"
---
# <a name="upgrade-sql-server-management-tools"></a>SQL Server 관리 도구 업그레이드

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상에서의 업그레이드가 지원됩니다. 이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구 및 관리 구성 요소(예: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트, 데이터베이스 메일, 유지 관리 계획, XPStar 및 XPWeb) 업그레이드를 위한 지원 및 동작에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  로컬로 설치하는 경우 관리자로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용하십시오.  
  
## <a name="known-upgrade-issues"></a>알려진 업그레이드 문제  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하기 전에 다음 사항을 고려하십시오.  
  
### <a name="for-all-upgrade-scenarios"></a>모든 업그레이드 시나리오  
  
- MSX 서버를 업그레이드하기 전에 모든 TSX 서버를 업그레이드해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 MSX/TSX에 대한 자세한 내용은 [기업 내 관리 자동화](../../ssms/agent/automated-administration-across-an-enterprise.md)를 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 구성 요소를 동시에 업그레이드해야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 버전 번호는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인스턴스에서 동일해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 업그레이드할 때 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 기존 설치에 구성 요소를 추가할 수 있습니다. 자세한 내용은 [설치 마법사를 사용하여 SQL Server 2016 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)를 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 도구(예: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자, sqlcmd, osql)는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드되지 않습니다. 대신 클라이언트 도구는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도구와 함께 실행됩니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 이전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 클라이언트 도구의 설정을 가져올 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로의 인증이 업그레이드 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에서 Windows 인증으로 업데이트됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되지 않습니다.  
  
-   작업 및 경고 데이터는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로의 업그레이드에서 유지됩니다.  
  
-   업그레이드할 인스턴스에서 SQLMail을 사용 중인 경우에는 업그레이드 후에도 이와 연결된 XP가 지원 및 사용됩니다. 그렇지 않은 경우 SQLMail은 해제됩니다.  
  
-   SQLiMail이라고도 하는 데이터베이스 메일은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]구성 요소와 함께 업그레이드됩니다. 기본적으로 데이터베이스 메일은 업그레이드 후에 해제됩니다. 모든 스키마 업데이트는 업그레이드 후에 업데이트 스크립트로 조정해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [이전 버전과의 호환성_삭제됨](https://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)   
 [설치 마법사를 사용하여 SQL Server 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
