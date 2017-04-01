---
title: "QN:Parameter Table 이벤트 클래스 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "이벤트 클래스 [SQL Server], QN:Parameter Table"
ms.assetid: 292da1ed-4c7e-4bd2-9b84-b9ee09917724
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 21
---
# QN:Parameter Table 이벤트 클래스
  QN:Parameter table 이벤트는 매개 변수 테이블에 대한 참조 수를 만들고 보관하며 매개 변수 정보를 저장하는 내부 테이블을 삭제하는 데 필요한 작업에 대한 정보를 보고합니다. 이 이벤트는 또한 매개 변수 테이블에 대한 사용 개수를 다시 설정하기 위한 내부 작업도 보고합니다.  
  
## QN:Parameter table 이벤트 클래스 데이터 열  
  
|데이터 열|유형|설명|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database*문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|EventClass|**정수**|이벤트 유형 = 200|27|아니요|  
|EventSequence|**int**|이 이벤트의 시퀀스 번호입니다.|51|아니요|  
|EventSubClass|**nvarchar**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 이 열에는 다음 값이 포함될 수 있습니다.<br /><br /> **테이블 생성됨**: 매개 변수 테이블이 데이터베이스에 생성되었음을 나타냅니다.<br /><br /> **테이블 삭제 시도**: 데이터베이스에서 사용하지 않는 매개 변수 테이블을 자동으로 삭제하여 리소스를 늘리려고 했음을 나타냅니다.<br /><br /> **테이블 삭제 시도 실패**: 데이터베이스에서 사용하지 않는 매개 변수 테이블을 삭제하려고 했지만 실패했음을 나타냅니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 자동으로 매개 변수 테이블 삭제 일정을 다시 조정하여 리소스를 늘립니다.<br /><br /> **테이블 삭제됨**: 데이터베이스에서 성공적으로 매개 변수 테이블을 삭제했음을 나타냅니다.<br /><br /> **테이블 고정됨**: 내부 처리에서 매개 변수 테이블을 현재 사용으로 표시했음을 나타냅니다.<br /><br /> **테이블 고정 해제됨**: 매개 변수 테이블이 고정 해제되었음을 나타냅니다. 내부 처리에서 테이블 사용을 마쳤습니다.<br /><br /> **증가한 사용자 수**: 매개 변수 테이블을 참조하는 쿼리 알림 구독 수가 증가했음을 나타냅니다.<br /><br /> **감소한 사용자 수**: 매개 변수 테이블을 참조하는 쿼리 알림 구독 수가 감소했음을 나타냅니다.<br /><br /> **LRU 카운터 다시 설정**: 매개 변수 테이블에 대한 사용 수가 다시 설정되었음을 나타냅니다.<br /><br /> **정리 작업 시작됨**: 이 매개 변수 테이블의 모든 구독 정리가 시작되었음을 나타냅니다. 이 이벤트는 데이터베이스가 시작될 때나 이 매개 변수 테이블 구독의 기반이 되는 테이블이 삭제되었을 때 발생합니다.<br /><br /> **정리 작업 완료됨**: 이 매개 변수 테이블의 모든 구독 정리를 마쳤음을 나타냅니다.|21|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> 0 = 사용자<br /><br /> 1 = 시스템|60|아니요|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 *DOMAIN*\\*Username* 형식의 Windows 로그인 자격 증명 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 로그인입니다.|11|아니요|  
|LoginSID|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|RequestID|**int**|문을 포함하는 요청의 식별자입니다.|49|예|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 응용 프로그램이 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하고 Login2로 문을 실행하는 경우 SessionLoginName은 "Login1"을 표시하고 LoginName은 "Login2"를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|이 이벤트에 해당하는 정보가 포함된 XML 문서를 반환합니다. 이 문서는 [SQL Server 쿼리 알림 프로파일러 이벤트 스키마](http://go.microsoft.com/fwlink/?LinkId=63331) 페이지에서 사용할 수 있는 XML 스키마를 따릅니다.|1|예|  
  
  