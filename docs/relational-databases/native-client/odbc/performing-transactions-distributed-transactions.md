---
title: "분산된 트랜잭션 수행 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|ODBC
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
caps.latest.revision: "36"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 176f39a779bcb50ecc35c49856b1ed96f2f61173
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="performing-transactions---distributed-transactions"></a>트랜잭션 수행-분산된 트랜잭션
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하면 응용 프로그램이 둘 이상의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 트랜잭션을 확장할 수 있습니다. 또한 응용 프로그램이 Open Group DTP XA 표준을 준수하는 트랜잭션 관리자가 관리하는 트랜잭션에 참가할 수 있습니다.  
  
 일반적으로 모든 트랜잭션 관리 명령은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 통해 서버로 전달됩니다. 응용 프로그램 호출 하 여 트랜잭션을 시작 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 는 자동 커밋 모드를 해제 합니다. 그런 다음 응용 프로그램 트랜잭션과 호출을 구성 하는 업데이트 수행 [SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) SQL_COMMIT 또는 SQL_ROLLBACK 옵션을 사용 합니다.  
  
 그러나 MS DTC를 사용할 때 MS DTC가 트랜잭션 관리자 및 응용 프로그램을 더 이상 사용 **SQLEndTran**합니다.  
  
 분산 트랜잭션에 등록된 경우 두 번째 분산 트랜잭션에 등록하고 원분 분산 트랜잭션의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 결함을 새 트랜잭션에 등록합니다. 자세한 내용은 참조 [DTC 프로그래머 참조](http://msdn.microsoft.com/library/ms686108\(VS.85\).aspx)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [수행 하는 트랜잭션 &#40; ODBC &#41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
