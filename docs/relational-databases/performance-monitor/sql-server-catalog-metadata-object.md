---
title: SQL Server, Catalog Metadata 개체 | Microsoft 문서
description: SQL Server용 카탈로그 메타데이터에 대한 카운터를 제공하는 SQLServer:Catalog Metadata 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 54beed996f87ad279ed097efe8e4a8ca9558634e
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458655"
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, 카탈로그 메타데이터 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
**SQLServer:Catalog Metadata** 성능 개체는 SQL Server용 카탈로그 메타데이터에 대한 카운터를 제공합니다.

다음 표에서는 SQL Server **Catalog Metadata** 성능 개체에 대해 설명합니다.


|**SQL Server 카탈로그 메타데이터 카운터**|Description|  
|-------------|-----------------|  
|**Cache Entries Count**|카탈로그 메타데이터 캐시의 항목 수입니다.|
|**Cache Entries Pinned Count**|고정된 카탈로그 메타데이터 캐시 항목의 수입니다.|
|**Cache Hit Ratio**|카탈로그 메타데이터 캐시 적중 횟수와 조회 간 비율입니다.|
|**Cache Hit Ratio**|내부 전용입니다.|

데이터베이스별로 카운터 인스턴스는 한 개입니다.

## <a name="see-also"></a>참고 항목  
[리소스 사용 모니터링(시스템 모니터)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
