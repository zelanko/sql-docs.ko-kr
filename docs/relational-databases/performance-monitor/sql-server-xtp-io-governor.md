---
title: SQL Server XTP IO 관리자 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c5c66968245ff2944d1d16e73ed766b7e09ef122
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158541"
---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO 관리자
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server XTP IO 관리자 성능 개체에는 메모리 내 OLTP IO 속도 관리자와 관련된 카운터가 포함되어 있습니다.

이 표에서는 **SQL Server XTP IO 관리자** 카운터에 대해 설명합니다.

|카운터|설명|  
|-------------|-----------------|  
|**Insufficient Credits Waits/sec**|속도 개체에서 크레딧 부족으로 인한 대기하는 초당 크레딧 수입니다.|
|**Io Issued/sec**|플러시 스레드에 의해 실행되는 초당 Io 횟수입니다.|
|**Log Blocks/sec**|컨트롤러에서 처리하는 초당 로그 블록 수입니다.|
|**Missed Credit Slots**|속도 개체에서 크레딧 대기로 인해 누락된 크레딧 슬롯 수입니다.|
|**Stale Rate Object Waits/sec**|오래된 속도 개체로 인한 초당 대기 수입니다.|
|**Total Rate Objects Published**|게시된 총 속도 개체 수입니다.|
 

## <a name="see-also"></a>참고 항목  
[SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
