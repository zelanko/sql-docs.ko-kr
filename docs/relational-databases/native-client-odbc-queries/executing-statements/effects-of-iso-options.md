---
title: "ISO 옵션의 효과 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2267290d43ec746fd3f2d11597eeefa498651e62
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="effects-of-iso-options"></a>ISO 옵션의 효과
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC 표준은 ISO 표준과 거의 일치하며, ODBC 응용 프로그램은 ODBC 드라이버가 표준 동작을 수행할 것으로 예상합니다. ODBC 표준에서 정의 하는 더욱 긴밀 하 게 준수 하는 동작을 만들기 위해는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 연결 하는 SQL Server 버전에서 사용할 수 있는 ISO 옵션을 항상 사용 합니다.  
  
 때는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 인스턴스로 연결할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 클라이언트에서 사용 감지 되 면 서버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 몇 가지 옵션 집합.  
  
 드라이버는 이러한 문을 자체적으로 실행하며 ODBC 응용 프로그램에서 이를 요청하는 것은 아닙니다. 이러한 옵션을 설정하면 서버 동작이 ISO 표준과 일치하게 되므로 드라이버를 사용하는 ODBC 응용 프로그램의 이식성을 높일 수 있습니다.  
  
 DB-Library 기반 응용 프로그램은 일반적으로 이러한 옵션을 설정하지 않습니다. 다른 관찰 하는 사이트에 문제가 가리키는 동일한 SQL 문을 실행할 것 가정 안이 때 ODBC 또는 Db-library 클라이언트 간에 동작이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버. 이러한 해야 먼저 문을 다시 실행 옵션과 동일한 SET 옵션으로 Db-library 환경에서 사용 하면 사용 하는 대로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버.  
  
 SET 옵션은 사용자와 응용 프로그램이 언제라도 설정하거나 해제할 수 있으므로 저장 프로시저 및 트리거 개발자는 위에 나열된 SET 옵션을 설정한 상태와 해제한 상태 모두에서 프로시저 및 트리거를 신중하게 테스트해야 합니다. 이렇게 하면 프로시저나 트리거가 호출될 때 특정 연결에서 설정하는 옵션에 관계없이 프로시저 및 트리거가 올바르게 작동합니다. 위의 옵션 중 하나에 대한 특정한 설정이 필요한 트리거 또는 저장 프로시저는 트리거 또는 저장 프로시저의 시작 부분에서 SET 문을 실행해야 합니다. 이 SET 문은 해당 트리거 또는 저장 프로시저가 실행되는 동안에만 적용됩니다. 프로시저 또는 트리거가 종료되면 원래 설정이 복원됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 네 번째 SET 옵션인 CONCAT_NULL_YIELDS_NULL이 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 경우 이러한 옵션을 설정 하지 않으면 AnsiNPW = NO 데이터 원본이 나 둘 모두에 지정 된 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 또는 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)합니다.  
  
 앞서 언급 한 ISO 옵션과 마찬가지로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 경우 QUOTED_IDENTIFIER 옵션을 설정 하지 않습니다 QuotedID = NO 데이터 원본이 나 둘 모두에 지정 된 **SQLDriverConnect** 또는  **SQLBrowseConnect**합니다.  
  
 드라이버가 SET 옵션의 현재 상태를 알 수 있도록 ODBC 응용 프로그램은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SET 문을 사용하여 이러한 옵션을 설정해서는 안 되며 데이터 원본 또는 연결 옵션을 통해서만 이러한 옵션을 설정해야 합니다. 응용 프로그램이 SET 문을 실행하면 드라이버가 잘못된 SQL 문을 생성할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [실행 중인 문 &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
