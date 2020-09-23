---
title: SQL Server 기능용 OLE DB 드라이버
description: 데이터베이스 미러링, 비동기 작업, Azure Active Directory 등 OLE DB Driver for SQL Server에서 지원하는 기능에 대해 알아봅니다.
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c93a622561a7c4384f4e7be3d0e95daf9d46abb
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861449"
---
# <a name="ole-db-driver-for-sql-server-features"></a>SQL Server 기능용 OLE DB 드라이버
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버는 WDAC(Windows Data Access Component)(이전의 MDAC(Microsoft Data Access Component))의 기능을 제공할 뿐만 아니라 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능을 제공하는 다른 여러 기능도 구현합니다.  
  
## <a name="in-this-section"></a>섹션 내용    
 [데이터베이스 미러링 사용](../../oledb/features/using-database-mirroring.md)  
 SQL Server용 OLE DB 드라이버가 미러된 데이터베이스의 사용을 지원하는 방법을 설명합니다. 미러된 데이터베이스는 대기 서버의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 복사본, 즉 미러를 보관하는 기능입니다.  
  
 [비동기 작업 수행](../../oledb/features/performing-asynchronous-operations.md)  
 SQL Server용 OLE DB 드라이버가 비동기 작업을 지원하는 방법을 설명합니다. 비동기 작업은 호출 스레드를 차단하지 않고 즉시 반환할 수 있는 기능입니다.  

[Azure Active Directory 사용](using-azure-active-directory.md)  
보다 안전한 기본 설정을 제공하고 페더레이션 ID를 사용한 Azure SQL Database 인스턴스 연결을 허용하는 OLE DB 드라이버 18.2.1에 도입된 새로운 인증 방법에 대해 설명합니다.

 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 OLE DB Driver for SQL Server가 MARS(Multiple Active Result Set)를 지원하는 방법을 설명합니다. MARS를 사용하면 단일 데이터베이스 연결을 통해 여러 결과 집합을 실행 및 검색할 수 있습니다.  
  
 [XML 데이터 형식 사용](../../oledb/features/using-xml-data-types.md)  
 SQL Server용 OLE DB 드라이버가 XML 데이터 형식을 지원하는 방법을 설명합니다. XML 데이터 형식은 열 형식, 변수 형식, 매개 변수 형식 또는 함수 반환 형식에 사용할 수 있는 XML 기반 데이터 형식입니다.  
  
 [사용자 정의 형식 사용](../../oledb/features/using-user-defined-types.md)  
 SQL Server용 OLE DB 드라이버가 UDT(사용자 정의 형식)을 지원하는 방법을 설명합니다. UDT를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 개체 및 사용자 지정 데이터 구조에 데이터를 저장할 수 있으므로 SQL 형식 시스템이 확장됩니다.  
  
 [큰 값 형식 사용](../../oledb/features/using-large-value-types.md)  
 OLE DB Driver for SQL Server가 큰 값 데이터 형식인 LOB(Large Object) 데이터 형식을 지원하는 방법을 설명합니다.  
  
 [프로그래밍 방식으로 암호 변경](../../oledb/features/changing-passwords-programmatically.md)  
 SQL Server용 OLE DB 드라이버가 만료된 암호를 처리하는 방법을 설명합니다. 이제 관리자의 개입 없이도 클라이언트에서 암호를 변경할 수 있습니다.  
  
 [스냅샷 격리 작업](../../oledb/features/working-with-snapshot-isolation.md)  
 SQL Server용 OLE DB 드라이버가 읽기/쓰기 차단 시나리오를 방지하여 데이터베이스 성능을 개선하는 향상된 행 버전 관리 기능을 지원하는 방법을 설명합니다.  
  
 [쿼리 알림 작업](../../oledb/features/working-with-query-notifications.md)  
 OLE DB Driver for SQL Server가 행 집합 수정에 대한 소비자 알림을 지원하는 방법을 설명합니다.  
  
 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md)  
 SQL Server용 OLE DB 드라이버가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블 또는 뷰 안팎으로 다량의 데이터를 전송할 수 있는 대량 복사 작업을 지원하는 방법을 설명합니다.  
  
 [유효성 검사 없이 암호화 사용](../../oledb/features/using-encryption-without-validation.md)  
 OLE DB Driver for SQL Server를 사용하여 인증서 유효성을 검사하지 않고 서버에 전송되는 데이터를 암호화하는 방법을 설명합니다.  
  
 [테이블 반환 매개 변수&#40;SQL Server용 OLE DB 드라이버&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 OLE DB Driver for SQL Server의 테이블 반환 매개 변수 지원에 대해 설명합니다.  
  
 [큰 CLR 사용자 정의 형식](../../oledb/features/large-clr-user-defined-types.md)  
 큰 CLR(공용 언어 런타임) UDT(사용자 정의 형식)에 대한 지원을 설명합니다.  
  
 [FILESTREAM 지원](../../oledb/features/filestream-support.md)  
 OLE DB Driver for SQL Server의 향상된 FILESTREAM 기능 지원에 대해 설명합니다.  
  
 [클라이언트 연결의 서비스 사용자 이름&#40;SPN&#41; 지원](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 모든 프로토콜에서 상호 인증을 지원하기 위해 SPN(서비스 사용자 이름)이 어떻게 확장되었는지 설명합니다.  
  
 [SQL Server용 OLE DB 드라이버에서 스파스 열 지원](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 OLE DB Driver for SQL Server의 스파스 열 지원에 대해 설명합니다.  
  
 [날짜 및 시간 기능 향상](../../oledb/features/date-and-time-improvements.md)  
 OLE DB Driver for SQL Server에 추가된 날짜 및 시간 데이터 형식 지원에 대해 설명합니다.  
  
 [메타데이터 검색](../../oledb/features/metadata-discovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서의 메타데이터 검색 개선 사항을 설명합니다.  
  
 [SQL Server용 OLE DB 드라이버에서 UTF-16 지원](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 도입된 동작 변경 사항에 대해 설명합니다. 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공하는 경우, 종결 문자 이전에 버퍼에 작성된 **wchar** 문자가 서로게이트 쌍의 상위 서로게이트 코드 포인트인 경우 및 다음 **wchar** 문자가 하위 서로게이트 코드 포인트인 경우 SQL Server용 OLE DB 드라이버에서 상위 서로게이트 코드 포인트를 버퍼에 추가하지 않습니다.  
 
 [SQL Server용 OLE DB 드라이버에서 UTF-8 지원](../../oledb/features/utf-8-support-in-oledb-driver-for-sql-server.md)  
 UTF-8로 인코딩된 데이터로 작업할 때 사용자가 수행해야 하는 UTF-8 서버 인코딩 및 구성 주의 사항에 대해 설명합니다.
  
 [SQL Server용 OLE DB 드라이버의 고가용성, 재해 복구 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에 추가된 고가용성의 재해 복구 기능을 활용하도록 애플리케이션을 구성할 수 있는 방법을 설명합니다.  
  
 [확장 이벤트 로그의 진단 정보 액세스](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 SQL Server용 OLE DB 드라이버의 향상된 기능과, 링 버퍼 및 XEvents 로그의 진단 정보에 액세스하는 데 사용되는 데이터 추적 기능에 대해 설명합니다.  
  
 [SQL Server용 OLE DB 드라이버의 LocalDB 지원](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 OLE DB Driver for SQL Server의 LocalDB 기능 지원에 대해 설명합니다.  
  
 [투명 네트워크 IP 확인 사용](../../oledb/features/using-transparent-network-ip-resolution.md)  
 장애 조치(failover) 클러스터에서 OLE DB Driver for SQL Server가 투명 네트워크 IP 확인을 지원하는 방식을 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server용 OLE DB 드라이버](../../oledb/oledb-driver-for-sql-server.md)      
 [OLE DB 방법 도움말 항목](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [SQL Server용 OLE DB 드라이버 설치](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
