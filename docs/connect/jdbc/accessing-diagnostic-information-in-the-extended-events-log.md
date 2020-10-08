---
title: 확장 이벤트 로그의 진단 정보 액세스
description: SQL Server용 Microsoft JDBC 드라이버의 이벤트와 관련된 서버의 확장 이벤트에 액세스하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d9b75ea8c722ca753e831811226b8128df15266
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725509"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>확장 이벤트 로그의 진단 정보 액세스
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]에서 추적([드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md))이 업데이트되어 서버의 연결 링 버퍼와 확장 이벤트 로그의 애플리케이션 성능 정보에서 클라이언트 이벤트와 진단 정보(예: 연결 실패)의 상관관계를 손쉽게 지정할 수 있게 되었습니다. 확장 이벤트 로그를 읽는 방법에 대한 자세한 내용은 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)를 참조하세요.  
  
## <a name="details"></a>세부 정보  
 연결 작업의 경우 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서 클라이언트 연결 ID를 전송합니다. 연결이 실패하는 경우 연결 링 버퍼에 액세스할 수 있으며([연결 링 버퍼가 있는 SQL Server 2008의 연결 문제 해결](/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer)) **ClientConnectionID** 필드를 찾아서 연결 실패에 대한 진단 정보를 얻을 수 있습니다. 클라이언트 연결 ID는 오류가 발생하는 경우에만 링 버퍼에 기록됩니다. 로그인 전 패킷을 전송하기 전에 연결이 실패하는 경우 클라이언트 연결 ID는 생성되지 않습니다. 클라이언트 연결 ID는 16바이트 GUID입니다. 확장 이벤트 세션에서 **client_connection_id** 동작을 이벤트에 추가한 경우 확장 이벤트 대상 출력에서 클라이언트 연결 ID를 찾을 수도 있습니다. 클라이언트 드라이버 진단 추가 지원이 필요한 경우 추적을 사용하도록 설정하고 연결 명령을 다시 실행하여 추적에 있는 **ClientConnectionID** 필드를 관찰할 수 있습니다.  
  
 [ISQLServerConnection 인터페이스](../../connect/jdbc/reference/isqlserverconnection-interface.md)를 사용하여 클라이언트 연결 ID를 프로그래밍 방식으로 가져올 수 있습니다. 연결 ID는 연결 관련 예외에서도 표시됩니다.  
  
 연결 오류가 발생하는 경우 서버의 BID(기본 제공 진단) 추적 정보 및 연결 링 버퍼에 있는 클라이언트 연결 ID를 사용하여 클라이언트 연결과 서버 연결의 상관관계를 지정할 수 있습니다. 서버의 BID 추적에 대한 자세한 내용은 [데이터 액세스 추적](/previous-versions/sql/sql-server-2008/cc765421(v=sql.100))을 참조하세요. 데이터 액세스 추적 문서에는 데이터 액세스 추적에 대한 정보도 포함되어 있습니다. 이 정보는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에 적용되지 않습니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]을(를) 사용하여 데이터 액세스 추적을 수행하는 방법에 대한 자세한 내용은 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)을 참조하세요.  
  
 JDBC 드라이버는 또한 스레드별 작업 ID를 전송합니다. TRACK_CAUSAILITY 옵션이 활성화된 상태에서 세션을 시작한 경우 작업 ID는 확장 이벤트 세션에서 캡처됩니다. 활성 연결의 성능 문제를 위해 클라이언트의 추적(ActivityID 필드)에서 작업 ID를 가져온 다음 확장 이벤트 출력에 작업 ID를 배치할 수 있습니다. 확장 이벤트의 작업 ID는 16바이트 GUID(클라이언트 연결 ID의 GUID와 같지 않음)에 4바이트 시퀀스 번호가 추가된 형식입니다. 시퀀스 번호는 스레드 내 요청의 순서를 나타냅니다. ActivityId는 SQL 배치 문과 RPC 요청을 위해 전송됩니다. ActivityId가 서버로 전송되도록 하려면 먼저 Logging.Properties 파일에 다음 키-값 쌍을 지정해야 합니다.  
  
```
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 값이 `on`(대/소문자 구분)이 아닌 경우 ActivityId를 전송할 수 없습니다.  
  
 자세한 내용은 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)을 참조하세요. 이 추적 플래그는 해당 JDBC 개체 로거와 함께 사용되어 JDBC 드라이버의 ActivityId를 추적하고 전송할지 여부를 결정합니다. Logging.Properties 파일 업데이트 외에 com.microsoft.sqlserver.jdbc 로거를 FINER 이상으로 설정해야 합니다. 특정 클래스에서 생성된 요청에 대해 ActivityId를 서버로 전송하려는 경우 해당 클래스 로거는 FINER 또는 FINEST로 설정되어야 합니다. 예를 들어, 클래스가 SQLServerStatement인 경우 com.microsoft.sqlserver.jdbc.SQLServerStatement 로거를 설정해야 합니다.  
  
 다음 샘플에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 링 버퍼에 저장되고 RPC 및 일괄 처리 작업 시 클라이언트에서 전송된 작업 ID를 기록하는 확장 이벤트 세션을 시작합니다.  
  
```sql
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)