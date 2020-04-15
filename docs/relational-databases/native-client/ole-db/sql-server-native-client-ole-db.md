---
title: SQL 서버 네이티브 클라이언트(OLE DB) | 마이크로 소프트 문서
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 424565f5eb1b0e9ee0770f988090ecb16788c585
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307282"
---
# <a name="sql-server-native-client-ole-db"></a>SQL Server Native Client(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLNCLI(네이티브 클라이언트 OLE DB 공급자)는 데이터에 액세스하는 데 사용되는 하위 수준 COM API입니다. 고성능이 필요한 도구, 유틸리티 및 하위 수준 구성 요소 개발에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] TDS(Tabular Data Stream) 프로토콜에 직접적으로 액세스하는 고성능 네이티브 공급자입니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 애플리케이션에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결할 수 있는 OLE DB 지원을 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 OLE DB 버전 2.0 을 준수하는 공급자입니다.  
 
> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] SQLNCLI(네이티브 클라이언트 OLE DB)는 더 이상 사용되지 않으며 새 개발 작업에는 사용하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server Native Client OLE DB 공급자 애플리케이션 만들기](../../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
-   [데이터 원본 개체 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
-   [명령](../../../relational-databases/native-client-ole-db-commands/commands.md)  
  
-   [행 집합](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
-   [저장 절차](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
-   [BLOB 및 OLE 개체](../../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)  
  
-   [테이블 및 인덱스](../../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
-   [데이터 형식&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
-   [스키마 행 집합 지원&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
-   [테이블 반환 매개 변수&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)  
  
-   [날짜 및 시간 기능 향상&#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
-   [큰 CLR 사용자 정의 형식&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md)  
  
-   [올레 DB &#40;파일스트림 지원&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [트랜잭션](../../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
-   [오류](../../../relational-databases/native-client-ole-db-errors/errors.md)  
  
-   [클라이언트 연결의 SPN&#40;서비스 사용자 이름&#41;&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
-   [스파스 열 지원&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md)  
  
-   [OLE DB&#41; 참조를 &#40;SQL 서버 네이티브 클라이언트](../../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)  
  
-   [OLE DB 방법 도움말 항목](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
