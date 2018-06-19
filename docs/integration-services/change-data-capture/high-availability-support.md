---
title: 고가용성 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2e0f6d3f-0536-46d9-8630-835e199515bf
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae0ee26dfd95ef6f425b749e24b6e5d506ece235
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35335567"
---
# <a name="high-availability-support"></a>고가용성 지원
  Oracle CDC Service는 고가용성을 위해 디자인되었습니다. 다음 기능은 일부 고가용성 지원을 제공합니다.  
  
-   Oracle CDC Service는 파일 리소스(로컬 또는 기타 방식)를 사용하지 않습니다. 전체 상태는 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 저장됩니다. 그러면 서비스가 실행되는 컴퓨터에 장애가 발생할 경우 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용하는 다른 컴퓨터에서 서비스를 쉽게 시작할 수 있습니다. 복구 시간을 줄이기 위해 긴 또는 장기 실행되는 Oracle 트랜잭션은 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 준비 테이블에 유지되므로 장애(또는 서비스 다시 시작) 후에 많은 트랜잭션 로그를 다시 검색할 필요가 없습니다.  
  
-   Oracle CDC Service는 클러스터형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용할 수 있으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 다른 클러스터 노드로 장애 조치된 후 복구할 수 있습니다. Oracle CDC Service 컴퓨터 관리자가 Oracle CDC Service를 만들 때 연결 정보를 클러스터형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 지정하면 됩니다.  
  
-   Oracle CDC Service는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**Always On** 데이터베이스 미러링 기능을 사용할 수 있습니다. 이 기능을 지원하려면 MSXDBCDC 및 모든 CDC 데이터베이스가 동일한 가용성 그룹에 있어야 합니다. 또한 Oracle CDC Service 컴퓨터 관리자가 해당 **Always On** 연결 정보를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가용성 그룹에 지정해야 합니다(예: 연결 속성 `Failover_Partner and Network=dbmssocn`). 그러면 CDC Service는 장애 조치(failover) 후 데이터베이스의 보조 복제에서 처리를 자동으로 재개할 수 있습니다.  
  
-   Windows 장애 조치(failover) 클러스터에서( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 또는 따로) Oracle CDC Service를 구성할 수 있으므로 간단하게 장애 조치를 수행하고 CDC 처리를 클러스터로 대체할 수 있습니다. 장애 조치(failover) 클러스터에서 Oracle CDC Service를 리소스로 구성하려면 시스템 관리자가 장애 조치(failover) 클러스터의 각 노드에서 Oracle CDC Service를 일반 서비스 리소스로 설정해야 합니다.  
  
-   Oracle CDC Service는 Oracle RAC 노드 중 하나가 중지되는 경우에도 Oracle 데이터베이스와 통신하여 로그를 처리할 수 있는 Oracle RAC를 지원합니다.  
  
  
