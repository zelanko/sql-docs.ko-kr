---
title: 쿼리 실행 (ODBC) | Microsoft Docs
description: ODBC 응용 프로그램은 연결 핸들을 초기화 하 고 데이터 원본에 연결 하 여 SQL Server 인스턴스에서 문을 실행할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, executing queries
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
- SQL Server Native Client ODBC driver, queries
- queries [ODBC]
ms.assetid: d935bcba-8ce6-4159-8395-6c86431602ad
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33248595ddf7a52e17664847b2a7c9e99a4f8e1a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730342"
---
# <a name="executing-queries-odbc"></a>쿼리 실행(ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  ODBC 애플리케이션은 연결 핸들을 초기화하고 데이터 원본에 연결한 후 연결 핸들에 하나 이상의 문 핸들을 할당합니다. 그런 다음 응용 프로그램은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문 핸들에서 문을 실행할 수 있습니다. SQL 문을 실행하는 이벤트의 일반적인 순서는 다음과 같습니다.  
  
1.  필요한 모든 문 특성을 설정합니다.  
  
2.  해당 문을 구성합니다.  
  
3.  해당 문을 실행합니다.  
  
4.  결과 집합을 검색합니다.  
  
 애플리케이션은 SQL 문으로 반환된 모든 결과 집합에서 모든 행을 검색한 후 동일한 문 핸들에서 다른 쿼리를 실행할 수 있습니다. 응용 프로그램에서 특정 결과 집합의 모든 행을 검색할 필요가 없다고 결정 한 경우 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 또는 [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)를 호출 하 여 나머지 결과 집합을 취소할 수 있습니다.  
  
 ODBC 애플리케이션에서 서로 다른 데이터를 사용하여 동일한 SQL 문을 여러 번 실행해야 한다면 SQL 문을 생성할 때 물음표(?)로 표시되는 매개 변수 표식을 사용합니다.  
  
```  
INSERT INTO MyTable VALUES (?, ?, ?)  
```  
  
 그런 다음 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)를 호출 하 여 각 매개 변수 표식을 프로그램 변수에 바인딩할 수 있습니다.  
  
 모든 SQL 문을 실행하고 해당 결과 집합을 처리한 후 애플리케이션은 문 핸들을 해제합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 연결 핸들 당 여러 문 핸들을 지원 합니다. 트랜잭션은 연결 수준에서 관리되므로 단일 연결 핸들의 모든 문 핸들에서 수행된 모든 작업은 동일한 트랜잭션의 일부로 관리됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [문 핸들 할당](../../relational-databases/native-client-odbc-queries/allocating-a-statement-handle.md)  
  
-   [ODBC&#41;&#40;SQL 문 생성](../../relational-databases/native-client-odbc-queries/constructing-an-sql-statement-odbc.md)  
  
-   [쿼리에 대한 SQL 문 생성](../../relational-databases/native-client-odbc-queries/constructing-sql-statements-for-cursors.md)  
  
-   [문 매개 변수 사용](../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)  
  
-   [ODBC&#41;&#40;문을 실행 하는 중](../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
-   [문 핸들 해제](../../relational-databases/native-client-odbc-queries/freeing-a-statement-handle.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
