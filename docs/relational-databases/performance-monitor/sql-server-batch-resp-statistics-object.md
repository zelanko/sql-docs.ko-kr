---
title: SQL Server, Batch Resp Statistics 개체 | Microsoft 문서
description: SQL Server 일괄 처리 응답 시간을 추적하는 카운터를 제공하는 SQLServer:Batch Resp Statistics 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Batch Resp Statistics
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 155ff6d21fdb0a40e042463b809c1ed14bbe70df
ms.sourcegitcommit: a49a66dbda0cb16049e092b49c8318ac3865af3c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2020
ms.locfileid: "94983167"
---
# <a name="sql-server-batch-resp-statistics-object"></a>SQL Server, 일괄 처리 응답 통계 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
**SQLServer:Batch Resp Statistics** 성능 개체는 SQL Server 일괄 처리 응답 시간을 추적하는 카운터를 제공합니다.

다음 표에서는 SQL Server에 **Batch Resp Statistics** 성능 개체에 대해 설명합니다.


|**SQL Server Batch Resp Statistics 카운터**|Description|  
|-------------|-----------------|  
|**Batches >=000000ms & \<000001ms**|응답 시간이 0ms보다 크거나 같고 1ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000001ms & \<000002ms**|응답 시간이 1ms보다 크거나 같고 2ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000002ms & \<000005ms**|응답 시간이 2ms보다 크거나 같고 5ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000005ms & \<000010ms**|응답 시간이 5ms보다 크거나 같고 10ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000010ms & \<000020ms**|응답 시간이 10ms보다 크거나 같고 20ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000020ms & \<000050ms**|응답 시간이 20ms보다 크거나 같고 50ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000050ms & \<000100ms**|응답 시간이 50ms보다 크거나 같고 100ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000100ms & \<000200ms**|응답 시간이 100ms보다 크거나 같고 200ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000200ms & \<000500ms**|응답 시간이 200ms보다 크거나 같고 500ms보다 작은 SQL 일괄 처리 수|
|**Batches >=000500ms & \<001000ms**|응답 시간이 500ms보다 크거나 같고 1,000ms보다 작은 SQL 일괄 처리 수|
|**Batches >=001000ms & \<002000ms**|응답 시간이 1,000ms보다 크거나 같고 2,000ms보다 작은 SQL 일괄 처리 수|
|**Batches >=002000ms & \<005000ms**|응답 시간이 2,000ms보다 크거나 같고 5,000ms보다 작은 SQL 일괄 처리 수|
|**Batches >=005000ms & \<010000ms**|응답 시간이 5,000ms보다 크거나 같고 10,000ms보다 작은 SQL 일괄 처리 수|
|**Batches >=010000ms & \<020000ms**|응답 시간이 10,000ms보다 크거나 같고 20,000ms보다 작은 SQL 일괄 처리 수|
|**Batches >=020000ms & \<050000ms**|응답 시간이 20,000ms보다 크거나 같고 50,000ms보다 작은 SQL 일괄 처리 수|
|**Batches >=050000ms & \<100000ms**|응답 시간이 50,000ms보다 크거나 같고 100,000ms보다 작은 SQL 일괄 처리 수| 
|**Batches >=100000ms**|응답 시간이 100,000ms보다 크거나 같은 SQL 일괄 처리 수| 

개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|항목|Description|  
|----------|-----------------|  
|**CPU Time:Requests**|CPU 시간을 기준으로 한 요청 수입니다.|  
|**CPU Time:Total(ms)**|일괄 처리에 소요되는 CPU 총 시간입니다.|  
|**Elapsed Time:Requests**|경과된 시간을 기준으로 한 요청 수입니다.|  
|**Elapsed Time:Total(ms)**|일괄 처리의 경과 시간입니다.|  

## <a name="see-also"></a>참고 항목
[SQL Server, Plan Cache 개체](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[리소스 사용 모니터링(시스템 모니터)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
