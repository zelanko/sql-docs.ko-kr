---
title: 작업 범주를 전달 하는 SQL Server 에이전트 로그에는 업그레이드가 실패 하면 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7145d846657613b50706ebe75c9832f40f49383e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092036"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>SQL Server 에이전트 로그 전달 작업 범주로 인해 업그레이드하지 못합니다.
  로그 전달이라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 범주가 있으면 업그레이드 프로세스가 실패합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트  
  
## <a name="description"></a>Description  
 로그 전달이라는 시스템 작업 범주가 있습니다. 업그레이드하려는 설치에 로그 전달이라는 사용자가 만든 작업 범주가 이미 있으면 업그레이드하기 전에 이 작업 범주의 이름을 바꿔야 합니다. 그렇지 않으면 업그레이드 프로세스가 실패합니다.  
  
## <a name="see-also"></a>관련 항목  
 [로그 전달 업그레이드 한 후 실행 되지 않습니다.](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [SQL Server 에이전트 사용자 프록시 계정이 임시 UpgradedProxyAccount로 변경 됩니다 업그레이드](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [SQL Server 에이전트 업그레이드 문제](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
