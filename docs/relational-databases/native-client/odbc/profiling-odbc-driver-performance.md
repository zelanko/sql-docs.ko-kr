---
title: ODBC 드라이버 성능 프로 파일링 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- profiling ODBC driver performance data [SQL Server Native Client]
- performance [ODBC]
- application statistics [ODBC]
- time statistics [ODBC]
- ODBC, performance data
- SQL Server Native Client ODBC driver, profiling performance data
- SQLPERF data structure
- statistical information [ODBC]
ms.assetid: 8f44e194-d556-4119-a759-4c9dec7ecead
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c15c8920d2a0188a7dbe517149dc369dea95522e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73760712"
---
# <a name="profiling-odbc-driver-performance"></a>ODBC 드라이버 성능 프로파일링
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 다음과 같은 두 가지 유형의 성능 데이터를 프로파일링할 수 있습니다.  
  
-   장기 실행 쿼리  
  
     드라이버는 지정된 시간 내에 서버로부터 응답을 받지 못한 쿼리를 로그 파일에 기록할 수 있습니다. 애플리케이션 프로그래머 또는 데이터베이스 관리자는 기록된 각 SQL 문을 연구하여 성능 향상 방법을 확인할 수 있습니다.  
  
-   드라이버 성능 데이터  
  
     드라이버는 성능 통계를 기록하여 이를 파일에 쓰거나 SQLPERF라는 드라이버별 데이터 구조를 통해 애플리케이션에 제공할 수 있습니다. 성능 통계가 포함된 파일은 탭으로 구분된 형식의 파일이므로 Microsoft Excel과 같이 탭으로 구분된 파일을 지원하는 스프레드시트를 사용하여 손쉽게 분석이 가능합니다.  
  
 두 가지 프로파일링 유형은 다음 방법으로 활성화할 수 있습니다.  
  
-   로깅을 지정하는 데이터 원본에 연결합니다.  
  
-   [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 를 호출 하 여 프로 파일링을 제어 하는 드라이버 관련 특성을 설정 합니다.  
  
 애플리케이션 프로세스는 각자 고유의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 복사본을 받으며, 프로파일링은 드라이버 복사본과 애플리케이션 프로세스의 조합에 대해 전역으로 적용됩니다. 애플리케이션의 어떤 항목이 프로파일링을 활성화하면 프로파일링은 해당 애플리케이션의 드라이버에서 활성 상태인 모든 연결에 대한 정보를 기록합니다. 명확하게 프로파일링을 요청하지 않은 연결도 포함됩니다.  
  
 드라이버가 프로파일링 로그(성능 데이터 또는 장기 실행 쿼리 로그)를 연 후 로그는 ODBC 드라이버 관리자가 드라이버를 언로드하여 애플리케이션이 드라이버에서 연 모든 환경 핸들을 해제할 때까지 닫히지 않습니다. 애플리케이션이 새 환경 핸들을 열면 드라이버의 새 복사본이 로드됩니다. 이후 애플리케이션이 동일한 로그 파일을 지정하는 데이터 원본에 연결되거나 동일한 파일에 기록하도록 드라이버별 특성을 설정하면 드라이버는 기존 로그를 덮어씁니다.  
  
 애플리케이션이 로그 파일에 프로파일링을 시작한 상태에서 두 번째 애플리케이션이 동일한 로그 파일에 프로파일링을 시작하려고 시도하면 두 번째 애플리케이션은 어떠한 프로파일링 데이터도 기록할 수 없습니다. 첫 번째 애플리케이션이 드라이버를 언로드한 후 두 번째 애플리케이션이 프로파일링을 시작하면 두 번째 애플리케이션이 첫 번째 애플리케이션의 로그 파일을 덮어씁니다.  
  
 응용 프로그램이 프로 파일링을 사용 하도록 설정 된 데이터 원본에 연결 하는 경우 응용 프로그램에서 **SQLSetConnectOption** 를 호출 하 여 로깅을 시작 하면 드라이버가 SQL_ERROR 반환 됩니다. **SQLGetDiagRec** 를 호출 하면 다음이 반환 됩니다.  
  
```  
SQLState: 01000, pfNative = 0  
ErrorMsg: [Microsoft][SQL Server Native Client]  
   An error has occurred during the attempt to access  
   the log file, logging disabled.  
```  
  
 드라이버는 환경 핸들이 닫히면 성능 데이터 수집을 중지합니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 애플리케이션에 각각 고유의 환경 핸들이 있는 여러 개의 연결이 사용되는 경우 드라이버는 관련된 환경 핸들 중 하나가 닫히면 성능 데이터 수집을 중지합니다.  
  
 드라이버의 성능 데이터는 SQLPERF 데이터 구조에 저장되거나 탭으로 구분된 파일에 기록될 수 있습니다. 데이터에는 다음 통계 범주가 포함됩니다.  
  
-   애플리케이션 프로필  
  
-   연결  
  
-   네트워크  
  
-   Time  
  
 다음 표에서 SQLPERF 데이터 구조의 필드에 대한 설명은 성능 로그 파일에 기록되는 통계에도 적용됩니다.  
  
### <a name="application-profile-statistics"></a>애플리케이션 프로필 통계  
  
|SQLPERF 필드|Description|  
|-------------------|-----------------|  
|TimerResolution|서버 클럭 시간의 최소 인식 값(밀리초)입니다. 일반적으로 0으로 보고되며, 보고된 수가 큰 경우에만 고려되어야 합니다. 서버 클럭의 최소 인식 값이 시간 기반 통계의 적정 간격보다 클 경우 해당 통계는 과장될 수 있습니다.|  
|SQLidu|SQL_PERF_START 이후의 INSERT, DELETE 또는 UPDATE 문의 수입니다.|  
|SQLiduRows|SQL_PERF_START 이후의 INSERT, DELETE 또는 UPDATE 문의 수입니다.|  
|SQLSelects|SQL_PERF_START 이후 처리된 SELECT 문의 수입니다.|  
|SQLSelectRows|SQL_PERF_START 이후에 선택된 행의 수입니다.|  
|트랜잭션|SQL_PERF_START 이후 롤백을 포함한 사용자 트랜잭션의 수입니다. ODBC 애플리케이션이 SQL_AUTOCOMMIT_ON 상태로 실행 중인 경우 각 명령은 트랜잭션으로 간주됩니다.|  
|SQLPrepares|SQL_PERF_START 후 [Sqlprepare 함수](https://go.microsoft.com/fwlink/?LinkId=59360) 호출 수입니다.|  
|ExecDirects|SQL_PERF_START 후 **Sqlexecdirect** 호출 수입니다.|  
|SQLExecutes|SQL_PERF_START 후의 **Sqlexecute** 호출 수입니다.|  
|CursorOpens|SQL_PERF_START 이후 드라이버가 서버 커서를 연 횟수입니다.|  
|CursorSize|SQL_PERF_START 이후 커서에서 연 결과 집합의 행 수입니다.|  
|CursorUsed|SQL_PERF_START 이후 커서에서 드라이버를 통해 실제로 검색된 행의 수입니다.|  
|PercentCursorUsed|CursorUsed/CursorSize와 같습니다. 예를 들어 애플리케이션에 의해 드라이버가 서버 커서를 열어 &quot;SELECT COUNT(*) FROM Authors,&quot;를 수행할 경우 SELECT 문에 대한 결과 집합의 행은 23개입니다. 그런 다음 애플리케이션이 이 행에서 3개의 행만 인출할 경우 CursorUsed/CursorSize는 3/23이 되며, 따라서 PercentCursorUsed는 13.043478이 됩니다.|  
|AvgFetchTime|SQLFetchTime/SQLFetchCount와 같습니다.|  
|AvgCursorSize|CursorSize/CursorOpens와 같습니다.|  
|AvgCursorUsed|CursorUsed/CursorOpens와 같습니다.|  
|SQLFetchTime|서버 커서에 대한 인출을 완료하는 데 소요된 누적 시간입니다.|  
|SQLFetchCount|SQL_PERF_START 이후 서버 커서에 대해 수행된 인출 횟수입니다.|  
|CurrentStmtCount|드라이버에 열린 모든 연결에 대해 현재 열려 있는 문 핸들의 수입니다.|  
|MaxOpenStmt|SQL_PERF_START 이후 동시에 열린 문 핸들의 최대 수입니다.|  
|SumOpenStmt|SQL_PERF_START 이후 열린 문 핸들의 수입니다.|  
|**연결 통계:**||  
|CurrentConnectionCount|애플리케이션이 서버에 대해 연 활성 연결 핸들의 현재 수입니다.|  
|MaxConnectionsOpened|SQL_PERF_START 이후 열린 동시 연결 핸들의 최대 수입니다.|  
|SumConnectionsOpened|SQL_PERF_START 이후 열린 연결 핸들 수의 합계입니다.|  
|SumConnectionTime|SQL_PERF_START 이후 열린 모든 연결의 시간 합계입니다. 예를 들어 애플리케이션이 10개의 연결을 열었고 각 연결을 5초 동안 유지했다면 SumConnectionTime은 50초가 됩니다.|  
|AvgTimeOpened|SumConnectionsOpened/ SumConnectionTime과 같습니다.|  
|**네트워크 통계:**||  
|ServerRndTrips|드라이버가 서버로 명령을 보내고 응답을 받은 횟수입니다.|  
|BuffersSent|SQL_PERF_START 이후 드라이버에 의해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 전송된 TDS(Tabular Data Stream) 패킷의 수입니다. 큰 명령은 여러 개의 버퍼를 점유할 수 있으므로 하나의 큰 명령이 서버로 전송되고 이 명령이 6개의 패킷을 채운다면 ServerRndTrips은 1만큼 증가하고 BuffersSent는 6만큼 증가합니다.|  
|BuffersRec|애플리케이션이 드라이버를 사용하여 시작된 후 드라이버가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로부터 받은 TDS 패킷의 수입니다.|  
|BytesSent|애플리케이션이 드라이버를 사용하여 시작된 후 TDS 패킷으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 전송된 데이터의 바이트 수입니다.|  
|BytesRec|애플리케이션이 드라이버를 사용하여 시작된 후 드라이버가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로부터 받은 TDS 패킷의 데이터 바이트 수입니다.|  
  
### <a name="time-statistics"></a>시간 통계  
  
|SQLPERF 필드|Description|  
|-------------------|-----------------|  
|msExecutionTime|SQL_PERF_START 이후 드라이버가 처리를 위해 소요한 누적 시간으로, 서버의 응답을 대기하는 데 보낸 시간도 포함됩니다.|  
|msNetworkServerTime|드라이버가 서버의 응답을 대기하는 데 보낸 누적 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [ODBC 드라이버 성능 프로 파일링 방법 항목 ODBC&#41;&#40;](../../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)  
  
  
