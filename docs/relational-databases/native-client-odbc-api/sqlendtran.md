---
title: SQLEndTran | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 68a3d0f6df87f316e3bf2055365aa09493135b97
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlendtran"></a>SQLEndTran
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 **SQLEndTran** 가 작업을 커밋하거나 롤백할 때 문과 연결된 커서를 닫습니다. 서버 커서는 정적 상태가 될 때까지 닫힙니다. **SQLEndTran** 가 작업을 커밋하거나 롤백할 때 문과 연결된 커서의 동작은 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)을 통해 설정된, 드라이버 관련 ODBC 연결 특성인 SQL_COPT_SS_PRESERVE_CURSORS의 값에 의해 결정됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SQLEndTran 함수](http://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
