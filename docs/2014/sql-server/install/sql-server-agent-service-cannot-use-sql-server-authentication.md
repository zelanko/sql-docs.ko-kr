---
title: SQL Server 에이전트 서비스에서 SQL Server 인증을 사용할 수 없습니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- authentication [SQL Server Agent]
- SQL Server Authentication [SQL Server Agent]
ms.assetid: c39f3ec3-fc2c-4c12-940f-60d8d3d17660
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e16882247a123b32ba07fbbae0d1f3573fd2d678
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092073"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>SQL Server 에이전트 서비스는 SQL Server 인증을 사용할 수 없습니다.
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 연결될 때 Windows 인증만 지원됩니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트  
  
## <a name="description"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 Windows 인증을 사용해서만 데이터베이스에 로그온할 수 있습니다. 즉, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자여야 합니다.  
  
 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "자동 관리를 위한 보안" 및 " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 보안 구현"을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 에이전트 업그레이드 문제](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
