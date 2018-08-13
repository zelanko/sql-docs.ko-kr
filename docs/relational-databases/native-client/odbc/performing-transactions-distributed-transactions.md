---
title: 분산된 트랜잭션 수행 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 588fc51619624b59aef4db1a27deff33d75f8b2a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39561423"
---
# <a name="performing-transactions---distributed-transactions"></a>트랜잭션 수행 - 분산 트랜잭션
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하면 응용 프로그램이 둘 이상의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 트랜잭션을 확장할 수 있습니다. 또한 응용 프로그램이 Open Group DTP XA 표준을 준수하는 트랜잭션 관리자가 관리하는 트랜잭션에 참가할 수 있습니다.  
  
 일반적으로 모든 트랜잭션 관리 명령은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 통해 서버로 전달됩니다. 응용 프로그램이 호출 하 여 트랜잭션을 시작 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 는 자동 커밋 모드를 해제 합니다. 트랜잭션 및 호출을 구성 하는 업데이트를 수행 하는 응용 프로그램을 다음 [SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) SQL_COMMIT 또는 SQL_ROLLBACK 옵션을 사용 하 여.  
  
 그러나 MS DTC를 사용할 때 MS DTC가 트랜잭션 관리자와 응용 프로그램을 더 이상 사용 **SQLEndTran**.  
  
 분산 트랜잭션에 등록된 경우 두 번째 분산 트랜잭션에 등록하고 원분 분산 트랜잭션의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 결함을 새 트랜잭션에 등록합니다. 자세한 내용은 [DTC 프로그래머 참조](http://msdn.microsoft.com/library/ms686108\(VS.85\).aspx).  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 수행 &#40;ODBC&#41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
