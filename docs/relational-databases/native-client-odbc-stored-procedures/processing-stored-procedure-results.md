---
title: 저장 프로시저 결과 처리 | Microsoft Docs
description: 저장 프로시저에서 응용 프로그램에 데이터를 반환 하는 데 사용 하 SQL Server 메커니즘에 대해 알아봅니다. 응용 프로그램은 이러한 모든 형식을 처리할 수 있어야 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3027c2624d34d685491d00fe9e5d84109a0322d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967554"
---
# <a name="processing-stored-procedure-results"></a>저장 프로시저 결과 처리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 데이터를 반환하기 위해 네 가지 메커니즘을 사용합니다.  
  
-   프로시저의 각 SELECT 문은 결과 집합을 생성합니다.  
  
-   프로시저는 출력 매개 변수를 통해 데이터를 반환할 수 있습니다.  
  
-   커서 출력 매개 변수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 커서를 다시 전달할 수 있습니다.  
  
-   프로시저에는 정수 반환 코드가 있을 수 있습니다.  
  
 애플리케이션은 저장 프로시저의 이러한 모든 출력을 처리할 수 있어야 합니다. CALL 또는 EXECUTE 문에는 반환 코드 및 출력 매개 변수에 대한 매개 변수 표식이 포함되어야 합니다. [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) 를 사용 하 여 모두 출력 매개 변수로 바인딩하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 출력 값을 바인딩된 변수에 전송 합니다. 출력 매개 변수 및 반환 코드는에서 클라이언트로 반환 되는 마지막 항목 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 입니다. [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 가 SQL_NO_DATA를 반환할 때까지 응용 프로그램에 반환 되지 않습니다.  
  
 ODBC는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서 매개 변수를 바인딩하는 기능을 제공하지 않습니다. 출력 커서 매개 변수가 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저는 실행하기 전에 모든 출력 매개 변수를 바인딩해야 하므로 ODBC 애플리케이션은 이를 호출할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [저장 프로시저 실행](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
