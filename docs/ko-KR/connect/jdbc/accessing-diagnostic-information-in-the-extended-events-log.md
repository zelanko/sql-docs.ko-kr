---
title: 확장된 이벤트 로그의 진단 정보 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a79e9468-2257-4536-91f1-73b008c376c3
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0695988b46ab28e47d2e6cdaa27ecac2b9daecb7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>확장 이벤트 로그의 진단 정보 액세스
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  에 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]추적 ([드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)) 쉽게 클라이언트 이벤트 간의 상관 관계와 서버의 연결 링에서 연결 실패 등의 진단 정보를 보다 쉽게 하도록 업데이트 되었습니다 확장된 이벤트 로그의 버퍼 및 응용 프로그램 성능 정보입니다. 확장 이벤트 로그를 읽는 방법에 대한 자세한 내용은 [View Event Session Data](http://msdn.microsoft.com/library/hh710068(SQL.110).aspx)를 참조하십시오.  
  
## <a name="details"></a>세부 정보  
 연결 작업에는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 클라이언트 보낼 연결 id입니다. 연결이 실패하는 경우 연결 링 버퍼에 액세스할 수 있으며([연결 링 버퍼가 있는 SQL Server 2008의 연결 문제 해결](http://go.microsoft.com/fwlink/?LinkId=207752)) **ClientConnectionID** 필드를 찾아서 연결 실패에 대한 진단 정보를 얻을 수 있습니다. 클라이언트 연결 ID는 오류가 발생하는 경우에만 링 버퍼에 기록됩니다. 로그인 전 패킷을 전송하기 전에 연결이 실패하는 경우 클라이언트 연결 ID는 생성되지 않습니다. 클라이언트 연결 ID는 16바이트 GUID입니다. 클라이언트 연결을 찾을 수 있습니다 하는 경우 확장된 이벤트 대상 출력에서 ID는 **client_connection_id** 동작이 확장된 이벤트 세션의 이벤트에 추가 됩니다. 추적을 설정 하 고 연결 명령을 다시 실행 하는 관찰의 **ClientConnectionID** 있습니다 클라이언트 드라이버 진단 추가 지원이 필요한 경우 추적에 있는 필드입니다.  
  
 클라이언트를 얻을 수 있습니다를 사용 하 여 프로그래밍 방식으로 연결 ID [ISQLServerConnection 인터페이스](../../connect/jdbc/reference/isqlserverconnection-interface.md)합니다. 연결 ID는 연결 관련 예외에서도 표시됩니다.  
  
 연결 오류가 발생하는 경우 서버의 BID 추적 정보 및 연결 링 버퍼에 있는 클라이언트 연결 ID를 사용하여 클라이언트 연결을 서버에서의 연결로 상관 관계를 지정할 수 있습니다. 서버에서 BID에 대 한 자세한 내용은 레코더 추적은 참조 [데이터 액세스 추적](http://go.microsoft.com/fwlink/?LinkId=125805)합니다. 참고에 적용 되지 않는 데이터 액세스 추적 수행에 대 한 정보를도 포함 하는 데이터 액세스 추적 아티클에 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]; 참조 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md) 사용 하 여 데이터 액세스 추적에 대 한 내용은 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 JDBC 드라이버는 또한 스레드별 작업 ID를 전송합니다. TRACK_CAUSAILITY 옵션이 활성화된 상태에서 세션을 시작한 경우 작업 ID는 확장 이벤트 세션에서 캡처됩니다. 활성 연결의 성능 문제를 위해 클라이언트의 추적(ActivityID 필드)에서 작업 ID를 가져온 다음 확장 이벤트 출력에 작업 ID를 배치할 수 있습니다. 확장 이벤트의 작업 ID는 16바이트 GUID(클라이언트 연결 ID의 GUID와 같지 않음)에 4바이트 시퀀스 번호가 추가된 형식입니다. 시퀀스 번호는 스레드 내 요청의 순서를 나타냅니다. ActivityId는 SQL 배치 문과 RPC 요청을 위해 전송됩니다. ActivityId가 서버로 전송되도록 하려면 먼저 Logging.Properties 파일에 다음 키-값 쌍을 지정해야 합니다.  
  
```  
com.microsoft.sqlserver.jdbc.traceactivity = on  
```  
  
 이외의 모든 값 `on` (대/소문자 구분) ActivityId 보내는 사용할 수 없게 됩니다.  
  
 자세한 내용은 참조 [드라이버 작업 추적](../../connect/jdbc/tracing-driver-operation.md)합니다. 이 추적 플래그는 해당 JDBC 개체 로거와 함께 사용되어 JDBC 드라이버의 ActivityId를 추적하고 전송할지 여부를 결정합니다. Logging.Properties 파일 업데이트 외에 com.microsoft.sqlserver.jdbc 로거를 FINER 이상으로 설정해야 합니다. 특정 클래스에서 생성된 요청에 대해 ActivityId를 서버로 전송하려는 경우 해당 클래스 로거는 FINER 또는 FINEST로 설정되어야 합니다. 예를 들어, 클래스가 SQLServerStatement인 경우 com.microsoft.sqlserver.jdbc.SQLServerStatement 로거를 설정해야 합니다.  
  
 다음은 사용 하는 샘플 [!INCLUDE[tsql](../../includes/tsql_md.md)] RPC 및 일괄 처리 작업 시 클라이언트에서 보낸 링 버퍼에 저장 되 고 활동 ID를 기록 하는 확장된 이벤트 세션을 시작 하려면:  
  
```  
create event session MySession on server  
add event connectivity_ring_buffer_recorded,  
add event sql_statement_starting (action (client_connection_id)),  
add event sql_statement_completed (action (client_connection_id)),  
add event rpc_starting (action (client_connection_id)),  
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
