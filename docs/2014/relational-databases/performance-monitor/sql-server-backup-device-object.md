---
title: SQL Server, Backup Device 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 80f6fbec56a086ad150620dac1179da9018370b2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63250746"
---
# <a name="sql-server-backup-device-object"></a>SQL Server, Backup Device 개체
  **Backup Device** 개체는 백업 및 복원 작업에 사용되는 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 디바이스를 모니터링하는 카운터를 제공합니다. 디바이스 단위로 백업 및 복원 작업의 처리량, 진행률, 성능 등을 결정하려면 백업 디바이스를 모니터링합니다. 전체 데이터베이스 백업이나 복원 작업의 처리량을 모니터링하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **데이터베이스** 개체의 **Backup/Restore Throughput/sec** 카운터를 사용합니다. 자세한 내용은 [SQL Server, Databases Object](sql-server-databases-object.md)을 참조하세요.  
  
 이 테이블에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** 카운터에 대해 설명합니다.  
  
|SQL Server Backup Device 카운터|Description|  
|---------------------------------------|-----------------|  
|**Device Throughput Bytes/sec**|데이터베이스를 백업하거나 복원하는 데 사용되는 백업 디바이스의 읽기/쓰기 작업 처리량(초당 바이트 수)입니다. 이 카운터는 백업이나 복원 작업이 실행 중일 때만 존재합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [백업 디바이스&#40;SQL Server&#41;](../backup-restore/backup-devices-sql-server.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
