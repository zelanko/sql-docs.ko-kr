---
title: 이벤트 파일 대상을 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- event file target
- file target [SQL Server extended events]
- targets [SQL Server extended events], file target
ms.assetid: 4f0ee6ec-a0a8-4c38-aa61-8293ab6ac7fd
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d943983e7cf8f5246aa6ef07449dc0b459a8f4b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089621"
---
# <a name="event-file-target"></a>Event File Target
  이벤트 파일 대상은 전체 버퍼를 디스크에 기록하는 대상입니다.  
  
 다음 표에서는 이벤트 파일 대상을 구성하는 데 사용할 수 있는 옵션에 대해 설명합니다.  
  
|옵션|허용된 값|Description|  
|------------|--------------------|-----------------|  
|filename|최대 260자까지의 모든 문자열. 이 값은 필수 사항입니다.|파일 위치 및 파일 이름입니다.<br /><br /> 원하는 파일 확장명을 사용할 수 있습니다.|  
|max_file_size|64비트 정수. 이 값은 선택 사항입니다.|최대 파일 크기(MB)입니다. max_file_size가 지정되지 않은 경우 파일 크기는 디스크가 꽉 찰 때까지 증가합니다. 기본 파일 크기는 1GB입니다.<br /><br /> max_file_size는 세션 버퍼의 현재 크기보다 커야 합니다. 그렇지 않으면 파일 대상은 초기화에 실패하고 max_file_size가 잘못되었다고 보고합니다. 버퍼의 현재 크기를 보려면 [sys.dm_xe_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql) 동적 관리 뷰의 buffer_size 열을 쿼리합니다.<br /><br /> 기본 파일 크기가 세션 버퍼 크기보다 작으면 max_file_size를 [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) 카탈로그 뷰의 max_memory 열에 지정된 값으로 설정하는 것이 좋습니다.<br /><br /> max_file_size가 세션 버퍼보다 크게 설정된 경우 세션 버퍼 크기의 배수 중에서 가장 가까운 값으로 반내림될 수 있습니다. 그러면 지정된 max_file_size 값보다 작은 대상 파일이 생성될 수 있습니다. 예를 들어 버퍼 크기가 100MB이고 max_file_size가 150MB로 설정된 경우 두 번째 버퍼가 남은 50MB 공간에 들어가지 않기 때문에 결과 파일 크기는 100MB로 반내림됩니다.<br /><br /> 기본 파일 크기가 세션 버퍼 크기보다 작으면 max_file_size를 [sys.server_event_sessions](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql) 카탈로그 뷰의 max_memory 열에 있는 값으로 설정하는 것이 좋습니다.|  
|max_rollover_files|32비트 정수. 이 값은 선택 사항입니다.|파일 시스템에 보관할 최대 파일 수입니다. 기본값은 5입니다.|  
|increment|32비트 정수. 이 값은 선택 사항입니다.|파일의 증가분(MB)입니다. 이 값이 지정되지 않은 경우 증분에 대한 기본값은 세션 버퍼 크기의 두 배가 됩니다.|  
  
 이벤트 파일 대상이 처음 만들어질 때 지정한 파일 이름에는 _0\_ 과 정수(Long) 값이 추가됩니다. 이 정수 값은 1600년 1월 1일에서 파일이 만들어진 날짜 및 시간 사이의 밀리초 수로 계산됩니다. 이후의 롤오버 파일도 이 형식을 사용합니다. 정수(Long) 값을 검토하면 가장 최근 파일을 확인할 수 있습니다. 다음 예에서는 파일 이름 옵션을 C:\OutputFiles\MyOutput.xel로 지정한 경우 파일의 이름이 지정되는 방식을 보여 줍니다.  
  
-   처음 생성된 파일 - C:\OutputFiles\MyOutput_0_128500310259380000.xel  
  
-   첫 번째 롤오버 파일 - C:\OutputFiles\MyOutput_0_128505831770890000.xel  
  
-   두 번째 롤오버 파일 - C:\OutputFiles\MyOutput_0_132410772966237000.xel  
  
## <a name="adding-the-target-to-a-session"></a>세션에 대상 추가  
 확장 이벤트 세션에 이벤트 파일 대상을 추가하려면 이벤트 세션을 만들거나 변경할 때 다음 문을 포함합니다. 문에서 *file_name* 을 원하는 파일 이름 및 경로로 바꿉니다.  
  
```  
ADD TARGET package0.event_file(  
   SET filename='file_name.xel')  
```  
  
## <a name="reviewing-the-target-output"></a>대상 출력 검토  
 파일 대상의 출력을 검토하려면 sys.fn_xe_file_target_read_file 함수를 사용해야 합니다. 데이터를 XML로 캐스팅하는 것이 좋습니다. 다음 구문을 사용할 수 있습니다. 구문에서 *file_name* 을 대상을 추가할 때 지정한 파일 이름 및 경로로 바꿉니다.  
  
```  
SELECT *, CAST(event_data AS XML) AS 'event_data_XML'  
FROM sys.fn_xe_file_target_read_file('file_name*.xel', NULL, NULL, NULL)  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 확장 이벤트 대상](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [sys.fn_xe_file_target_read_file &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)   
 [CREATE EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
