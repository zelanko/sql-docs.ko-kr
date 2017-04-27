---
title: "Database Suspect Data Page 이벤트 클래스 | Microsoft 문서"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 404b8a88ae9523573df9eab15f27357a0a494027
ms.lasthandoff: 04/11/2017

---
# <a name="database-suspect-data-page-event-class"></a>Database Suspect Data Page 이벤트 클래스
  **Database Suspect Data Page** 이벤트 클래스는 [msdb](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 의 [suspect_pages](../../relational-databases/databases/msdb-database.md)테이블에 페이지가 추가되었음을 나타냅니다. 주의 대상 페이지의 발생을 모니터링하는 추적에 이 이벤트 클래스를 포함합니다.  
  
> [!NOTE]  
>  이 이벤트는 해당 행을 **suspect_pages** 테이블에 삽입하면 비동기적으로 생성됩니다. 따라서 이 이벤트를 수신하는 작업이 해당 **suspect_pages** 항목을 바로 찾지 못할 수 있습니다.  
  
 **Database Suspect Data Page** 이벤트 클래스가 추적에 포함되면 상대적인 오버헤드가 줄어듭니다. 디스크 드라이브에 문제가 있는 경우처럼 주의 대상 페이지의 수가 늘어나면 오버헤드가 커질 수 있습니다.  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Database Suspect Data Page 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|주의 대상 페이지 이벤트가 발생한 데이터베이스의 ID입니다. 이 ID는 **suspect_pages** 테이블의 **database_id** 열과 같습니다.|3|예|  
|**EventClass**|**int**|이벤트 유형이 213입니다.|27|아니요|  
|**EventSequence**|**int**|일괄 처리 내의 이벤트 클래스 순서입니다.|51|아니요|  
|**SPID**|**int**|주의 대상 페이지가 발생한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 태스크의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 발생한 시간입니다.|14|예|  
|**Exchange Spill**|**int**|주의 대상 페이지가 포함된 데이터베이스 파일의 ID입니다. 이 ID는 **suspect_pages** 테이블의 **file_id** 열과 같습니다.|22|예|  
|**ObjectID2**|**int**|파일 내 주의 대상 페이지의 ID입니다. 이 ID는 **suspect_pages** 테이블의 **page_id** 열과 같습니다.|56|예|  
|**오류**|**int**|발생한 오류 유형입니다. 이 값은 **suspect_pages** 테이블의 페이지에 대한 **event_type** 값과 같습니다.|31|예|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [suspect_pages 테이블 관리&#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
