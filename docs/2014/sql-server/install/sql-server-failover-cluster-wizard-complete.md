---
title: SQL Server 장애 조치 클러스터 마법사-완료 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 820f35b7-a3cd-46c9-9963-811633d0711a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 436882e02c2a752052536ae29619fb0990989175
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091994"
---
# <a name="sql-server-failover-cluster-wizard---complete"></a>SQL Server 장애 조치(Failover) 클러스터 마법사 - 완료
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 설치 작업이 완료되기 전에 컴퓨터 구성의 유효성을 검사합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 SCC(시스템 구성 검사기)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치할 컴퓨터를 검색합니다. SCC는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성공적인 설치 작업을 방해하는 조건이 있는지 확인합니다. 설치 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 시작하기 전에 SCC는 각 항목의 상태를 검색합니다. 그런 다음 검색 결과를 필수 조건과 비교하고 차단 문제 해결을 위한 지침을 제공합니다.  
  
 시스템 구성 검사에서는 각 실행 규칙에 대한 간단한 설명과 실행 상태를 포함하는 보고서를 생성합니다. 시스템 구성 검사 보고서는 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\합니다.  
  
 설치 작업을 실행하기 전에 다음 항목을 검토하십시오.  
  
1.  [SQL Server 2014 설치를 위한 하드웨어 및 소프트웨어 요구 사항](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [SQL Server 2014 버전에서 지원하는 기능](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [SQL Server 설치에 대한 보안 고려 사항](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [SQL Server의 로컬 언어 버전](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 기타 참조:  
  
1.  [지원되는 버전 및 에디션 업그레이드](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [장애 조치(Failover) 클러스터링을 설치하기 전에](../failover-clusters/install/before-installing-failover-clustering.md)  
  
## <a name="see-also"></a>관련 항목  
 [설치 규칙](../../../2014/sql-server/install/install-rules.md)  
  
  
