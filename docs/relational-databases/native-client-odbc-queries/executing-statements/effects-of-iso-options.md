---
title: ISO 옵션의 효과 | 마이크로 소프트 문서
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: adf37d03f5ea4f06be4d58e60deca68e10d45abb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297940"
---
# <a name="effects-of-iso-options"></a>ISO 옵션의 효과
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC 표준은 ISO 표준과 거의 일치하며, ODBC 애플리케이션은 ODBC 드라이버가 표준 동작을 수행할 것으로 예상합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 동작이 ODBC 표준에 정의된 동작과 더 밀접하게 일치하도록 네이티브 클라이언트 ODBC 드라이버는 항상 연결하는 SQL Server 버전에서 사용할 수 있는 모든 ISO 옵션을 사용합니다.  
  
 네이티브 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 ODBC 드라이버가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에 연결하면 서버는 클라이언트가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버를 사용하고 있음을 감지하고 여러 옵션을 설정합니다.  
  
 드라이버는 이러한 문을 자체적으로 실행하며 ODBC 애플리케이션에서 이를 요청하는 것은 아닙니다. 이러한 옵션을 설정하면 서버 동작이 ISO 표준과 일치하게 되므로 드라이버를 사용하는 ODBC 애플리케이션의 이식성을 높일 수 있습니다.  
  
 DB-Library 기반 애플리케이션은 일반적으로 이러한 옵션을 설정하지 않습니다. 동일한 SQL 문을 실행할 때 ODBC 또는 DB-Library 클라이언트 간에 서로 다른 동작을 관찰하는 사이트는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이 점을 네이티브 클라이언트 ODBC 드라이버의 문제로 가정해서는 안 됩니다. 먼저 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버에서 사용하는 것과 동일한 SET 옵션을 사용하여 DB-Library 환경에서 문을 다시 실행해야 합니다.  
  
 SET 옵션은 사용자와 애플리케이션이 언제라도 설정하거나 해제할 수 있으므로 저장 프로시저 및 트리거 개발자는 위에 나열된 SET 옵션을 설정한 상태와 해제한 상태 모두에서 프로시저 및 트리거를 신중하게 테스트해야 합니다. 이렇게 하면 프로시저나 트리거가 호출될 때 특정 연결에서 설정하는 옵션에 관계없이 프로시저 및 트리거가 올바르게 작동합니다. 위의 옵션 중 하나에 대한 특정한 설정이 필요한 트리거 또는 저장 프로시저는 트리거 또는 저장 프로시저의 시작 부분에서 SET 문을 실행해야 합니다. 이 SET 문은 해당 트리거 또는 저장 프로시저가 실행되는 동안에만 적용됩니다. 프로시저 또는 트리거가 종료되면 원래 설정이 복원됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 네 번째 SET 옵션인 CONCAT_NULL_YIELDS_NULL이 설정됩니다. 네이티브 클라이언트 ODBC 드라이버는 AnsiNPW=NO가 데이터 원본또는 [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 또는 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)에 지정된 경우 이러한 옵션을 설정하지 않습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
 앞에서 설명한 ISO 옵션과 마찬가지로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 데이터 원본 또는 **SQLDriverConnect** 또는 **SQLBrowseConnect에서**quotedID=NO가 지정된 경우 QUOTED_IDENTIFIER 옵션을 켜지 않습니다.  
  
 드라이버가 SET 옵션의 현재 상태를 알 수 있도록 ODBC 애플리케이션은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SET 문을 사용하여 이러한 옵션을 설정해서는 안 되며 데이터 원본 또는 연결 옵션을 통해서만 이러한 옵션을 설정해야 합니다. 애플리케이션이 SET 문을 실행하면 드라이버가 잘못된 SQL 문을 생성할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;문 실행](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)   
 [SQL드라이버 연결](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)  
  
  
