---
title: SQL Server, Transactions 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Transactions
- Transactions object
ms.assetid: 85240267-78fd-476a-9ef6-010d6cf32dd8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 80c62c0048f40ba945d3204c414180be9f8e0d7b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67995649"
---
# <a name="sql-server-transactions-object"></a>SQL Server, Transactions 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft **의** Transactions [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스의 활성 트랜잭션 수와 **tempdb**의 스냅샷 격리 행 버전 저장소 등의 리소스에 대해 이러한 트랜잭션이 미치는 영향을 모니터링하기 위한 카운터를 제공합니다. 트랜잭션은 논리적 작업 단위이며 데이터의 논리적 무결성을 유지하기 위해 모두 성공하거나 데이터베이스에서 지워져야 하는 작업 집합입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 있는 데이터는 모두 트랜잭션에서 수정됩니다.  
  
 스냅샷 격리 수준을 허용하도록 데이터베이스를 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스에 있는 각 행의 수정 내용에 대한 기록을 보관해야 합니다. 행을 수정할 때마다 수정되지 않은 행의 복사본이 **tempdb**의 행 버전 저장소에 기록됩니다. **Transaction** 개체의 여러 카운터는 **tempdb**에 있는 행 버전 저장소의 크기와 증가율을 모니터링하는 데 사용할 수 있습니다.  
  
 **Transactions** 개체 카운터는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스 하나의 모든 트랜잭션을 보고합니다.  
  
 이 표에서는 **SQLServer:Transactions** 카운터에 대해 설명합니다.  
  
|SQL Server Transactions 카운터|Description|  
|--------------------------------------|-----------------|  
|**Free Space in tempdb (KB)**|**tempdb**의 사용 가능한 공간(KB)입니다. 스냅샷 격리 수준 버전 저장소와 이 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에서 생성된 모든 새 임시 개체를 저장할 수 있도록 충분한 여유 공간이 있어야 합니다.|  
|**Longest Transaction Running Time**|다른 현재 트랜잭션보다 오래 활성화된 트랜잭션이 시작된 후 경과한 시간(초)입니다. 이 카운터는 데이터베이스가 읽기 커밋된 스냅샷 격리 수준 이하일 때만 작업을 보여 주고 다른 수준일 때는 작업을 기록하지 않습니다.|  
|**NonSnapshot Version Transactions**|스냅샷 격리 수준을 사용하지 않고 데이터를 수정하여 **tempdb** 버전 저장소에 행 버전을 생성한 현재 활성 트랜잭션의 수입니다.|  
|**Snapshot Transactions**|스냅샷 격리 수준을 사용하는 현재 활성 트랜잭션의 수입니다.<br /><br /> 참고: **Snapshot Transactions** 개체 카운터는 첫 번째 데이터 액세스가 발생할 때 응답하지만 `BEGIN TRANSACTION` 문이 실행될 때는 응답하지 않습니다.|  
|**트랜잭션**|모든 형식의 현재 활성 트랜잭션 수입니다.|  
|**Update conflict ratio**|마지막 1초 동안 업데이트 충돌이 발생하였고 스냅샷 격리 수준을 사용하는 트랜잭션의 비율입니다. 스냅샷 격리 수준 트랜잭션이 시작될 때 커밋되지 않은 다른 트랜잭션이 마지막으로 수정한 행을 스냅샷 격리 수준 트랜잭션에서 수정하려고 하면 업데이트 충돌이 발생합니다.|  
|**Update conflict ratio base**|내부 전용입니다.|
|**Update Snapshot Transactions**|스냅샷 격리 수준을 사용하고 수정된 데이터가 있는 현재 활성 트랜잭션의 수입니다.|  
|**Version Cleanup rate (KB/s)**|**tempdb**의 스냅샷 격리 버전 저장소에서 행 버전이 제거되는 비율(KB/초)입니다.|  
|**Version Generation rate (KB/s)**|**tempdb**의 스냅샷 격리 버전 저장소에 새로운 행 버전이 추가되는 비율(KB/초)입니다.|  
|**Version Store Size (KB)**|스냅샷 격리 수준 행 버전을 저장하는 데 사용되는 **tempdb**의 공간(KB)입니다.|  
|**Version Store unit count**|**tempdb**의 스냅샷 격리 버전 저장소에 있는 활성 할당 단위 수입니다.|  
|**Version Store unit creation**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 시작 이후 스냅샷 격리 저장소에 만들어진 할당 단위 수입니다.|  
|**Version Store unit truncation**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 시작 이후 스냅샷 격리 저장소에서 제거된 할당 단위 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
