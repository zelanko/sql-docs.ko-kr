---
title: Database 이벤트 범주 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0300d8c67bd99f160eb89a7d29848736ceb09d5c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642941"
---
# <a name="database-event-category"></a>Database 이벤트 범주
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Database** 이벤트 범주에는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 모니터링하는 이벤트 클래스가 포함됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|설명|  
|-----------|-----------------|  
|[Data File Auto Grow 이벤트 클래스](../../relational-databases/event-classes/data-file-auto-grow-event-class.md)|데이터 파일이 자동으로 증가함을 나타냅니다. 데이터 파일이 ALTER DATABASE를 통해 명시적으로 증가하는 경우 이 이벤트는 트리거되지 않습니다.|  
|[Data File Auto Shrink 이벤트 클래스](../../relational-databases/event-classes/data-file-auto-shrink-event-class.md)|데이터 파일이 축소되었음을 나타냅니다.|  
|[데이터베이스 미러링 Connection 이벤트 클래스](../../relational-databases/event-classes/database-mirroring-connection-event-class.md)|데이터베이스 미러링에서 관리하는 전송 연결 상태를 보고하기 위해 생성되는 이벤트입니다.|  
|[Database Mirroring State Change 이벤트 클래스](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)|미러된 데이터베이스의 상태가 변경되었음을 나타냅니다.|  
|[Database Suspect Data Page 이벤트 클래스](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)|**msdb** 데이터베이스의 **suspect_pages** 테이블에 페이지가 추가된 시간을 나타냅니다.|  
|[Log File Auto Grow 이벤트 클래스](../../relational-databases/event-classes/log-file-auto-grow-event-class.md)|로그 파일이 자동으로 증가함을 나타냅니다. 이 이벤트는 ALTER DATABASE 문의 명시적인 실행으로 로그 파일이 증가하는 경우에는 트리거되지 않습니다.|  
|[Log File Auto Shrink 이벤트 클래스](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)|로그 파일이 자동으로 증가함을 나타냅니다. 로그 파일이 ALTER DATABASE를 통해 명시적으로 축소되는 경우 이 이벤트는 트리거되지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
