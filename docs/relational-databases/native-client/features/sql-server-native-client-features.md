---
title: SQL Server Native Client 기능 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2bf0766c2a9d90bc49189b4e99b208173709669e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744405"
---
# <a name="sql-server-native-client-features"></a>SQL Server Native Client 기능
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 WDAC(Windows Data Access Component)(이전의 MDAC(Microsoft Data Access Component))의 기능을 제공할 뿐만 아니라 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능을 제공하는 다른 여러 기능도 구현합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [문자 변환을 처리 시 ODBC 드라이버 동작 변경](../../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client부터 변경된 동작에 대해 설명합니다.  
  
 [데이터베이스 미러링 사용](../../../relational-databases/native-client/features/using-database-mirroring.md)  
 에 대해 설명 하는 방법 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 미러된 데이터베이스의 복사본, 즉 미러를 보관 하는 기능 사용을 지 원하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대기 서버의 데이터베이스입니다.  
  
 [비동기 작업 수행](../../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 비동기 작업을 지원하는 방법을 설명합니다. 비동기 작업은 호출 스레드를 차단하지 않고 즉시 반환할 수 있는 기능입니다.  
  
 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 MARS(Multiple Active Result Sets)를 지원하는 방법을 설명합니다. MARS를 사용하면 단일 데이터베이스 연결을 통해 여러 결과 집합을 실행 및 검색할 수 있습니다.  
  
 [XML 데이터 형식 사용](../../../relational-databases/native-client/features/using-xml-data-types.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 XML 데이터 형식을 지원하는 방법을 설명합니다. XML 데이터 형식은 열 형식, 변수 형식, 매개 변수 형식 또는 함수 반환 형식에 사용할 수 있는 XML 기반 데이터 형식입니다.  
  
 [사용자 정의 형식 사용](../../../relational-databases/native-client/features/using-user-defined-types.md)  
 에 대해 설명 하는 방법 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 사용자 정의 형식 (UDT), 개체 및 사용자 지정 데이터 구조에 저장할 수 있으므로 SQL 형식 시스템이 확장을 지원 한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스.  
  
 [큰 값 형식 사용](../../../relational-databases/native-client/features/using-large-value-types.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 큰 값 데이터 형식인 LOB(Large Object) 데이터 형식을 지원하는 방법을 설명합니다.  
  
 [프로그래밍 방식으로 암호 변경](../../../relational-databases/native-client/features/changing-passwords-programmatically.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 만료된 암호를 처리하는 방법을 설명합니다. 이제 관리자의 개입 없이도 클라이언트에서 암호를 변경할 수 있습니다.  
  
 [스냅숏 격리 작업](../../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 읽기/쓰기 차단 시나리오를 방지하여 데이터베이스 성능을 개선하는 향상된 행 버전 관리 기능을 지원하는 방법을 설명합니다.  
  
 [쿼리 알림 작업](../../../relational-databases/native-client/features/working-with-query-notifications.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 행 집합 수정에 대한 소비자 알림을 지원하는 방법을 설명합니다.  
  
 [대량 복사 작업 수행](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
 에 대해 설명 하는 방법 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 지원 안이나 밖으로 많은 양의 데이터 전송할 수 있는 대량 복사 작업을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블 또는 뷰.  
  
 [유효성 검사 없이 암호화 사용](../../../relational-databases/native-client/features/using-encryption-without-validation.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하여 인증서 유효성을 검사하지 않고 서버에 전송된 데이터를 암호화하는 방법을 설명합니다.  
  
 [테이블 반환 매개 변수 &#40;SQL Server Native Client&#41;](../../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
 테이블 반환 매개 변수에 대한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 지원을 설명합니다.  
  
 [큰 CLR 사용자 정의 형식](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
 큰 CLR(공용 언어 런타임) UDT(사용자 정의 형식)에 대한 지원을 설명합니다.  
  
 [FILESTREAM 지원](../../../relational-databases/native-client/features/filestream-support.md)  
 설명 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 향상된 된 FILESTREAM 기능에 대 한 네이티브 클라이언트 지원 합니다.  
  
 [클라이언트 연결의 서비스 사용자 이름&#40;SPN&#41; 지원](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
 모든 프로토콜에서 상호 인증을 지원하기 위해 SPN(서비스 사용자 이름)이 어떻게 확장되었는지 설명합니다.  
  
 [SQL Server Native Client의 스파스 열 지원](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 스파스 열을 어떻게 지원하는지 설명합니다.  
  
 [날짜 및 시간 기능 향상](../../../relational-databases/native-client/features/date-and-time-improvements.md)  
 날짜 및 시간 데이터 형식을 지원하기 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에 추가된 기능을 설명합니다.  
  
 [메타데이터 검색](../../../relational-databases/native-client/features/metadata-discovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서의 메타데이터 검색 개선 사항을 설명합니다.  
  
 [SQL Server Native Client 11.0의 UTF-16 지원](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 도입된 동작 변경 사항에 대해 설명합니다. 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공 하는 경우는 **wchar** 종결 문자는 서로게이트 쌍의 상위 서로게이트 코드 포인트를 전과 경우 버퍼에 기록 된 문자 다음 **wchar** 문자가 하위 서로게이트 코드 포인트에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 상위 서로게이트 코드 포인트인 버퍼에 추가 되지 않습니다.  
  
 [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에 추가된 고가용성의 재해 복구 기능을 활용하도록 애플리케이션을 구성할 수 있는 방법을 설명합니다.  
  
 [확장 이벤트 로그의 진단 정보 액세스](../../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 향상된 기능과, 링 버퍼 및 XEvents 로그의 진단 정보에 액세스하는 데 사용되는 데이터 추적 기능에 대해 설명합니다.  
  
 [LocalDB에 대한 SQL Server Native Client 지원](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 지원하는 LocalDB 기능을 설명합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC 방법 도움말 항목](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB 방법 도움말 항목](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [SQL Server Native Client 설치](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
