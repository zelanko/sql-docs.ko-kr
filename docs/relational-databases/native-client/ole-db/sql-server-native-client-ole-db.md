---
title: OLE DB
description: SQL Server Native Client OLE DB 공급자는 데이터에 액세스 하기 위한 COM API로, 고성능을 필요로 하는 도구, 유틸리티 또는 하위 수준 구성 요소에 사용 됩니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, about SQL Server Native Client OLE DB provider
- OLE DB, SQL Server Native Client OLE DB provider
- data access [SQL Server Native Client], OLE DB
- SQLNCLI, OLE DB
- OLE DB
- SQL Server Native Client OLE DB provider
- SQL Server Native Client, OLE DB
ms.assetid: da846da4-ec19-4a4f-81fb-7d5a2b2bf80a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 133f9a53d6de89b6d8720781606301b939a32bf3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467554"
---
# <a name="sql-server-native-client-ole-db"></a>SQL Server Native Client(OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]SQLNCLI (Native Client OLE DB provider)는 데이터 액세스에 사용 되는 하위 수준 COM API입니다. 고성능이 필요한 도구, 유틸리티 및 하위 수준 구성 요소 개발에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TDS(Tabular Data Stream) 프로토콜에 직접적으로 액세스하는 고성능 네이티브 공급자입니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 애플리케이션에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 수 있는 OLE DB 지원을 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 OLE DB 버전 2.0 호환 공급자입니다.  
 
> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB (SQLNCLI)는 더 이상 사용 되지 않으며 새로운 개발 작업에 사용 하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server Native Client OLE DB 공급자 애플리케이션 만들기](../../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
-   [데이터 원본 개체 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
-   [명령](../../../relational-databases/native-client-ole-db-commands/commands.md)  
  
-   [행 집합](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
-   [저장 프로시저](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
-   [BLOB 및 OLE 개체](../../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)  
  
-   [테이블 및 인덱스](../../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
-   [데이터 형식 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
-   [스키마 행 집합 지원&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
-   [테이블 반환 매개 변수&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)  
  
-   [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
-   [큰 CLR 사용자 정의 형식&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md)  
  
-   [FILESTREAM Support &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [트랜잭션](../../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
-   [Errors](../../../relational-databases/native-client-ole-db-errors/errors.md)  
  
-   [클라이언트 연결&#40;OLE DB&#41;의 SPN&#40;서비스 사용자 이름&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
-   [스파스 열 지원&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md)  
  
-   [SQL Server Native Client &#40;OLE DB&#41; 참조](../../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)  
  
-   [OLE DB 방법 도움말 항목](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
