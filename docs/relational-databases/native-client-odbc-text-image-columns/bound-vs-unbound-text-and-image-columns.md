---
title: Vs 바인딩됩니다. Text 및 Image 열에 바인딩되지 않은 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-text-image-columns
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b8677ba4369063f5364410799c3ca4f7bb75f267
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Vs 바인딩됩니다. 바인딩되지 않은 Text 및 Image 열
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  서버 커서를 사용 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 바인딩되지 않은 대 한 데이터를 전송 하지 않도록 최적화 되어 **텍스트**, **ntext**, 또는 **이미지** 당시 열 **SQLFetch** 수행 됩니다. **텍스트**, **ntext**, 또는 **이미지** 데이터 실제로에서 검색 되지 않는 서버 응용 프로그램 문제까지 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 열에 대 한 합니다.  
  
 대부분의 응용 프로그램을 작성할 수 있습니다 있도록 없는 **텍스트**, **ntext**, 또는 **이미지** 사용자가 커서에서 위와 아래로 스크롤 하는 동안 데이터가 표시 됩니다. 응용 프로그램이 호출할 수는 사용자가 자세한 내용을 보려면 행을 선택 하면 **SQLGetData** 검색 하는 **텍스트**, **ntext**, 또는 **이미지** 데이터입니다. 이 전송 하지 것입니다는 **텍스트**, **ntext**, 또는 **이미지** 사용자를 선택 하지 않으며 따라서 수 행에 대 한 데이터 매우 많은 양의 데이터 전송을 방지 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Text 및 Image 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [커서 동작](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
