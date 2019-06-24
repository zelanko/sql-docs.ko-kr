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
manager: jroth
ms.openlocfilehash: 58ebcb2560e3b03703d7a419b28c6c04e41c19f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794085"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 드라이버에 대한 준비된 명령문 메타데이터 캐싱
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

이 문서에서는 드라이버의 성능 향상을 위해 구현 되는 두 가지 변경 내용을 설명 합니다.

## <a name="batching-of-unprepare-for-prepared-statements"></a>준비 된 문의 Unprepare의 일괄 처리
버전 6.1.6-preview, 성능이 개선 되었습니다 최소화를 통해 구현 되므로 서버 왕복 수를 SQL Server입니다. 이전에 모든 prepareStatement 쿼리에 대해 unprepare에 대 한 호출도 전송 되었습니다. 드라이버는 일괄 처리는 이제 임계값의 기본값은 10는 "ServerPreparedStatementDiscardThreshold"까지 쿼리를 준비 취소 합니다.

> [!NOTE]  
>  사용자는 다음 메서드를 사용 하 여 기본값을 변경할 수 있습니다: setServerPreparedStatementDiscardThreshold (int 값)

6\.1.6-preview에서 도입 된 가지 더 변경은 그 전에 드라이버는 항상 호출 sp_prepexec입니다. 이제 준비 된 문을 첫 번째 실행에서 sp_executesql을 호출 하는 드라이버 및 나머지 sp_prepexec 실행에 대 한 핸들을 할당 합니다. 자세한 세부 정보를 찾을 수 있습니다 [여기](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)합니다.

> [!NOTE]  
>  사용자를 enablePrepareOnFirstPreparedStatementCall 설정 하 여 sp_prepexec를 항상 호출의 이전 버전에 기본 동작을 변경할 수 있습니다 **true** 다음 메서드를 사용 하 여: setEnablePrepareOnFirstPreparedStatementCall (부울 값)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>준비 된 문의 일괄 처리에 대 한이 변경으로 도입 된 새 Api 목록은 Unprepare

 **SQLServerConnection**
 
|새 메서드|설명|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|준비 된 현재 처리 중인 개수를 반환 문 준비 작업을 취소 합니다.|
|void closeUnreferencedPreparedStatementHandles()|실행 대기 중인 모든 삭제 된 준비 된 문의 unprepare 요청을 강제로 수행 합니다.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|특정 연결 인스턴스에 대 한 동작을 반환합니다. False 이면 첫 번째 실행에서 sp_executesql을 호출 하지는 문 준비를 두 번째 실행 sp_prepexec 호출 되 면 및 실제로 준비 된 문 핸들을 설정 합니다. 다음 호출 sp_execute을 실행 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되 면 됩니다. 호출 setDefaultEnablePrepareOnFirstPreparedStatementCall() 하 여이 옵션의 기본값을 변경할 수 있습니다.|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|특정 연결 인스턴스에 대 한 동작을 지정 합니다. 값이 false 이면 첫 번째 실행에서 sp_executesql을 호출 하지는 문 준비를 두 번째 실행 sp_prepexec 호출 되 면 및 실제로 준비 된 문 핸들을 설정 합니다. 다음 호출 sp_execute을 실행 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되 면 됩니다.|
|int getServerPreparedStatementDiscardThreshold()|특정 연결 인스턴스에 대 한 동작을 반환합니다. 이 설정은 얼마나 많은 처리 중인 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출 실행 되기 전에 작업 (sp_unprepare) 연결 별로 처리 하지 않을 수를 제어 합니다. 설정 되어 있으면 < = 1, unprepare 준비 된 문에서 닫기 작업이 즉시 실행 됩니다. 로 설정 된 경우 {@literal >} 1, 이러한 호출이 함께 일괄 처리 너무 자주 호출 sp_unprepare 오버 헤드를 방지 하려면. 호출 getDefaultServerPreparedStatementDiscardThreshold() 하 여이 옵션의 기본값을 변경할 수 있습니다.|
|void setServerPreparedStatementDiscardThreshold(int value)|특정 연결 인스턴스에 대 한 동작을 지정 합니다. 이 설정은 얼마나 많은 처리 중인 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출 실행 되기 전에 작업 (sp_unprepare) 연결 별로 처리 하지 않을 수를 제어 합니다. 설정 되어 있으면 < = 1 unprepare 작업 준비 된 문에서 닫기 즉시 실행 됩니다. > 1로 설정 된 경우 이러한 호출은 함께 일괄 처리 sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하려면.|

 **SQLServerDataSource**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|이 구성은 false 인 경우 준비 된 문을 첫 번째 실행 sp_executesql을 호출 하지는 문 준비를 두 번째 실행 sp_prepexec 호출 되 면 및 실제로 준비 된 문 핸들을 설정 합니다. 다음 호출 sp_execute을 실행 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되 면 됩니다.|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|이 구성은 sp_executesql을 호출 하는 첫 번째 실행 준비 된 문을 false를 반환 하지는 문 준비를 두 번째로 실행 되 면를 sp_prepexec를 호출 하 고 실제로 준비 된 문 핸들을 설정 합니다. 다음 호출 sp_execute을 실행 합니다. 닫기에 준비 된 문에서 sp_unprepare 필요를에서는이 문이 한 번만 실행 되 면 됩니다.|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|이 설정은 얼마나 많은 처리 중인 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출 실행 되기 전에 작업 (sp_unprepare) 연결 별로 처리 하지 않을 수를 제어 합니다. 설정 되어 있으면 < = 1 unprepare 작업 준비 된 문에서 닫기 즉시 실행 됩니다. 로 설정 된 경우 {@literal >} sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하려면 이러한 호출은 함께 일괄 처리 1|
|int getServerPreparedStatementDiscardThreshold()|이 설정은 얼마나 많은 처리 중인 준비 문을 삭제 서버의 미처리 핸들을 정리에 대 한 호출 실행 되기 전에 작업 (sp_unprepare) 연결 별로 처리 하지 않을 수를 제어 합니다. 설정 되어 있으면 < = 1 unprepare 작업 준비 된 문에서 닫기 즉시 실행 됩니다. 로 설정 된 경우 {@literal >} sp_unprepare를 너무 자주 호출 하는 오버 헤드를 방지 하려면 이러한 호출은 함께 일괄 처리 1입니다.|

## <a name="prepared-statement-metatada-caching"></a>준비 된 문 메타 캐싱
6\.3.0-preview 버전부터 SQL Server 용 Microsoft JDBC 드라이버는 준비 된 문의 캐싱을 지원합니다. V6.3.0-미리 보기 전에 이미 준비 되어 캐시에 저장 하는 쿼리를 실행 한 경우 동일한 쿼리를 다시 호출 되지 않습니다 준비 합니다. 이제 드라이버 캐시에서 쿼리 조회 핸들을 찾아서 sp_execute를 사용 하 여 실행 합니다.
준비 된 문 메타 데이터 캐싱은 **비활성화** 기본적으로 합니다. 활성화 하기 위해 연결 개체에서 다음 메서드를 호출 해야 합니다.

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

예: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>준비 된 문에 대 한이 변경으로 도입 된 새 Api 목록은 메타 데이터 캐싱

 **SQLServerConnection**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|문 풀링을 true 또는 false로 설정 합니다.|
|boolean getDisableStatementPooling()|문 풀링을 사용 하지 않도록 설정 하는 경우 true를 반환 합니다.|
|void setStatementPoolingCacheSize(int value)|이 연결에 대 한 준비 된 문 캐시의 크기를 지정합니다. 값이 1 보다 작은 캐시 없음를 의미 합니다.|
|int getStatementPoolingCacheSize()|이 연결에 대 한 준비 된 문 캐시의 크기를 반환합니다. 값이 1 보다 작은 캐시 없음를 의미 합니다.|
|int getStatementHandleCacheEntryCount()|풀링된 준비 된 문 핸들의 현재 수를 반환합니다.|
|boolean isPreparedStatementCachingEnabled()|문 풀링을 사용 하도록 설정할지 여부 또는이 연결에 없습니다.|

 **SQLServerDataSource**
 
|새 메서드|설명|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|True 또는 false로 문 풀링 설정|
|boolean getDisableStatementPooling()|문 풀링을 사용 하지 않도록 설정 하는 경우 true를 반환 합니다.|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|이 연결에 대 한 준비 된 문 캐시의 크기를 지정합니다. 값이 1 보다 작은 캐시 없음를 의미 합니다.|
|int getStatementPoolingCacheSize()|이 연결에 대 한 준비 된 문 캐시의 크기를 반환합니다. 값이 1 보다 작은 캐시 없음를 의미 합니다.|

## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
