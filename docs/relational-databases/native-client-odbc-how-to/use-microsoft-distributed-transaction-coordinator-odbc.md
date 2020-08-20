---
description: Microsoft Distributed Transaction Coordinator 사용(ODBC)
title: DTC(Distributed Transaction Coordinator) (ODBC)
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7e35f7ed3cc4f93dd4a3b9a7ef697733cbdf99b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499194"
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Microsoft Distributed Transaction Coordinator 사용(ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>MS DTC를 사용하여 두 대 이상의 SQL Server를 업데이트하려면  
  
1.  MS DTC OLE DtcGetTransactionManager 함수를 사용하여 MS DTC에 연결합니다. MS DTC에 대한 자세한 내용은 Microsoft Distributed Transaction Coordinator를 참조하십시오.  
  
2.  설정 하려는 각 SQL Server 연결에 대해 SQL DriverConnect를 한 번씩 호출 합니다.  
  
3.  MS DTC OLE ITransactionDispenser::BeginTransaction 함수를 호출하여 MS DTC 트랜잭션을 시작하고 해당 트랜잭션을 나타내는 트랜잭션 개체를 가져옵니다.  
  
4.  MS DTC 트랜잭션에 참여시킬 각 ODBC 연결에 대해 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)을 한 번 이상 호출합니다. [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)의 두 번째 매개 변수는 SQL_ATTR_ENLIST_IN_DTC여야 하고 세 번째 매개 변수는 3단계에서 얻은 트랜잭션 개체여야 합니다.  
  
5.  업데이트할 각 SQL Server에 대해 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)를 한 번씩 호출합니다.  
  
6.  MS DTC OLE ITransaction::Commit 함수를 호출하여 MS DTC 트랜잭션을 커밋합니다. 트랜잭션 개체가 더 이상 유효하지 않게 됩니다.  

 일련의 MS DTC 트랜잭션을 수행하려면 3 - 6단계를 반복합니다.  
  
 트랜잭션 개체에 대한 참조를 해제하려면 MS DTC OLE ITransaction::Return 함수를 호출합니다.  
  
 MS DTC 트랜잭션에서 ODBC 연결을 사용한 다음 로컬 SQL Server 트랜잭션에서 같은 연결을 사용하려면 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)을 SQL_DTC_DONE과 함께 호출합니다.  
  
> [!NOTE]  
>  앞의 4 - 5단계에서 제안한 대로 호출하는 대신 각 SQL Server에 대해 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 및 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399)를 차례로 호출할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;트랜잭션 수행 ](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
