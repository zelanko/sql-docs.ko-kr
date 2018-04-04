---
title: SQL Server 기능에 대 한 OLE DB 드라이버 | Microsoft Docs
description: OLE DB Driver SQL Server 기능에 대 한
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], features
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bda748c764d49044a76638ebd2e87a6d831ae66f
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server-features"></a>OLE DB Driver for SQL Server 기능
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Windows (이전의 Microsoft) 데이터 액세스 구성 요소 (WDAC)의 기능을 노출할 뿐 아니라 OLE DB Driver for SQL Server도 다른 여러 기능도 구현 노출 하도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능입니다.  
  
## <a name="in-this-section"></a>섹션 내용    
 [데이터베이스 미러링 사용](../../oledb/features/using-database-mirroring.md)  
 OLE DB Driver for SQL Server의 한 복사, 즉 미러를 보관 하는 기능 미러된 데이터베이스의 사용을 지 원하는 방법에 대해 설명 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대기 서버에는 데이터베이스입니다.  
  
 [비동기 작업 수행](../../oledb/features/performing-asynchronous-operations.md)  
 OLE DB Driver for SQL Server에서 지 원하는 방법 비동기 작업 호출 스레드를 차단 하지 않고 즉시 반환할 수 있는 방법을 설명 합니다.  
  
 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../oledb/features/using-multiple-active-result-sets-mars.md)  
 OLE DB Driver for SQL Server에서 여러 활성 결과 집합 MARS ()를 지 원하는 방법에 대해 설명 합니다. MARS를 사용하면 단일 데이터베이스 연결을 통해 여러 결과 집합을 실행 및 검색할 수 있습니다.  
  
 [XML 데이터 형식 사용](../../oledb/features/using-xml-data-types.md)  
 OLE DB Driver for SQL Server 열 형식, 변수 형식, 매개 변수 형식 또는 함수 반환 형식으로 사용할 수 있는 XML 기반 데이터 형식이 XML 데이터 형식에서 지 원하는 방법에 대해 설명 합니다.  
  
 [사용자 정의 형식 사용](../../oledb/features/using-user-defined-types.md)  
 OLE DB Driver for SQL Server 사용자 정의 형식 (UDT) 개체 및 사용자 지정 데이터 구조에 저장할 수 있으므로 SQL 형식 시스템이 확장을 지 원하는 방법에 대해 설명 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
 [큰 값 형식 사용](../../oledb/features/using-large-value-types.md)  
 OLE DB Driver for SQL Server는 큰 개체 데이터 형식인 lob (기간 업무)는 큰 값 데이터 형식에서 지 원하는 방법에 대해 설명 합니다.  
  
 [프로그래밍 방식으로 암호 변경](../../oledb/features/changing-passwords-programmatically.md)  
 이제 관리자의 개입 없이도 클라이언트에서 암호를 변경할 수 있도록 OLE DB Driver for SQL Server 암호 만료 처리 하는 방법을 설명 합니다.  
  
 [스냅숏 격리 작업](../../oledb/features/working-with-snapshot-isolation.md)  
 OLE DB Driver for SQL Server 읽기 / 쓰기 차단 시나리오를 방지 하 여 데이터베이스 성능을 개선 하는 행 버전 관리 기능을 지 원하는 방법을 설명 합니다.  
  
 [쿼리 알림 작업](../../oledb/features/working-with-query-notifications.md)  
 OLE DB Driver for SQL Server 소비자 알림을 행 집합 수정에 지원 하는 방법을 설명 합니다.  
  
 [대량 복사 작업 수행](../../oledb/features/performing-bulk-copy-operations.md)  
 OLE DB Driver for SQL Server 안이나 밖으로 많은 양의 데이터 전송할 수 있는 대량 복사 작업을 지 원하는 방법에 대해 설명 된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블 또는 뷰.  
  
 [유효성 검사 없이 암호화 사용](../../oledb/features/using-encryption-without-validation.md)  
 OLE DB Driver for SQL Server를 사용 하 여 인증서 유효성을 검사 하지 않고 서버에 전송 하는 데이터를 암호화 하는 방법을 설명 합니다.  
  
 [테이블 반환 매개 변수 &#40;OLE DB Driver for SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md)  
 테이블 반환 매개 변수에 대 한 SQL Server 지원에 대 한 OLE DB Driver를 설명합니다.  
  
 [큰 CLR 사용자 정의 형식](../../oledb/features/large-clr-user-defined-types.md)  
 큰 CLR(공용 언어 런타임) UDT(사용자 정의 형식)에 대한 지원을 설명합니다.  
  
 [FILESTREAM 지원](../../oledb/features/filestream-support.md)  
 향상된 된 FILESTREAM 기능에 대 한 SQL Server 지원에 대 한 OLE DB Driver를 설명합니다.  
  
 [서비스 사용자 이름 &#40;SPN&#41; 클라이언트 연결의 지원](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)  
 모든 프로토콜에서 상호 인증을 지원하기 위해 SPN(서비스 사용자 이름)이 어떻게 확장되었는지 설명합니다.  
  
 [SQL Server 용 OLE DB 드라이버에서 스파스 열 지원](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md)  
 스파스 열에 대 한 SQL Server 지원에 대 한 OLE DB Driver를 설명합니다.  
  
 [날짜 및 시간 기능 향상](../../oledb/features/date-and-time-improvements.md)  
 날짜 및 시간 데이터 형식에 대 한 SQL Server 용 OLE DB Driver에 추가 지원을 설명 합니다.  
  
 [메타데이터 검색](../../oledb/features/metadata-discovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서의 메타데이터 검색 개선 사항을 설명합니다.  
  
 [SQL Server 용 OLE DB 드라이버의 utf-16 지원](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 도입된 동작 변경 사항에 대해 설명합니다. 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공 하는 경우는 **wchar** 문자 버퍼에 기록 하는 경우 및 종결 문자에 서로게이트 쌍의 상위 서로게이트 코드 포인트 크기를 다음 **wchar** 문자 하위 서로게이트 코드 포인트는, OLE DB Driver for SQL Server 버퍼를 상위 서로게이트 코드 포인트를 추가 하지 것입니다.  
  
 [OLE DB Driver for SQL Server Support for High Availability, Disaster Recovery](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
 고가용성, 재해 복구에 추가 된 기능을 활용 하도록 응용 프로그램을 구성할 수 있는 방법을 설명 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]합니다.  
  
 [확장 이벤트 로그의 진단 정보 액세스](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 SQL Server 및 링 버퍼 및 XEvents 로그의 진단 정보에 액세스할 수 있는 데이터 추적에 대 한 향상 된 OLE DB 드라이버 기능에 설명 합니다.  
  
 [SQL Server Support for LocalDB에 대 한 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  
 SQL Server에서 지 원하는 LocalDB 기능에 대 한 OLE DB Driver를 설명합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 프로그래밍에 대 한 OLE DB 드라이버](../../oledb/oledb-driver-for-sql-server-programming.md)      
 [OLE DB 방법 도움말 항목](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)   
 [OLE DB Driver for SQL Server 설치](../../oledb/applications/installing-oledb-driver-for-sql-server.md)  
  
  
