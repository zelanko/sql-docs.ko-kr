---
title: 도메인 컨트롤러에서 SQL Server 2008로 업그레이드 하기 위한 계정 요구 사항 서비스 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- domain controllers
- service accounts
- network service accounts
- local service accounts
ms.assetid: 574245b6-11e2-4849-b0ca-836d673ecd0d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dc00c4195b54101c24bc05218e4ea7c3abac53e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659883"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>도메인 컨트롤러에서 SQL Server 2008로 업그레이드하기 위한 서비스 계정 요구 사항
  업그레이드 관리자의 인스턴스를 발견 했습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 로컬 서비스나 네트워크 서비스 계정으로 실행 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 도메인 컨트롤러입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도메인 컨트롤러에 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]가 설치되어 있으면 로컬 서비스 계정 또는 네트워크 서비스 계정 권한으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 실행할 수 없습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>수정 동작  
 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 도메인 계정이나 로컬 시스템 계정에 할당합니다. 업그레이드하기 전에 이러한 변경 작업을 수행하지 못하면 설치가 차단됩니다. 서비스 계정 SQL 기록기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Active Directory Helper Service는 네트워크 서비스 계정으로 하드 코딩되어 변경할 수 없으므로 예외입니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
