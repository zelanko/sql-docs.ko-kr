---
title: SQL Server XTP IO 관리자 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: fede0215ef21ee7680068629a990ec1a9dd3417f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718958"
---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO 관리자
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
 

## <a name="see-also"></a>참고 항목  
[SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
