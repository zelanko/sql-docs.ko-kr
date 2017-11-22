---
title: "SQL Server XTP IO 관리자 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
caps.latest.revision: "2"
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 530500f1dafa732f008f3d08de0caaad43ce1021
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO 관리자
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server XTP IO 관리자 성능 개체에는 메모리 내 OLTP IO 속도 관리자와 관련된 카운터가 포함되어 있습니다.

이 표에서는 **SQL Server XTP IO 관리자** 카운터에 대해 설명합니다.

|카운터|Description|  
|-------------|-----------------|  
|**Insufficient Credits Waits/sec**|속도 개체에서 크레딧 부족으로 인한 대기하는 초당 크레딧 수입니다.|
|**Io Issued/sec**|플러시 스레드에 의해 실행되는 초당 Io 횟수입니다.|
|**Log Blocks/sec**|컨트롤러에서 처리하는 초당 로그 블록 수입니다.|
|**Missed Credit Slots**|속도 개체에서 크레딧 대기로 인해 누락된 크레딧 슬롯 수입니다.|
|**Stale Rate Object Waits/sec**|오래된 속도 개체로 인한 초당 대기 수입니다.|
|**Total Rate Objects Published**|게시된 총 속도 개체 수입니다.|
 

## <a name="see-also"></a>관련 항목:  
[SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
