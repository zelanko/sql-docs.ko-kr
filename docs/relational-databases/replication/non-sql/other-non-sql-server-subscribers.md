---
title: "다른 SQL Server 이외 구독자 | Microsoft Docs"
ms.custom: ""
ms.date: "03/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server 이외 구독자, 다른 유형"
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# 다른 SQL Server 이외 구독자
  비-목록에 대 한[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구독자에서 지 원하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)], 참조 [비-SQL Server 구독자](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)합니다. 이 항목에는 ODBC 드라이버 및 OLE DB 공급자에 대한 요구 사항 정보가 포함되어 있습니다.  
  
## ODBC 드라이버 요구 사항  
 ODBC 드라이버는  
  
-   ODBC 수준-1과 호환되어야 합니다.  
  
-   스레드로부터 안전한 배포자 환경이어야 합니다.  
  
-   트랜잭션이 가능해야 합니다.  
  
-   DDL(데이터 정의 언어)을 지원해야 합니다.  
  
-   읽기 전용이 될 수 없습니다.  
  
-   와 같은 긴 테이블 이름을 지원 해야 **MSreplication_subscriptions**합니다.  
  
## OLE DB 인터페이스를 통한 복제  
 OLE DB 공급자는 트랜잭션 복제에 대해 다음과 같은 개체를 지원해야 합니다.  
  
-   **DataSource** 개체  
  
-   **Session** 개체  
  
-   **Command** 개체  
  
-   **Rowset** 개체  
  
-   **Error** 개체  
  
### DataSource 개체 인터페이스  
 다음은 데이터 원본에 연결하기 위해 필요한 인터페이스입니다.  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
 공급자가 **IDBInfo** 인터페이스를 지원하는 경우 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 이 인터페이스를 사용하여 따옴표 붙은 식별 문자, 최대 SQL 문 길이, 테이블과 열 이름의 최대 문자 수 등의 정보를 검색합니다.  
  
### Session 개체 인터페이스  
 필요한 인터페이스는 다음과 같습니다.  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### Command 개체 인터페이스  
 필요한 인터페이스는 다음과 같습니다.  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** 는 매개 변수 접근자를 만들기 위해 필요합니다. 공급자가 **IColumnRowset**을 지원하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 이 인터페이스를 사용하여 열이 ID 열인지 여부를 결정합니다.  
  
### Rowset 개체 인터페이스  
 필요한 인터페이스는 다음과 같습니다.  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 응용 프로그램은 구독 데이터베이스에서 생성된 복제된 테이블의 행 집합을 열어야 합니다. **IColumnsInfo** 와 **IAccessor** 는 이 행 집합의 데이터에 액세스하기 위해 필요합니다.  
  
### Error 개체 인터페이스  
 다음 인터페이스를 사용하여 오류를 관리합니다.  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 OLE DB 공급자에 의해 지원되는 경우에는 **ISQLErrorInfo** 를 사용합니다.  
  
 OLE DB 공급자에 대한 자세한 내용은 사용 중인 OLE DB 공급자와 함께 제공된 설명서를 참조하십시오.  
  
## 참고 항목  
 [SQL Server 이외 구독자](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  