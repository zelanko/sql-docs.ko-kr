---
title: 환경 핸들 할당 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-communication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1a24ae1e30ca2c6d39584635460df703d5b04a42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="allocating-an-environment-handle"></a>환경 핸들 할당
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  응용 프로그램에서 ODBC 함수를 호출하려면 먼저 ODBC 환경을 초기화하고 환경 핸들을 할당해야 합니다. 이 핸들은 전역 컨텍스트 핸들이고 ODBC의 다른 핸들에 대한 자리 표시자입니다. 호출 하 여이 작업을 수행 **SQLAllocHandle** 와 *HandleType* 매개 변수를 SQL_HANDLE_ENV로 설정 하 고 *InputHandle* SQL_NULL_HANDLE로 설정 합니다.  
  
 응용 프로그램은 환경 핸들을 할당한 후 환경 특성을 설정하여 사용할 ODBC 함수 호출 버전을 지정해야 합니다. ODBC 3 사용 하려면. *x* 함수 호출 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) 와 *특성* 매개 변수를 sql_attr_odbc_version으로 설정 하 고 *ValuePtr* SQL_OV_로 설정 ODBC3 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server와 통신 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
