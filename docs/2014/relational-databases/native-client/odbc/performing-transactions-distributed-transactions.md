---
title: 분산된 트랜잭션 수행 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa5c6b607fa7523380950ecd89f9cae20ffc6f21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228957"
---
# <a name="performing-distributed-transactions"></a>분산 트랜잭션 수행
  MS DTC(Microsoft Distributed Transaction Coordinator)를 사용하면 응용 프로그램이 둘 이상의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 트랜잭션을 확장할 수 있습니다. 또한 응용 프로그램이 Open Group DTP XA 표준을 준수하는 트랜잭션 관리자가 관리하는 트랜잭션에 참가할 수 있습니다.  
  
 일반적으로 모든 트랜잭션 관리 명령은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 통해 서버로 전달됩니다. 응용 프로그램이 호출 하 여 트랜잭션을 시작 [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) 는 자동 커밋 모드를 해제 합니다. 그런 다음 응용 프로그램은 트랜잭션을 호출 구성 업데이트를 수행 [SQLEndTran](../../native-client-odbc-api/sqlendtran.md) SQL_COMMIT 또는 SQL_ROLLBACK 옵션을 사용 하 여 합니다.  
  
 그러나 MS DTC를 사용할 때 MS DTC가 트랜잭션 관리자와 응용 프로그램을 더 이상 사용 **SQLEndTran**.  
  
 분산 트랜잭션에 등록된 경우 두 번째 분산 트랜잭션에 등록하고 원분 분산 트랜잭션의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 결함을 새 트랜잭션에 등록합니다. 자세한 내용은 [DTC 프로그래머 참조](https://msdn.microsoft.com/library/ms686108\(VS.85\).aspx).  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 수행 &#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
