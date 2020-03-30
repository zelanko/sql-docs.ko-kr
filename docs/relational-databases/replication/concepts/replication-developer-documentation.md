---
title: 복제 개발자 설명서 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
helpviewer_keywords:
- developer's guide [SQL Server replication]
- programming [SQL Server replication]
- replication [SQL Server], development
ms.assetid: 7ee134ae-1cab-4a35-8017-8ac6d8fc64b6
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: aa10d72d9b634ad2e7270566a6e6f43da26b4040
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287890"
---
# <a name="replication-developer-documentation"></a>복제 개발자 설명서
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  복제 토폴로지를 프로그래밍 방식으로 구성, 유지 관리 및 모니터링하면 반복되는 복제 태스크를 간소화하고 복제 기반 애플리케이션의 사용자 환경을 향상시킬 수 있습니다. 복제를 프로그래밍하면 최종 사용자가 복제 저장 프로시저와 복제 에이전트 실행 파일에 대해 잘 알지 못하거나 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 구현된 복제 사용자 인터페이스를 사용하지 않아도 사용자 지정 복제 기능을 사용할 수 있습니다.  
  
 다음과 같은 시나리오에서는 애플리케이션에서 복제 서비스에 대한 프로그래밍 방식 액세스의 장점을 활용할 수 있습니다.  
  
-   사용자가 단추를 클릭했을 때 끌어오기 구독을 동기화하는 것과 같은 복제 기능을 기존 최종 사용자 애플리케이션에 추가하는 경우  
  
-   복제를 원격으로 관리하기 위한 웹 기반 사용자 인터페이스를 만드는 경우  
  
-   관리 기능의 일부만 제공하거나, 한 곳에서 여러 복제 토폴로지를 원격으로 관리하거나, 관리 및 동기화 기능을 결합하는 사용자 지정 인터페이스를 만드는 경우  
  
-   게시, 구독 또는 배포자에 대한 상태 모니터링 기능을 추가하여 기존의 모니터링 도구를 향상시키는 경우  
  
-   Oracle 게시자에 대해 구독을 동기화하거나 관리하는 사용자 지정 애플리케이션을 만드는 경우  
  
-   병합 구독이 동기화될 때 실행되는 사용자 지정 비즈니스 규칙을 작성하는 경우  
  
-   새 구독자를 구성할 때 반복 실행될 수 있는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 스크립트를 생성하는 경우  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 복제 에이전트를 프로그래밍 방식으로 제어하고 복제 토폴로지를 프로그래밍 방식으로 관리 및 모니터링할 수 있습니다. 복제 프로그래밍에 대한 자세한 내용은 [복제 프로그래밍 개념](../../../relational-databases/replication/concepts/replication-programming-concepts.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [복제 프로그래밍 개념](../../../relational-databases/replication/concepts/replication-programming-concepts.md)  
 복제를 사용하는 애플리케이션을 개발하기 위한 계획 단계에 대해 설명합니다.  
  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
 시스템 저장 프로시저를 사용하여 복제 토폴로지에서 프로그래밍 방식 액세스를 제공하는 방법에 대해 설명합니다.  
  
 [복제 관리 개체 개념](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
 RMO(복제 관리 개체) 사용과 관련된 개념에 대해 설명합니다. RMO는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 복제 기능을 캡슐화하는 관리 코드 어셈블리입니다.  
  
 [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
 복제 에이전트 실행 파일 사용 방법에 대해 설명합니다.  
  
  
  
