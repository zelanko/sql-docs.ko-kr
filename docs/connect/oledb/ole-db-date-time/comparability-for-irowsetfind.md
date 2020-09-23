---
title: IRowsetFind 비교 | Microsoft Docs
description: OLE DB Driver for SQL Server에서 IRowsetFind가 날짜/시간 형식에 대해 지원하는 비교에 대해 알아봅니다. 다른 비교를 위해 DB_E_BADCOMPAREOP가 반환됩니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16ef589a18c2be5317157e7db5790af06c8c613a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861400"
---
# <a name="comparability-for-irowsetfind"></a>IRowsetFind 비교
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  IRowsetFind는 날짜/시간 형식에 대해서만 다음과 같은 비교를 지원합니다.  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 다른 비교를 시도하면 DB_E_BADCOMPAREOP가 반환됩니다. 이것은 OLE DB 사양에 따른 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
