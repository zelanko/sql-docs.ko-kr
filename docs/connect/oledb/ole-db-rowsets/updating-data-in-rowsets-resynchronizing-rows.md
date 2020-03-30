---
title: 행 다시 동기화 | Microsoft Docs
description: OLE DB Driver for SQL Server를 사용하여 행 다시 동기화
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2f1ea1a563e986914c5fe820740776da129c3b28
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994166"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>행 집합의 데이터 업데이트 - 행 다시 동기화
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 **커서 지원 행 집합에서만**IRowsetResynch[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 지원합니다. **IRowsetResynch**는 요청 시 사용할 수 없으며 소비자가 행 집합을 열기 전에 이 인터페이스를 요청해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합의 데이터 업데이트](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
