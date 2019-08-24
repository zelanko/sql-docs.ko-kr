---
title: ISO 옵션의 효과 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 442900f22aa408d91175e0a58b9f5b7ca7aceaef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937269"
---
# <a name="effects-of-iso-options"></a>ISO 옵션의 효과
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC 표준은 ISO 표준과 거의 일치하며, ODBC 애플리케이션은 ODBC 드라이버가 표준 동작을 수행할 것으로 예상합니다. ODBC 표준에서 정의 하는 동작이 좀 더 밀접 하 게 준수 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버 연결 된 SQL Server 버전에서 사용할 수 있는 ISO 옵션을 항상 사용 합니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버의 인스턴스에 연결 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 서버 클라이언트를 사용 하는지 감지 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버 및 여러 옵션 집합.  
  
 드라이버는 이러한 문을 자체적으로 실행하며 ODBC 애플리케이션에서 이를 요청하는 것은 아닙니다. 이러한 옵션을 설정하면 서버 동작이 ISO 표준과 일치하게 되므로 드라이버를 사용하는 ODBC 애플리케이션의 이식성을 높일 수 있습니다.  
  
 DB-Library 기반 애플리케이션은 일반적으로 이러한 옵션을 설정하지 않습니다. 다른 관찰 하는 사이트에 문제가 가리키는 SQL 명령문 실행 가정 하지 않아야이 ODBC 또는 Db-library 클라이언트 간에 동작의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버. 해야 먼저 문을 다시 실행 하십시오의 동일한 옵션 설정으로 DB 라이브러리 환경에서 사용할 것은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버.  
  
 SET 옵션은 사용자와 애플리케이션이 언제라도 설정하거나 해제할 수 있으므로 저장 프로시저 및 트리거 개발자는 위에 나열된 SET 옵션을 설정한 상태와 해제한 상태 모두에서 프로시저 및 트리거를 신중하게 테스트해야 합니다. 이렇게 하면 프로시저나 트리거가 호출될 때 특정 연결에서 설정하는 옵션에 관계없이 프로시저 및 트리거가 올바르게 작동합니다. 위의 옵션 중 하나에 대한 특정한 설정이 필요한 트리거 또는 저장 프로시저는 트리거 또는 저장 프로시저의 시작 부분에서 SET 문을 실행해야 합니다. 이 SET 문은 해당 트리거 또는 저장 프로시저가 실행되는 동안에만 적용됩니다. 프로시저 또는 트리거가 종료되면 원래 설정이 복원됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 네 번째 SET 옵션인 CONCAT_NULL_YIELDS_NULL이 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버가 경우이 옵션을 설정 하지 않으면 AnsiNPW = NO 또는 데이터 소스에 지정 된 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 또는 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md).  
  
 앞에서 설명한 ISO 옵션과 마찬가지로 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 경우 QUOTED_IDENTIFIER 옵션을 설정 하지 않습니다 QuotedID = NO 데이터 소스의 나 지정 된 **SQLDriverConnect** 또는  **SQLBrowseConnect**합니다.  
  
 드라이버가 SET 옵션의 현재 상태를 알 수 있도록 ODBC 애플리케이션은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SET 문을 사용하여 이러한 옵션을 설정해서는 안 되며 데이터 원본 또는 연결 옵션을 통해서만 이러한 옵션을 설정해야 합니다. 애플리케이션이 SET 문을 실행하면 드라이버가 잘못된 SQL 문을 생성할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [문 실행 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
