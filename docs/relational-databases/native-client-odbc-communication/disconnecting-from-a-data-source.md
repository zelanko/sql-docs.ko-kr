---
description: 데이터 원본에서 연결 끊기
title: 데이터 원본에서 연결을 끊는 중 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fd4277c773c07e56a8669d1bb5c6f9d8e024d769
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464974"
---
# <a name="disconnecting-from-a-data-source"></a>데이터 원본에서 연결 끊기
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  응용 프로그램이 데이터 원본 사용을 마치면 **Sqldisconnect** 를 호출 합니다. **Sqldisconnect** 는 연결에 할당 된 모든 문을 해제 하 고 데이터 원본에서 드라이버의 연결을 끊습니다. 연결을 끊은 후 응용 프로그램은 [Sqlfreehandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) 을 호출 하 여 연결 핸들을 해제할 수 있습니다. 종료 하기 전에 응용 프로그램은 **Sqlfreehandle** 을 호출 하 여 환경 핸들을 해제 합니다.  
  
 연결을 끊은 후 애플리케이션에서 할당된 연결 핸들을 다시 사용하여 다른 데이터 원본에 연결하거나 동일한 데이터 원본에 다시 연결할 수 있습니다. 연결을 끊은 후 나중에 다시 연결하는 대신 연결된 상태로 유지할지 여부를 결정하는 경우 애플리케이션 작성기에서 각 옵션의 상대 비용을 고려해야 합니다. 데이터 원본에 연결하여 연결된 상태로 유지하는 것은 연결 매체에 따라 비교적 비용이 높을 수 있습니다. 장단점을 고려할 때 애플리케이션은 동일한 데이터 원본에서 추가 작업이 수행될 확률과 타이밍에 대해서도 가정해야 합니다. 한 애플리케이션에서 둘 이상의 연결을 사용해야 할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server &#40;ODBC&#41;와 통신 ](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
