---
title: 문 실행 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC]
- ODBC applications, statements
- statements [ODBC], executing
ms.assetid: 063fc40d-ff81-490d-9c9b-2faefb729f37
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1c4d892ca25aa2c3bff62ddb5f133f11b952d1d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937182"
---
# <a name="executing-statements-odbc"></a>문 실행(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 SQL 문을 실행 하는 다양 한 방법을 제공을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스:  
  
-   직접 실행  
  
-   준비된 실행  
  
 직접 실행에서는 포함 하는 문자 문자열을 작성을 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문과 사용 하 여 실행에 대 한 제출 합니다 **SQLExecDirect** 함수. 준비된 실행에서는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이 포함된 문자열을 작성한 다음 두 가지 단계로 실행합니다. 첫 번째 단계에서 사용 하는 [SQLPrepare 함수](https://go.microsoft.com/fwlink/?LinkId=59360) 함수를 구문 분석에서 문의 실행 계획을 컴파일하는 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]합니다. 두 번째 단계에서 사용 하 여 **SQLExecute** 이전에 준비 된 실행 계획을 실행 하는 함수입니다. 이렇게 하면 각각의 실행에서 구문 분석 및 컴파일 오버헤드를 줄일 수 있습니다. 준비된 실행은 애플리케이션에서 매개 변수가 있는 동일한 SQL 문을 반복적으로 실행하는 데 많이 사용됩니다.  
  
 직접 실행과 준비된 실행에서 모두 단일 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이나 SQL 문의 일괄 처리를 실행하거나 저장 프로시저를 호출할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [직접 실행](../../../relational-databases/native-client-odbc-queries/executing-statements/direct-execution.md)  
  
-   [준비된 실행](../../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
-   [절차](../../../relational-databases/native-client-odbc-queries/executing-statements/procedures.md)  
  
-   [문 일괄 처리](../../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)  
  
-   [ISO 옵션의 효과](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 실행 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
