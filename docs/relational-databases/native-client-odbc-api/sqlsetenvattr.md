---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 315a34127e5ff7d9a23f24fd37de23eb7dffef8a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012393"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [ODBC 프로그래머 참조(ODBC Programmer's Reference)](https://go.microsoft.com/fwlink/?LinkId=45250) 에는 ODBC 2. **x** 또는 ODBC 3.*x* API를 사용하도록 작성된 애플리케이션에서 ODBC 드라이버가*SQLSetEnvAttr* 특성 사양을 해석하는 방법이 정의되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 이러한 규칙을 준수합니다.  
  
 **SQLSetEnvAttr** 은 연결 풀링을 사용할지 여부를 제어하는 특성 중 하나를 갖습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 연결 풀링을 사용하려면 *SQLDriverConnect* 또는 [SQLConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 를 사용하여 연결할 때 **DriverCompletion**매개 변수를 SQL_DRIVER_NOPROMPT로 설정해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLSetEnvAttr 함수](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
