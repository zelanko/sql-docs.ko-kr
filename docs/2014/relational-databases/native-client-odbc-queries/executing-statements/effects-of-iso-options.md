---
title: ISO 옵션의 효과 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ISO options (ODBC)
- ODBC applications, ISO options
- ODBC applications, statements
- SQL Server Native Client ODBC driver, ISO options
- statements [ODBC], ISO options
ms.assetid: 813f1397-fa0b-45ec-a718-e13fe2fb88ac
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec72da4557bc851c833018cfff2cc53f8576da0b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411722"
---
# <a name="effects-of-iso-options"></a>ISO 옵션의 효과
  ODBC 표준은 ISO 표준과 거의 일치하며, ODBC 응용 프로그램은 ODBC 드라이버가 표준 동작을 수행할 것으로 예상합니다. ODBC 표준에 정의 된 보다 긴밀 하 게 준수 동작을 확인 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 항상 연결 하는 SQL Server 버전에서 사용할 수 있는 ISO 옵션을 사용 합니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버의 인스턴스에 연결 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 서버에서 클라이언트에서 사용을 검색 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 몇 가지 옵션 집합.  
  
 드라이버는 이러한 문을 자체적으로 실행하며 ODBC 응용 프로그램에서 이를 요청하는 것은 아닙니다. 이러한 옵션을 설정하면 서버 동작이 ISO 표준과 일치하게 되므로 드라이버를 사용하는 ODBC 응용 프로그램의 이식성을 높일 수 있습니다.  
  
 DB-Library 기반 응용 프로그램은 일반적으로 이러한 옵션을 설정하지 않습니다. 다르더라도 사이트 문제를 가리키는 경우 동일한 SQL 문을 실행 가정해 서는 안이 ODBC 또는 Db-library 클라이언트 간에 동작이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버. 이러한 해야 먼저 문을 다시 실행 옵션과 동일한 SET 옵션으로 Db-library 환경에서 사용할 것으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버.  
  
 SET 옵션은 사용자와 응용 프로그램이 언제라도 설정하거나 해제할 수 있으므로 저장 프로시저 및 트리거 개발자는 위에 나열된 SET 옵션을 설정한 상태와 해제한 상태 모두에서 프로시저 및 트리거를 신중하게 테스트해야 합니다. 이렇게 하면 프로시저나 트리거가 호출될 때 특정 연결에서 설정하는 옵션에 관계없이 프로시저 및 트리거가 올바르게 작동합니다. 위의 옵션 중 하나에 대한 특정한 설정이 필요한 트리거 또는 저장 프로시저는 트리거 또는 저장 프로시저의 시작 부분에서 SET 문을 실행해야 합니다. 이 SET 문은 해당 트리거 또는 저장 프로시저가 실행되는 동안에만 적용됩니다. 프로시저 또는 트리거가 종료되면 원래 설정이 복원됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 네 번째 SET 옵션인 CONCAT_NULL_YIELDS_NULL이 설정됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 경우 이러한 옵션을 설정 하지 않으면 AnsiNPW = NO 데이터 소스의 나 지정 된 [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) 또는 [SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)합니다.  
  
 앞에서 설명한 ISO 옵션과 마찬가지로 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 경우 QUOTED_IDENTIFIER 옵션을 설정 하지 않습니다 QuotedID = NO 데이터 소스의 나 지정 된 **SQLDriverConnect** 또는  **SQLBrowseConnect**합니다.  
  
 드라이버가 SET 옵션의 현재 상태를 알 수 있도록 ODBC 응용 프로그램은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SET 문을 사용하여 이러한 옵션을 설정해서는 안 되며 데이터 원본 또는 연결 옵션을 통해서만 이러한 옵션을 설정해야 합니다. 응용 프로그램이 SET 문을 실행하면 드라이버가 잘못된 SQL 문을 생성할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [문 실행 &#40;ODBC&#41;](executing-statements-odbc.md)   
 [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)   
 [SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)  
  
  
