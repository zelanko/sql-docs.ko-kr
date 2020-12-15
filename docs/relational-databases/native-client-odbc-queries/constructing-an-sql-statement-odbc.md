---
title: SQL 문 생성 (ODBC) | Microsoft Docs
description: SQL Server Client ODBC 드라이버를 사용 하 여 SQL 문을 처리 하는 방법에 대해 알아봅니다. Transact-sql 문을 구문 분석 하 고 다른 데이터베이스를 변경 되지 않은 상태로 데이터베이스에 전달 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
ms.assetid: 0acc71e2-8004-4dd8-8592-05c022bdd692
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5963474c575dc33d7c33da14ae13dc43608a81b8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438429"
---
# <a name="constructing-an-sql-statement-odbc"></a>SQL 문 생성(ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC 애플리케이션에서는 거의 모든 데이터베이스 액세스를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 수행합니다. 이러한 문의 형식은 애플리케이션의 요구 사항에 따라 달라집니다. SQL 문은 다음과 같은 방법으로 생성할 수 있습니다.  
  
-   하드 코딩  
  
     애플리케이션에서 고정 태스크로 수행한 정적 문  
  
-   런타임에 생성  
  
     사용자가 SELECT, WHERE 및 ORDER BY와 같은 일반적인 절을 사용하여 문을 알맞게 조정할 수 있도록 런타임에 생성한 SQL 문. 여기에는 사용자가 입력한 임시 쿼리도 포함됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLIENT odbc 드라이버는에서 직접 지원 하지 않는 odbc 및 ISO 구문에 대해서만 SQL 문을 구문 분석 하며,이는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 드라이버가로 변환 [!INCLUDE[tsql](../../includes/tsql-md.md)] 됩니다. 다른 모든 SQL 구문은 변경되지 않고 [!INCLUDE[ssDE](../../includes/ssde-md.md)]으로 전달되며, 그곳에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 해당 구문이 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인지 확인합니다. 이 방법은 다음 두 가지 이점을 제공합니다.  
  
-   오버헤드 감소  
  
     드라이버에서 ODBC 및 ISO 절의 일부 집합만 스캔하면 되므로 드라이버의 처리 오버헤드가 최소화됩니다.  
  
-   유연성  
  
     프로그래머가 애플리케이션의 이식성이 알맞게 조정할 수 있습니다. 여러 데이터베이스에 대한 이식성을 향상하려면 주로 ODBC 및 ISO 구문을 사용합니다. 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 향상된 기능을 사용하려면 적절한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT odbc 드라이버는 [!INCLUDE[tsql](../../includes/tsql-md.md)] odbc 기반 응용 프로그램이의 모든 기능을 활용할 수 있도록 전체 구문을 지원 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 SELECT 문의 열 목록에는 현재 태스크를 수행하는 데 필요한 열만 포함되어 있어야 합니다. 그래야만 네트워크를 통해 보내는 데이터의 양이 줄 뿐 아니라 데이터베이스 변경이 애플리케이션에 미치는 영향도 줄어듭니다. 애플리케이션에서 테이블의 열을 참조하지 않는 경우 해당 열이 변경되어도 애플리케이션에는 영향을 주지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;쿼리 실행 ](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
