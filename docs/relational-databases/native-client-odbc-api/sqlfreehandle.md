---
description: SQLFreeHandle
title: SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ee9fa4d5dabc24bfe761de638c3b5626c89fd6d3
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809808"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  수동 커밋 모드에서 트랜잭션이 열려 있을 때 문 핸들에 대해 **SQLFreeHandle** 을 호출하면 보류 중인 변경 내용이 데이터베이스에 롤백됩니다. 문 핸들에 대해 **SQLFreeHandle** 을 호출하면 항상 열려 있는 모든 커서가 닫히고 보류 중인 결과가 삭제되어 문 핸들에 연결된 모든 리소스가 해제됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLFreeHandle 함수](../../odbc/reference/syntax/sqlfreehandle-function.md)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
