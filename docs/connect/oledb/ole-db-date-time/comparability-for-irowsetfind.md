---
title: Irowsetfind 비교 | Microsoft Docs
description: IRowsetFind 비교
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63f7625014822e063eb4ca8b91dd3411fc7d788c
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="comparability-for-irowsetfind"></a>IRowsetFind 비교
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  IRowsetFind는 날짜/시간 형식에 대해서만 다음과 같은 비교를 지원합니다.  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 다른 비교를 시도하면 DB_E_BADCOMPAREOP가 반환됩니다. 이것은 OLE DB 사양에 따른 것입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [날짜 및 시간 기능 향상 &#40; OLE db&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
