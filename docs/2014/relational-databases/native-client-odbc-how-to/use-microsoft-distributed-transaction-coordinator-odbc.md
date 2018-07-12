---
title: Microsoft Distributed Transaction Coordinator (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e7661b628e2664ba58c1020bd55fdec1e3d3e58
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414192"
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Microsoft Distributed Transaction Coordinator 사용(ODBC)
    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>MS DTC를 사용하여 두 대 이상의 SQL Server를 업데이트하려면  
  
1.  MS DTC OLE DtcGetTransactionManager 함수를 사용하여 MS DTC에 연결합니다. MS DTC에 대한 자세한 내용은 Microsoft Distributed Transaction Coordinator를 참조하십시오.  
  
2.  설정할 각 Microsoft® SQL Server™ 연결에 대해 SQL DriverConnect를 한 번씩 호출합니다.  
  
3.  MS DTC OLE ITransactionDispenser::BeginTransaction 함수를 호출하여 MS DTC 트랜잭션을 시작하고 해당 트랜잭션을 나타내는 트랜잭션 개체를 가져옵니다.  
  
4.  MS DTC 트랜잭션에 참여시킬 각 ODBC 연결에 대해 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)을 한 번 이상 호출합니다. [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)의 두 번째 매개 변수는 SQL_ATTR_ENLIST_IN_DTC여야 하고 세 번째 매개 변수는 3단계에서 얻은 트랜잭션 개체여야 합니다.  
  
5.  업데이트할 각 SQL Server에 대해 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399)를 한 번씩 호출합니다.  
  
6.  MS DTC OLE ITransaction::Commit 함수를 호출하여 MS DTC 트랜잭션을 커밋합니다. 트랜잭션 개체가 더 이상 유효하지 않게 됩니다.  
  
 일련의 MS DTC 트랜잭션을 수행하려면 3 - 6단계를 반복합니다.  
  
 트랜잭션 개체에 대한 참조를 해제하려면 MS DTC OLE ITransaction::Return 함수를 호출합니다.  
  
 MS DTC 트랜잭션에서 ODBC 연결을 사용한 다음 로컬 SQL Server 트랜잭션에서 같은 연결을 사용하려면 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)을 SQL_DTC_DONE과 함께 호출합니다.  
  
> [!NOTE]  
>  앞의 4 - 5단계에서 제안한 대로 호출하는 대신 각 SQL Server에 대해 [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399)를 차례로 호출할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 수행 &#40;ODBC&#41;](../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
