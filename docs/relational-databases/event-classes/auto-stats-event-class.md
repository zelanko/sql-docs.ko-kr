제목: "Auto Stats 이벤트 클래스 | Microsoft Docs" ms.custom: "" ms.date: "03/14/2017" ms.prod: sql ms.prod_service: "database-engine, sql-database" ms.component: "event-classes" ms.reviewer: "" ms.suite: "sql" ms.technology: 
  - "database-engine" ms.tgt_pltfrm: "" ms.topic: conceptual helpviewer_keywords: 
  - "Auto Stats event class" ms.assetid: cd613fce-01e1-4d8f-86cc-7ffbf0759f9e caps.latest.revision: 34 author: "stevestein" ms.author: "sstein" manager: craigg
---
# <a name="auto-stats-event-class"></a>Auto Stats 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Auto Stats** 이벤트 클래스는 인덱스 및 열 통계가 자동으로 업데이트되었음을 나타냅니다.  **Auto Stats**는 통계가 최적화 프로그램에서 사용하기 위해 로드되는 경우에 발생합니다.
  
## <a name="auto-stats-event-class-data-columns"></a>Auto Stats 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|**ClientProcessID**|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나 지정된 인스턴스에 대해 USE *database* 문이 실행되지 않은 경우 기본 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|**기간**|**bigint**|이벤트에 의해 사용된 시간(마이크로초)입니다.|13|예|  
|**EndTime**|**datetime**|이벤트가 종료된 시간입니다.|15|예|  
|**오류**|**int**|지정된 이벤트의 오류 번호입니다. 종종 **sys.messages** 카탈로그 뷰에 저장된 오류 번호를 나타냅니다.|31|예|  
|**EventClass**|**int**|이벤트 유형 = 58|27|아니오|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|**EventSubClass**|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1: 통계가 동기적으로 생성/업데이트되었습니다. **TextData** 열은 생성 또는 업데이트된 통계와 각 통계의 생성 또는 업데이트 여부를 나타냅니다.<br /><br /> 2: 비동기 통계 업데이트입니다. 작업이 지연되었습니다.<br /><br /> 3: 비동기 통계 업데이트입니다. 작업이 시작되었습니다.<br /><br /> 4: 비동기 통계 업데이트입니다. 작업이 완료되었습니다.|21|예|  
|**GroupID**|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IndexID**|**int**|이벤트에 의해 영향 받는 개체의 인덱스/통계 항목 ID입니다. 개체의 인덱스 ID를 확인하려면 **sys.indexes** 카탈로그 뷰의 **index_id** 열을 사용합니다.|24|예|  
|**IntegerData**|**int**|업데이트된 통계 컬렉션의 수입니다.|25|예|  
|**IntegerData2**|**int**|작업 시퀀스 번호입니다.|55|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 Windows 로그인 자격 증명 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 로그인)입니다.|11|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|**Exchange Spill**|**int**|시스템이 할당한 개체의 ID입니다.|22|예|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니오|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**성공**|**int**|0 = 오류<br /><br /> 1 = 성공,<br /><br /> 2 = 서버 스로틀로 인해 건너뜀(MSDE)|23|예|  
|**TextData**|**ntext**|이 열의 내용은 통계가 동기적으로 업데이트되는지(**EventSubClass** 1) 또는 비동기적으로 업데이트되는지(**EventSubClass** 2, 3 또는 4)에 따라 결정됩니다.<br /><br /> 1: 업데이트/생성된 통계를 나열합니다.<br /><br /> 2, 3 또는 4: NULL입니다. **IndexID** 열에 업데이트된 통계의 인덱스/통계 ID가 채워집니다.|1|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|**형식**|**int**|작업 유형입니다.|57|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
