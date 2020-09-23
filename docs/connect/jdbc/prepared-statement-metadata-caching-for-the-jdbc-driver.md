---
title: JDBC 드라이버에 대한 준비된 명령문 메타데이터 캐싱
description: SQL Server용 JDBC Driver에서 데이터베이스에 대한 호출을 최소화하여 성능을 개선하기 위해 준비된 문을 캐시하는 방법과 해당 동작을 제어하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67b35e04ede8608d222c8fc31d89bfd01b093ba7
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435390"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 드라이버에 대한 준비된 명령문 메타데이터 캐싱
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 드라이버의 성능 향상을 위해 구현된 두 가지 변경 사항을 소개합니다.

## <a name="batching-of-unprepare-for-prepared-statements"></a>준비된 문의 준비 취소 일괄 처리
버전 6.1.6(미리 보기)부터는 SQL Server에 대한 서버 라운드트립을 최소화하여 성능을 향상했습니다. 이전에는 모든 prepareStatement 쿼리에 대해 준비 취소 호출도 전송되었습니다. 이제는 드라이버가 기본값이 10인 "ServerPreparedStatementDiscardThreshold" 임계값까지 준비 취소 쿼리를 일괄 처리 합니다.

> [!NOTE]  
>  사용자는 setServerPreparedStatementDiscardThreshold(int value) 메서드로 기본값을 변경할 수 있습니다.

6.1.6(미리 보기)에서의 또 다른 변경 사항이 있는데, 이전 버전에서는 드라이버가 항상 sp_prepexec을 호출했다는 점이 바뀌었다는 사실입니다. 이제는 준비된 문이 처음 실행될 때 드라이버가 sp_executesql을 호출하며, 나머지에 대해서는 sp_prepexec을 실행하고 핸들을 할당합니다. 자세한 내용은 [여기](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)에서 찾을 수 있습니다.

> [!NOTE]  
>  사용자가 setEnablePrepareOnFirstPreparedStatementCall(부울 값) 메서드를 사용하여 enablePrepareOnFirstPreparedStatementCall을 **true**로 설정하면 기본 동작이 항상 sp_prepexec을 호출하던 이전의 버전으로 변경됩니다.

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>준비된 문의 준비 취소 일괄 처리를 위한 이번 변경으로 도입된 새 API의 목록

 **SQLServerConnection**
 
|새 메서드|설명|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|현재 해결되지 않은 준비 문의 준비 취소 작업 수를 반환합니다.|
|void closeUnreferencedPreparedStatementHandles()|해결되지 않아 삭제된 준비 문에 대해 준비 취소 요청을 강제로 실행합니다.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|특정 연결 인스턴스에 대한 동작을 반환합니다. false일 경우에는 첫 번째 실행에서 sp_executesql이 호출되고 문은 준비되지 않습니다. 두 번째 실행이 발생하면 sp_prepexec가 호출되고 준비된 문 핸들이 실제로 설정됩니다. 다음 실행은 sp_execute를 호출합니다. 이렇게 하면 문이 한 번만 실행될 때 준비된 문 닫기에서 sp_unprepare를 사용할 필요가 없습니다. 이 옵션의 기본값은 setDefaultEnablePrepareOnFirstPreparedStatementCall() 호출로 변경할 수 있습니다.|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|특정 연결 인스턴스에 대한 동작을 지정합니다. 값이 false일 경우에는 첫 번째 실행에서 sp_executesql이 호출되고 문은 준비되지 않습니다. 두 번째 실행이 발생하면 sp_prepexec가 호출되고 준비된 문 핸들이 실제로 설정됩니다. 다음 실행은 sp_execute를 호출합니다. 이렇게 하면 문이 한 번만 실행될 때 준비된 문 닫기에서 sp_unprepare를 사용할 필요가 없습니다.|
|int getServerPreparedStatementDiscardThreshold()|특정 연결 인스턴스에 대한 동작을 반환합니다. 이 설정은 서버의 미처리 핸들을 정리하기 위한 호출 실행 전에 연결별로 처리되지 않을 수 있는 미처리 준비 문 삭제 작업(sp_unprepare)의 수를 제어합니다. 설정이 <= 1로 되어 있다면 준비된 문이 종료되자마자 준비 취소 작업이 곧바로 실행됩니다. 설정이 {@literal >} 1로 되어 있다면 이러한 호출은 sp_unprepare 호출이 너무 잦아지는 오버헤드를 방지하기 위해 모두 함께 일괄 처리됩니다. 이 옵션의 기본값은 getDefaultServerPreparedStatementDiscardThreshold() 호출로 변경할 수 있습니다.|
|void setServerPreparedStatementDiscardThreshold(int value)|특정 연결 인스턴스에 대한 동작을 지정합니다. 이 설정은 서버의 미처리 핸들을 정리하기 위한 호출 실행 전에 연결별로 처리되지 않을 수 있는 미처리 준비 문 삭제 작업(sp_unprepare)의 수를 제어합니다. 설정이 <= 1로 되어 있다면 준비된 문이 종료되자마자 준비 취소 작업이 곧바로 실행됩니다. 설정이 > 1로 되어 있다면 이러한 호출은 sp_unprepare 호출이 너무 잦아지는 오버헤드를 방지하기 위해 모두 함께 일괄 처리됩니다.|

 **SQLServerDataSource**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|이 구성이 false일 경우에는 준비된 문의 첫 번째 실행에서 sp_executesql이 호출되고 문은 준비되지 않습니다. 두 번째 실행이 발생하면 sp_prepexec가 호출되고 준비된 문 핸들이 실제로 설정됩니다. 다음 실행은 sp_execute를 호출합니다. 이렇게 하면 문이 한 번만 실행될 때 준비된 문 닫기에서 sp_unprepare를 사용할 필요가 없습니다.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|이 구성으로 false가 반환되면 준비된 문의 첫 번째 실행에서 sp_executesql이 호출되고 문은 준비되지 않습니다. 두 번째 실행이 발생하면 sp_prepexec가 호출되고 준비된 문 핸들이 실제로 설정됩니다. 다음 실행은 sp_execute를 호출합니다. 이렇게 하면 문이 한 번만 실행될 때 준비된 문 닫기에서 sp_unprepare를 사용할 필요가 없습니다.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|이 설정은 서버의 미처리 핸들을 정리하기 위한 호출 실행 전에 연결별로 처리되지 않을 수 있는 미처리 준비 문 삭제 작업(sp_unprepare)의 수를 제어합니다. 설정이 <= 1로 되어 있다면 준비된 문이 종료되자마자 준비 취소 작업이 곧바로 실행됩니다. 설정이 {@literal >} 1로 되어 있다면 이러한 호출은 sp_unprepare 호출이 너무 잦아지는 오버헤드를 방지하기 위해 모두 함께 일괄 처리됩니다.|
|int getServerPreparedStatementDiscardThreshold()|이 설정은 서버의 미처리 핸들을 정리하기 위한 호출 실행 전에 연결별로 처리되지 않을 수 있는 미처리 준비 문 삭제 작업(sp_unprepare)의 수를 제어합니다. 설정이 <= 1로 되어 있다면 준비된 문이 종료되자마자 준비 취소 작업이 곧바로 실행됩니다. 설정이 {@literal >} 1로 되어 있다면 이러한 호출은 sp_unprepare 호출이 너무 잦아지는 오버헤드를 방지하기 위해 모두 함께 일괄 처리됩니다.|

## <a name="prepared-statement-metadata-caching"></a>준비된 문 메타데이터 캐싱
SQL Server용 Microsoft JDBC 드라이버는 버전 6.3.0(미리 보기)부터 준비된 문의 캐싱을 지원합니다. v6.3.0(미리 보기) 이전에는 이미 준비되어 캐시에 저장된 쿼리를 실행할 경우 동일한 쿼리를 다시 호출한다 해도 이를 준비할 수는 없었습니다. 이제는 드라이버가 캐시에서 쿼리를 조회하고 핸들을 찾은 후 with sp_execute로 실행합니다.
준비된 문의 메타데이터 캐싱은 기본적으로 **사용하지 않도록 설정**됩니다. 이를 사용 설정하려면 연결 개체에 다음 메서드를 호출해야 합니다.

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

예: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>준비된 문의 메타데이터 캐싱을 위해 이번 변경으로 도입된 새 API의 목록

 **SQLServerConnection**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|문 풀링을 true 또는 false로 설정합니다.|
|boolean getDisableStatementPooling()|문 풀링이 사용 해제된 경우 true를 반환합니다.|
|void setStatementPoolingCacheSize(int value)|이 연결에 대해 준비된 문 캐시의 크기를 지정합니다. 값이 1 미만이면 캐시가 없음을 뜻합니다.|
|int getStatementPoolingCacheSize()|이 연결에 대해 준비된 문 캐시의 크기를 반환합니다. 값이 1 미만이면 캐시가 없음을 뜻합니다.|
|int getStatementHandleCacheEntryCount()|현재 풀링된 준비 문 핸들의 수를 반환합니다.|
|boolean isPreparedStatementCachingEnabled()|이 연결에 대한 문 풀링의 사용 설정 여부를 표시합니다.|

 **SQLServerDataSource**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|문 풀링을 true 또는 false로 설정합니다.|
|boolean getDisableStatementPooling()|문 풀링이 사용 해제된 경우 true를 반환합니다.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|이 연결에 대해 준비된 문 캐시의 크기를 지정합니다. 값이 1 미만이면 캐시가 없음을 뜻합니다.|
|int getStatementPoolingCacheSize()|이 연결에 대해 준비된 문 캐시의 크기를 반환합니다. 값이 1 미만이면 캐시가 없음을 뜻합니다.|

## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
