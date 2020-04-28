---
title: Database 이벤트 범주 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], Database event category
- Database event category [SQL Server]
- SQL Server event classes, Database event category
ms.assetid: b61af738-f144-4992-b0b2-d44cb7240991
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0d725f95fc8e9de0865ad895abd860d5f03687b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62662931"
---
# <a name="database-event-category"></a>Database 이벤트 범주
  **Database** 이벤트 범주에는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 모니터링하는 이벤트 클래스가 포함됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[Data File Auto Grow 이벤트 클래스](data-file-auto-grow-event-class.md)|데이터 파일이 자동으로 증가함을 나타냅니다. 데이터 파일이 ALTER DATABASE를 통해 명시적으로 증가하는 경우 이 이벤트는 트리거되지 않습니다.|  
|[Data File Auto Shrink 이벤트 클래스](data-file-auto-shrink-event-class.md)|데이터 파일이 축소되었음을 나타냅니다.|  
|[데이터베이스 미러링 Connection 이벤트 클래스](database-mirroring-connection-event-class.md)|데이터베이스 미러링에서 관리하는 전송 연결 상태를 보고하기 위해 생성되는 이벤트입니다.|  
|[Database Mirroring State Change 이벤트 클래스](database-mirroring-state-change-event-class.md)|미러된 데이터베이스의 상태가 변경되었음을 나타냅니다.|  
|[Database Suspect Data Page 이벤트 클래스](database-suspect-data-page-event-class.md)|**msdb** 데이터베이스의 **suspect_pages** 테이블에 페이지가 추가된 시간을 나타냅니다.|  
|[Log File Auto Grow 이벤트 클래스](log-file-auto-grow-event-class.md)|로그 파일이 자동으로 증가함을 나타냅니다. 이 이벤트는 ALTER DATABASE 문의 명시적인 실행으로 로그 파일이 증가하는 경우에는 트리거되지 않습니다.|  
|[Log File Auto Shrink 이벤트 클래스](log-file-auto-shrink-event-class.md)|로그 파일이 자동으로 증가함을 나타냅니다. 로그 파일이 ALTER DATABASE를 통해 명시적으로 축소되는 경우 이 이벤트는 트리거되지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../extended-events/extended-events.md)  
  
  
