---
title: SQL Server 에이전트 사용자 프록시 계정이 임시 UpgradedProxyAccount에 변경 됩니다 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log shipping [SQL Server Agent]
ms.assetid: cd2d08c3-4e56-4034-8b68-0c78df8b5471
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9bae867b97a9fc63b97506fd8900e68b670b8013
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079669"
---
# <a name="upgrading-will-change-the-sql-server-agent-user-proxy-account-to-the-temporary-upgradedproxyaccount"></a>업그레이드하면 SQL Server 에이전트 사용자 프록시 계정이 임시 UpgradedProxyAccount로 변경됩니다.
  로그 전달을 사용하도록 설정된 데이터베이스 유지 관리 계획이 업그레이드 후에 활성화되지 않습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 데이터베이스 유지 관리 계획과 직접 호환되지 않는 새로운 로그 전달 함수 집합을 제공합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 로그 전달 함수가 포함된 데이터베이스 유지 관리 계획을 가진 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 사용자는 새 함수를 사용하여 로그 전달을 구성해야 합니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "로그 전달"을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 로그 전달 작업 범주로 인해 업그레이드 하지 못합니다.](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [로그 전달 업그레이드 한 후 실행 되지 않습니다.](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)  
  
  