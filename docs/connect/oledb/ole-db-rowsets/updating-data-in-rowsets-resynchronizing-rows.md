---
title: 행 다시 동기화 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버를 사용 하 여 행 다시 동기화
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 9cdd1b73d956650786b2456d6fc6bbecfb4837c4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>행 다시 동기화-행 집합의 데이터 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB driver for SQL Server **IRowsetResynch** 에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서 지원 행 집합에만 합니다. **IRowsetResynch** 를 필요에 따라 사용할 수 없습니다. 소비자가 행 집합을 열기 전에 이 인터페이스를 요청해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [행 집합의 데이터 업데이트](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
