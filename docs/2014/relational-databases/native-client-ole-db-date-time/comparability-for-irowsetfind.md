---
title: IRowsetFind 비교 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability [ODBC]
ms.assetid: 7d148b56-9bbe-4e55-b31f-43f115705402
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9aa8cb118a84bca1d37bdd409055b21d1d11552
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63233026"
---
# <a name="comparability-for-irowsetfind"></a>IRowsetFind 비교
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
 [날짜 및 시간 기능 향상&#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
