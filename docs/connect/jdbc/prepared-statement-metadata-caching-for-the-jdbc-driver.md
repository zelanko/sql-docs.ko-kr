---
title: JDBC 드라이버에 대 한 캐싱을 문 메타 데이터를 준비 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a291cfb9497cee4fea87db915ca088069c1ec3cf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32833158"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 드라이버에 대 한 캐싱을 준비 된 문의 메타 데이터
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 드라이버의 성능 향상을 위해 구현 되는 두 개의 변경 내용을 설명 합니다.

## <a name="batching-of-unprepare-for-prepared-statements"></a>준비 된 문의 Unprepare의 일괄 처리
버전 6.1.6-preview, 성능 향상을 최소화을 통해 구현 된 이후 서버 왕복 SQL Server에는 수입니다. 이전에 모든 prepareStatement 쿼리에 대해 unprepare에 대 한 호출 또한 보냈습니다. 드라이버는 일괄 처리는 이제 임계값 기본값 10에는 "ServerPreparedStatementDiscardThreshold" 최대 쿼리 준비가 취소 합니다.

> [!NOTE]  
>  사용자를 다음 메서드로 기본값을 변경할 수 있습니다: setServerPreparedStatementDiscardThreshold (int 값)

6.1.6-preview에서 도입 된 한 가지 더 많은 변경이이 앞서 드라이버는 항상 호출 하는 sp_prepexec입니다. 이제, 준비 된 문을 첫 번째 실행에서 드라이버 sp_executesql을 호출 하 고 나머지 sp_prepexec 실행 대 한 핸들을 할당 합니다. 자세한 내용은 있습니다 [여기](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)합니다.

> [!NOTE]  
>  사용자가을 이전 버전을 enablePrepareOnFirstPreparedStatementCall 설정 하 여 sp_prepexec를 항상 호출의 기본 동작을 변경할 수 **true** 다음 메서드를 사용 하 여: setEnablePrepareOnFirstPreparedStatementCall (부울 값)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>준비 된 문의 Unprepare의 일괄 처리를 위해이 변경으로 도입 된 새로운 Api 목록

 **SQLServerConnection**
 
|새 메서드|Description|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|현재 처리 중인 개수를 준비 반환 문을 준비 작업을 취소 합니다.|
|void closeUnreferencedPreparedStatementHandles()|실행할 모든 미해결 폐기 된 준비 된 문의 unprepare 요청을 강제로 수행 합니다.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|특정 연결 인스턴스에 대 한 동작을 반환 합니다. False 인 경우 첫 번째 실행에서 sp_executesql을 호출 하 고 sp_prepexec 호출 발생 하는 두 번째로 실행 되 면 문을 준비 하지 하며 실제로 준비 된 문 핸들을 설정 합니다. 다음 호출 sp_execute을 실행 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되는 경우 됩니다. SetDefaultEnablePrepareOnFirstPreparedStatementCall() 호출 하 여이 옵션의 기본값을 변경할 수 있습니다.|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|인스턴스를 특정 연결에 대 한 동작을 지정합니다. 값이 false 첫 번째 실행에서 sp_executesql을 호출 및 sp_prepexec 호출 발생 하는 두 번째로 실행 되 면 문을 준비 하지 않으며 실제로 준비 된 문 핸들을 설정 합니다. 다음 호출 sp_execute을 실행 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되는 경우 됩니다.|
|int getServerPreparedStatementDiscardThreshold()|특정 연결 인스턴스에 대 한 동작을 반환 합니다. 이 설정은 개수 뛰어난 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출을 실행 하기 전에 작업 (sp_unprepare) 연결당 보류 될 수를 제어 합니다. 설정 되어 있으면 < = 1, unprepare 준비 문에서 닫기 작업이 즉시 실행 됩니다. 로 설정 되어 있으면 {@literal >을 (를) 1, 이러한 호출이 일괄 처리할 함께 너무 자주 호출 sp_unprepare의 오버 헤드를 방지 하기 위해. GetDefaultServerPreparedStatementDiscardThreshold() 호출 하 여이 옵션의 기본값을 변경할 수 있습니다.|
|void setServerPreparedStatementDiscardThreshold(int value)|인스턴스를 특정 연결에 대 한 동작을 지정합니다. 이 설정은 개수 뛰어난 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출을 실행 하기 전에 작업 (sp_unprepare) 연결당 보류 될 수를 제어 합니다. 설정 되어 있으면 < = 1 준비 작업 준비 문에서 닫기 즉시 실행 됩니다. > 1로 설정 된 경우 이러한 호출은 sp_unprepare를 너무 자주 호출의 오버 헤드를 방지 하기 위해 일괄 됩니다.|

 **SQLServerDataSource**
 
|새 메서드|Description|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|이 구성은 false 준비 된 문을 첫 번째 실행에서 sp_executesql을 호출 및 sp_prepexec 호출 발생 하는 두 번째로 실행 되 면 문을 준비 하지 않으며 실제로 준비 된 문 핸들을 설정 합니다. 다음 호출 sp_execute을 실행 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되는 경우 됩니다.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|이 구성을 sp_executesql을 호출 하는 준비 된 문을 첫 번째 실행에서 false를 반환 하 고 발생 하는 두 번째로 실행 되 면 문을 준비 하지, sp_prepexec를 호출 하 고 실제로 준비 된 문 핸들을 설정 합니다. 다음 호출 sp_execute을 실행 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되는 경우 됩니다.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|이 설정은 개수 뛰어난 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출을 실행 하기 전에 작업 (sp_unprepare) 연결당 보류 될 수를 제어 합니다. 설정 되어 있으면 < = 1 준비 작업 준비 문에서 닫기 즉시 실행 됩니다. 로 설정 되어 있으면 {@literal >} sp_unprepare를 너무 자주 호출의 오버 헤드를 방지 하기 위해 이러한 호출은 내용이 함께 일괄 처리 1|
|int getServerPreparedStatementDiscardThreshold()|이 설정은 개수 뛰어난 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출을 실행 하기 전에 작업 (sp_unprepare) 연결당 보류 될 수를 제어 합니다. 설정 되어 있으면 < = 1 준비 작업 준비 문에서 닫기 즉시 실행 됩니다. 로 설정 되어 있으면 {@literal >} 1 sp_unprepare를 너무 자주 호출의 오버 헤드를 방지 하기 위해 이러한 호출은 함께 일괄 처리 됩니다.|

## <a name="prepared-statement-metatada-caching"></a>준비 된 문 같은 메타 데이터가 캐싱
6.3.0-preview 버전부터 SQL Server 용 Microsoft JDBC 드라이버는 준비 된 문의 캐싱을 지원합니다. V6.3.0-미리 보기 전에 이미 준비 및 캐시에 저장 된 쿼리를 실행 한 경우 동일한 쿼리를 다시 호출 되지 않습니다 준비 합니다. 이제 드라이버 캐시에서 쿼리를 조회와 핸들을 찾고 sp_execute로 실행 합니다.
준비 된 문 메타 데이터 캐싱을 **비활성화** 기본적으로 합니다. 을 사용 하려면 메서드를 호출 하는 다음 연결 개체에서 필요 합니다.

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

예를 들어: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>준비 된 문에 대 한이 변경으로 도입 된 새로운 Api 목록 메타 데이터 캐싱

 **SQLServerConnection**
 
|새 메서드|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|문 풀링을 true 또는 false로 설정 합니다.|
|부울 getDisableStatementPooling()|문 풀링을 사용 하지 않도록 설정 하는 경우 true를 반환 합니다.|
|void setStatementPoolingCacheSize(int value)|이 연결에 대 한 준비 된 문 캐시의 크기를 지정합니다. 값이 1 보다 작은 캐시 없음을 의미 합니다.|
|int getStatementPoolingCacheSize()|이 연결에 대 한 준비 된 문 캐시의 크기를 반환 합니다. 값이 1 보다 작은 캐시 없음을 의미 합니다.|
|int getStatementHandleCacheEntryCount()|풀링된 준비 된 문 핸들의 현재 수를 반환 합니다.|
|boolean isPreparedStatementCachingEnabled()|문 풀링을 사용 되는지 여부를 또는이 연결에 없습니다.|

 **SQLServerDataSource**
 
|새 메서드|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|True 또는 false로 설정 하는 문 풀링|
|부울 getDisableStatementPooling()|문 풀링을 사용 하지 않도록 설정 하는 경우 true를 반환 합니다.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|이 연결에 대 한 준비 된 문 캐시의 크기를 지정합니다. 값이 1 보다 작은 캐시 없음을 의미 합니다.|
|int getStatementPoolingCacheSize()|이 연결에 대 한 준비 된 문 캐시의 크기를 반환 합니다. 값이 1 보다 작은 캐시 없음을 의미 합니다.|

## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
