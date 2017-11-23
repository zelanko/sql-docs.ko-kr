---
title: SQLProcedures | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0bb243692d3781449f1f3da4e4cc3cc316e7b8b4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 값을 반환합니다. **SQLProcedures** 는 결과 집합 열 PROCEDURE_TYPE에 대해 sql_pt_function을 합니다.  
  
 **SQLProcedures** 에 대 한 값이 존재 하는지 여부에 관계 없이 SQL_SUCCESS를 반환 *CatalogName, SchemaName* 또는 *ProcName* 매개 변수입니다. **SQLFetch** 이러한 매개 변수에서 잘못 된 값을 사용할 경우 SQL_NO_DATA를 반환 합니다.  
  
 **SQLProcedures** 는 정적 서버 커서에 대해 실행할 수 있습니다. 실행 하려고 **SQLProcedures** 업데이트할 수 있는 (동적 또는 키 집합) 커서에서 커서 유형이 변경 되었음을 나타내는 sql_success_with_info가 반환 됩니다.  
  
 **SQLProcedures** 이름이 일치 하는 모든 프로시저에 대 한 정보를 반환 *ProcName* 하 고 있는 현재 사용자에 VIEW DEFINITION 권한이 부여 또는 현재 사용자가 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLProcedures 함수](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
