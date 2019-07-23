---
title: JDBC 드라이버에 대한 준비된 명령문 메타데이터 캐싱 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a9abd72b366060da2fdffd58c17ace50f01246a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956202"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 드라이버에 대한 준비된 명령문 메타데이터 캐싱
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 드라이버의 성능을 향상 시키기 위해 구현 된 두 가지 변경 내용에 대 한 정보를 제공 합니다.

## <a name="batching-of-unprepare-for-prepared-statements"></a>준비 된 문의 Unprepare 일괄 처리
버전 6.1.6-미리 보기에서는 서버 왕복을 SQL Server으로 최소화 하 여 성능 향상이 구현 되었습니다. 이전에는 모든 prepareStatement 쿼리를 위해 unprepare에 대 한 호출도 전송 했습니다. 이제 드라이버는 기본값 10을 포함 하는 임계값 "ServerPreparedStatementDiscardThreshold"까지 unprepare 쿼리를 일괄 처리 합니다.

> [!NOTE]  
>  사용자는 다음 메서드를 사용 하 여 기본값을 변경할 수 있습니다. setServerPreparedStatementDiscardThreshold (int value)

6\.1.6에서 도입 된 변경 내용 중 하나는이 이전에, 드라이버가 항상 sp_prepexec를 호출 한다는 것입니다. 이제 준비 된 문을 처음 실행 하는 경우 드라이버는 sp_executesql을 호출 하 고 rest에 대해 sp_prepexec를 실행 하 고 핸들을 할당 합니다. 자세한 내용은 [여기](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)를 참조 하세요.

> [!NOTE]  
>  사용자는 setEnablePrepareOnFirstPreparedStatementCall (부울 값) 메서드를 사용 하 여 enablePrepareOnFirstPreparedStatementCall를 **true** 로 설정 하 여 기본 동작을 항상 호출 하는 sp_prepexec의 이전 버전으로 변경할 수 있습니다. )

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>준비 된 문의 Unprepare 일괄 처리를 위해이 변경 내용으로 도입 된 새 Api 목록

 **SQLServerConnection**
 
|새 메서드|설명|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|현재 해결 되지 않은 준비 된 문 unprepare 작업 수를 반환 합니다.|
|void closeUnreferencedPreparedStatementHandles()|취소 된 모든 취소 된 준비 문에 대해 unprepare 요청을 강제로 실행 합니다.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|특정 연결 인스턴스에 대 한 동작을 반환 합니다. False 이면 첫 번째 실행에서 sp_executesql을 호출 하 고 문을 준비 하지 않고, 두 번째 실행이 수행 되 면 sp_prepexec를 호출 하 고 실제로 준비 된 문 핸들을 설정 합니다. 다음 실행은 sp_execute를 호출 합니다. 이렇게 하면 문이 한 번만 실행 되는 경우 준비 된 문에 대 한 sp_unprepare 필요 하지 않습니다. 이 옵션의 기본값은 setDefaultEnablePrepareOnFirstPreparedStatementCall ()를 호출 하 여 변경할 수 있습니다.|
|void setEnablePrepareOnFirstPreparedStatementCall (부울 값)|특정 연결 인스턴스에 대 한 동작을 지정 합니다. 값이 false 이면 첫 번째 실행에서 sp_executesql을 호출 하 고 문을 준비 하지 않습니다. 두 번째 실행이 수행 되 면 sp_prepexec를 호출 하 고 실제로 준비 된 문 핸들을 설정 합니다. 다음 실행은 sp_execute를 호출 합니다. 이렇게 하면 문이 한 번만 실행 되는 경우 준비 된 문에 대 한 sp_unprepare 필요 하지 않습니다.|
|int getServerPreparedStatementDiscardThreshold()|특정 연결 인스턴스에 대 한 동작을 반환 합니다. 이 설정은 서버에서 처리 중인 핸들 정리에 대 한 호출이 실행 되기 전에 연결 당 처리 되지 않은 준비 된 문 삭제 작업 수 (sp_unprepare)를 제어 합니다. 설정이 < = 1 이면 준비 된 문 종료 시 unprepare 작업이 즉시 실행 됩니다. {@literal >} 1로 설정 된 경우 이러한 호출은 sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하기 위해 함께 일괄 처리 됩니다. 이 옵션의 기본값은 getDefaultServerPreparedStatementDiscardThreshold ()를 호출 하 여 변경할 수 있습니다.|
|void setServerPreparedStatementDiscardThreshold(int value)|특정 연결 인스턴스에 대 한 동작을 지정 합니다. 이 설정은 서버에서 처리 중인 핸들 정리에 대 한 호출이 실행 되기 전에 연결 당 처리 되지 않은 준비 된 문 삭제 작업 수 (sp_unprepare)를 제어 합니다. 설정이 < = 1 이면 준비 된 문 종료 시 작업이 즉시 실행 됩니다. > 1로 설정 된 경우 이러한 호출은 sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하기 위해 함께 일괄 처리 됩니다.|

 **SQLServerDataSource**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall (부울 enablePrepareOnFirstPreparedStatementCall)|이 구성이 false 인 경우 준비 된 문의 첫 번째 실행은 sp_executesql을 호출 하 고 문을 준비 하지 않습니다. 두 번째 실행이 수행 되 면 sp_prepexec를 호출 하 고 실제로 준비 된 문 핸들을 설정 합니다. 다음 실행은 sp_execute를 호출 합니다. 이렇게 하면 문이 한 번만 실행 되는 경우 준비 된 문에 대 한 sp_unprepare 필요 하지 않습니다.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|이 구성이 false를 반환 하는 경우 준비 된 문의 첫 번째 실행은 sp_executesql을 호출 하 고 문을 준비 하지 않습니다. 두 번째 실행이 발생 하면 sp_prepexec를 호출 하 고 실제로 준비 된 문 핸들을 설정 합니다. 다음 실행은 sp_execute를 호출 합니다. 이렇게 하면 문이 한 번만 실행 되는 경우 준비 된 문에 대 한 sp_unprepare 필요 하지 않습니다.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|이 설정은 서버에서 처리 중인 핸들 정리에 대 한 호출이 실행 되기 전에 연결 당 처리 되지 않은 준비 된 문 삭제 작업 수 (sp_unprepare)를 제어 합니다. 설정이 < = 1 이면 준비 된 문 종료 시 작업이 즉시 실행 됩니다. {@literal >} 1로 설정 된 경우 이러한 호출은 sp_unprepare을 너무 자주 호출 하는 오버 헤드를 방지 하기 위해 함께 일괄 처리 됩니다.|
|int getServerPreparedStatementDiscardThreshold()|이 설정은 서버에서 처리 중인 핸들 정리에 대 한 호출이 실행 되기 전에 연결 당 처리 되지 않은 준비 된 문 삭제 작업 수 (sp_unprepare)를 제어 합니다. 설정이 < = 1 이면 준비 된 문 종료 시 작업이 즉시 실행 됩니다. {@literal >} 1로 설정 된 경우 이러한 호출은 sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하기 위해 함께 일괄 처리 됩니다.|

## <a name="prepared-statement-metatada-caching"></a>준비 된 문 같은 메타 데이터가 캐싱
6\.3.0 버전을 기반으로 하는 Microsoft JDBC driver for SQL Server은 준비 된 문 캐싱을 지원 합니다. V 6.3.0-미리 보기 이전에는 이미 준비 되어 캐시에 저장 된 쿼리를 실행 하는 경우 동일한 쿼리를 다시 호출 해도 준비 되지 않습니다. 이제 드라이버가 캐시에서 쿼리를 조회 하 고 핸들을 찾아 sp_execute를 사용 하 여 실행 합니다.
준비 된 문 메타 데이터 캐싱은 기본적으로 **사용 되지** 않습니다. 이를 사용 하도록 설정 하려면 연결 개체에 대해 다음 메서드를 호출 해야 합니다.

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

예: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>준비 된 문 메타 데이터 캐싱에 대해이 변경 내용으로 도입 된 새 Api 목록

 **SQLServerConnection**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|문 풀링을 true 또는 false로 설정 합니다.|
|boolean getDisableStatementPooling()|문 풀링이 사용 하지 않도록 설정 된 경우 true를 반환 합니다.|
|void setStatementPoolingCacheSize(int value)|이 연결에 대해 준비 된 문 캐시의 크기를 지정 합니다. 1 보다 작은 값은 캐시가 없음을 의미 합니다.|
|int getStatementPoolingCacheSize()|이 연결에 대해 준비 된 문 캐시의 크기를 반환 합니다. 1 보다 작은 값은 캐시가 없음을 의미 합니다.|
|int getStatementHandleCacheEntryCount()|풀링된 준비 된 문 핸들의 현재 수를 반환 합니다.|
|boolean isPreparedStatementCachingEnabled()|이 연결에 대해 문 풀링이 사용 되는지 여부를 나타냅니다.|

 **SQLServerDataSource**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setDisableStatementPooling (부울 Statementpoolingcachesize)|문 풀링을 true 또는 false로 설정 합니다.|
|boolean getDisableStatementPooling()|문 풀링이 사용 하지 않도록 설정 된 경우 true를 반환 합니다.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|이 연결에 대해 준비 된 문 캐시의 크기를 지정 합니다. 1 보다 작은 값은 캐시가 없음을 의미 합니다.|
|int getStatementPoolingCacheSize()|이 연결에 대해 준비 된 문 캐시의 크기를 반환 합니다. 1 보다 작은 값은 캐시가 없음을 의미 합니다.|

## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
