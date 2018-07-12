---
title: 구독 초기화 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
caps.latest.revision: 31
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7e21b5bb08e860f07d6d5fb99c91138584787d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37240583"
---
# <a name="initialize-a-subscription"></a>구독 초기화
  복제 토폴로지의 구독자는 구독한 게시에 있는 각 아티클의 스키마 복사본과 저장 프로시저, 트리거 및 메타데이터 테이블과 같이 필요한 모든 복제 개체를 포함하도록 초기화되어야 합니다. 일반적으로 구독자를 초기화하면 초기 데이터 집합도 구독자로 전달됩니다. 기본 초기화 메서드는 스키마, 복제 개체 및 데이터를 포함하는 전체 스냅숏을 사용하지만 전체 스냅숏 없이도 게시를 초기화할 수 있습니다.  
  
 자세한 내용은 [Initialize a Subscription with a Snapshot](initialize-a-subscription-with-a-snapshot.md) 및 [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md)를 참조하세요.  
  
  
