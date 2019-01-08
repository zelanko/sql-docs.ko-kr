---
title: SQL Server, Locks 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Locks object
- SQLServer:Locks
ms.assetid: ace04f0d-3993-4444-8317-ca39d7087e49
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cd7773177f6ec9d02df9d3d669abf561919ffe0b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748405"
---
# <a name="sql-server-locks-object"></a>SQL Server, Locks 개체
  Microsoft **의** SQLServer:Locks [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체는 개별 리소스 유형에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 잠금 정보를 제공합니다. 트랜잭션 동안 읽거나 수정한 행과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스에는 잠금이 설정되어 다른 트랜잭션에서 동시에 리소스를 사용하는 것을 방지합니다. 예를 들어 트랜잭션에 의해 테이블에 있는 행에 배타적(X) 잠금이 설정되어 있다면 잠금을 풀기 전까지는 다른 트랜잭션으로 수정할 수 없습니다. 잠금을 최소화하면 동시성을 늘려 성능을 향상시킬 수 있습니다. **Locks** 개체의 여러 인스턴스는 리소스 유형의 잠금을 나타내는 각 인스턴스와 함께 동시 모니터링이 가능합니다.  
  
 이 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** 카운터를 설명합니다.  
  
|SQL Server Locks 카운터|Description|  
|-------------------------------|-----------------|  
|**Average Wait Time(ms)**|대기한 각 잠금 요청에 대한 평균 대기 시간(밀리초)입니다.|  
|**Lock Requests/sec**|잠금 관리자에서 요청한 초당 새 잠금 및 잠금 변환 수입니다.|  
|**Lock Timeouts (timeout > 0)/sec**|시간 초과된 초당 잠금 요청 수입니다. 단, 여기에는 NOWAIT 잠금에 대한 요청이 제외됩니다.|  
|**Lock Timeouts/sec**|시간 초과된 초당 잠금 요청 수입니다. 여기에는 NOWAIT 잠금에 대한 요청이 포함됩니다.|  
|**Lock Wait Time(ms)**|마지막 1초 동안의 잠금에 대한 총 대기 시간(밀리초)입니다.|  
|**Lock Waits/sec**|호출자가 기다려야 하는 초당 잠금 요청 수입니다.|  
|**Number of Deadlocks/sec**|교착 상태를 일으킨 초당 잠금 요청 수입니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 잠글 수 있는 리소스는 다음과 같습니다.  
  
|항목|Description|  
|----------|-----------------|  
|**_Total**|모든 잠금 정보입니다.|  
|**AllocUnit**|할당 단위에 대한 잠금입니다.|  
|**응용 프로그램**|애플리케이션이 지정한 리소스에 대한 잠금입니다.|  
|**데이터베이스 백업**|데이터베이스의 모든 개체를 포함한 데이터베이스에 대한 잠금입니다.|  
|**Extent**|연결된 8페이지 그룹에 대한 잠금입니다.|  
|**최근에 사용한 파일**|데이터베이스 파일에 대한 잠금입니다.|  
|**Heap/BTree**|힙 또는 BTree(HOBT)입니다. 데이터 페이지의 힙 또는 인덱스의 BTree 구조에 대한 잠금입니다.|  
|**Key**|인덱스의 행에 대한 잠금입니다.|  
|**메타데이터**|메타데이터라고도 하는 카탈로그 정보에 대한 잠금입니다.|  
|**개체**|모든 데이터 및 인덱스를 포함한 테이블, 저장 프로시저, 뷰 등에 대한 잠금입니다. **sys.all_objects**에 항목이 있는 모든 개체가 해당됩니다.|  
|**호출**|데이터베이스의 8KB 페이지에 대한 잠금입니다.|  
|**RID**|행 ID를 의미하며 힙의 단일 행에 대한 잠금입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
