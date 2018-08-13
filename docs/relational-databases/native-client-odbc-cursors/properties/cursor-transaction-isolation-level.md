---
title: 커서 트랜잭션 격리 수준 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fa5d5e4ab98c49d80ef8daa0f1dfaa6bd37c3080
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536153"
---
# <a name="cursor-transaction-isolation-level"></a>커서 트랜잭션 격리 수준
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  커서의 전체 잠금 동작은 클라이언트에서 설정하는 동시성 특성과 트랜잭션 격리 수준 사이의 상호 작용을 기반으로 합니다. ODBC 클라이언트는 트랜잭션 격리 수준 사용 하 여 설정 합니다 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION 또는 SQL_COPT_SS_TXN_ISOLATION 특성입니다. 특정 커서 환경의 잠금 동작은 동시성 및 트랜잭션 격리 수준 옵션의 잠금 동작을 통해 결정됩니다.  
  
 다음과 같은 커서 트랜잭션 격리 수준에서 지원 되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버.  
  
-   커밋된 읽기(SQL_TXN_READ_COMMITTED)  
  
-   커밋되지 않은 읽기(SQL_TXN_READ_UNCOMMITTED)  
  
-   반복 읽기(SQL_TXN_REPEATABLE_READ)  
  
-   직렬화 가능(SQL_TXN_SERIALIZABLE)  
  
-   스냅숏(SQL_TXN_SS_SNAPSHOT)  
  
 ODBC API 추가 트랜잭션 격리 수준을 지정 하지만에서 지원 되지 않습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버.  
  
## <a name="see-also"></a>관련 항목  
 [커서 속성](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
