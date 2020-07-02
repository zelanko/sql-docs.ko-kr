---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dad8e1277a0161755f65bdafa1276ab401f9e3b7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789398"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  **SQLCloseCursor** 는 [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) 를 SQL_CLOSE의 *옵션* 값으로 바꿉니다. **SQLCloseCursor**를 수신한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 보류 중인 결과 집합 행을 무시합니다. 문의 열 및 매개 변수 바인딩(있는 경우)은 **SQLCloseCursor**에 의해 변경되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
