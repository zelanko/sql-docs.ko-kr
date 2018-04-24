---
title: MSSQLSERVER_1793 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00919111d7df7f3e6a3077a5c99e355c93abacad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver1793"></a>MSSQLSERVER_1793
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1793|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|FILESTREAM_BASEDATA_NEED_SAME_PARTITION|  
|메시지 텍스트|FILESTREAM 데이터에 지정된 파티션 구성표가 없으므로 '%.*ls' 인덱스를 삭제할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
이 메시지는 FILESTREAM 데이터가 들어 있는 테이블에서 클러스터형 인덱스를 삭제하려고 시도하고 기본 데이터에 대한 **MOVE TO** 절을 지정하지만 FILESTREAM 데이터에 대한 **FILESTREAM_ON** 절은 지정하지 않는 경우에 나타납니다.  
  
## <a name="user-action"></a>사용자 동작  
FILESTREAM 데이터가 들어 있는 테이블에서 클러스터형 인덱스를 삭제하는 경우 다음 옵션 중 하나를 사용하십시오.  
  
-   기본 데이터에 대한 **MOVE TO** 절과 FILESTREAM 데이터에 대한 **FILESTREAM_ON** 절을 지정합니다.  
  
-   기본 데이터에 대한 **MOVE TO** 절이나 FILESTREAM 데이터에 대한 **FILESTREAM_ON** 절을 지정하지 않습니다.  
  
다음 예는 파티션 구성표가 기본 데이터에 대해서는 지정되어 있지만 FILESTREAM 데이터에 대해서는 지정되어 있지 않기 때문에 실패합니다.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY] )  
GO  
```  
  
다음 예제는 기본 데이터에 대한 **MOVE TO** 절과 FILESTREAM 데이터에 대한 **FILESTREAM_ON** 절이 모두 지정되어 있기 때문에 성공합니다.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY], filestream_on 'default' )  
GO  
```  
  
또한 다음 예제는 기본 데이터에 대한 **MOVE TO** 절이나 FILESTREAM 데이터에 대한 **FILESTREAM_ON** 절이 둘 다 지정되어 있지 않기 때문에 성공합니다.  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF )  
GO  
```  
  
