---
title: XTP (메모리 내 OLTP) 성능 카운터 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69b24c96e4833a45038bfcae20f0a5fecd0d2340
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151131"
---
# <a name="xtp-in-memory-oltp-performance-counters"></a>XTP(메모리 내 OLTP) 성능 카운터
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 메모리 내 OLTP 작업을 모니터링하기 위해 성능 모니터에서 사용할 수 있는 개체 및 카운터를 제공합니다.  
  
##  <a name="SQLServerPOs"></a> XTP (메모리 내 OLTP) 성능 개체  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체에 대해 설명합니다.  
  
|성능 개체|Description|  
|------------------------|-----------------|  
|[XTP 커서](../cursors.md)|XTP 커서 성능 개체에는 내부 XTP 엔진 커서와 관련된 카운터가 포함됩니다. 커서는 XTP 엔진이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 처리하기 위해 사용하는 하위 수준의 기본 구성 요소입니다. 따라서 사용자는 일반적으로 이를 직접 제어하지 않습니다.|  
|[XTP 가비지 수집](sql-server-xtp-garbage-collection.md)|XTP 가비지 수집 성능 개체에는 XTP 엔진의 가비지 수집기와 관련된 카운터가 포함됩니다.|  
|[XTP 가상 프로세서](sql-server-xtp-phantom-processor.md)|XTP 가상 프로세서 성능 개체에는 XTP 엔진의 가상 처리 하위 시스템과 관련된 카운터가 포함됩니다. 이 구성 요소는 SERIALIZABLE 격리 수준에서 실행되는 트랜잭션에서 가상 행을 검색합니다.|  
|[XTP 저장소](sql-server-xtp-storage.md)|XTP 스토리지 성능 개체에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 XTP 스토리지와 관련된 카운터가 포함되어 있습니다.|  
|[XTP 트랜잭션 로그](sql-server-xtp-transaction-log.md)|XTP 트랜잭션 로그 성능 개체에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 XTP 트랜잭션 로깅과 관련된 카운터가 포함됩니다.|  
|[XTP 트랜잭션](sql-server-xtp-transactions.md)|XTP 트랜잭션 성능 개체에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 XTP 엔진 트랜잭션과 관련된 카운터가 포함됩니다.|  
  
  
