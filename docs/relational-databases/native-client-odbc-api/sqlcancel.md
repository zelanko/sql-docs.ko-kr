---
title: SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 05b4f3208b13f1f13f584628e9d495ff1cbf4060
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789408"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516) 항목의 설명에 따르면, ODBC 2.x에서는 문에 대한 처리가 수행되지 않았을 때 애플리케이션에서 **SQLCancel** 을 호출하는 경우 **SQLCancel** 호출 결과는 **SQLFreeStmt** 옵션을 사용하여 **SQL_CLOSE** 를 실행한 결과와 같습니다. 이 동작은 실행을 완료하기 위한 용도로만 정의되며, 애플리케이션에서는 **SQLFreeStmt** 또는 **SQLCloseCurs또는** to close curs또는s. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 애플리케이션에서 ODBC API 버전을 3.5.x 이상으로 설정하는 경우에도 **SQLCancel** 함수는 ODBC 2.x 동작을 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
