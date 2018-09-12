---
title: SQL Server, Backup Device 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d24d22fe3a2790f9dce20902b34cd192e572c3bd
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811639"
---
# <a name="sql-server-backup-device-object"></a>SQL Server, Backup Device 개체
  **Backup Device** 개체는 백업 및 복원 작업에 사용되는 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 장치를 모니터링하는 카운터를 제공합니다. 장치 단위로 백업 및 복원 작업의 처리량, 진행률, 성능 등을 결정하려면 백업 장치를 모니터링합니다. 전체 데이터베이스 백업이나 복원 작업의 처리량을 모니터링하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Databases** 개체의 **Backup/Restore Throughput/sec** 카운터를 사용합니다. 자세한 내용은 [SQL Server, Databases Object](sql-server-databases-object.md)을 참조하세요.  
  
 이 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** 카운터에 대해 설명합니다.  
  
|SQL Server Backup Device 카운터|Description|  
|---------------------------------------|-----------------|  
|**Device Throughput Bytes/sec**|데이터베이스를 백업하거나 복원하는 데 사용되는 백업 장치의 읽기/쓰기 작업 처리량(초당 바이트 수)입니다. 이 카운터는 백업이나 복원 작업이 실행 중일 때만 존재합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [백업 장치&#40;SQL Server&#41;](../backup-restore/backup-devices-sql-server.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
