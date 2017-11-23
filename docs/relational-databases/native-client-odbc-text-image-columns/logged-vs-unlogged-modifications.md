---
title: "로깅된 vs입니다. 수정 기록 되지 않는 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-text-image-columns
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a429671be26d53fe9354e4ab986cb10ac35d35b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="logged-vs-unlogged-modifications"></a>로깅된 vs입니다. 기록 되지 않는 수정
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  응용 프로그램 않도록 요청할 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 로그 아님 **텍스트**, **ntext**, 및 **이미지** 수정 합니다. 하지만 이 옵션을 사용할 때는 주의해야 합니다. 경우에만 사용 해야 여기서는 **텍스트**, **ntext**, 또는 **이미지** 데이터가 중요 하지 않으며 데이터 소유자는 기꺼이 포기에 대 한 데이터를 복구 하는 기능 성능 향상  
  
 로깅을 **텍스트**, **ntext**, 및 **이미지** 수정 작업을 호출 하 여 제어 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 와  *특성* 매개 변수 SQL_SOPT_SS_ TEXTPTR_LOGGING로 설정 하 고 *ValuePtr* SQL_TL_ON 또는 SQL_TL_OFF로 설정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [text 및 image 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
