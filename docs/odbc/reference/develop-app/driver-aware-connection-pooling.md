---
description: 드라이버 인식 연결 풀링
title: 드라이버 인식 연결 풀링 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed2fa29a68095be9cfcc7d4192c6dc2e15f3eac7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494661"
---
# <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링
드라이버 인식 연결 풀링은 Windows 8에서 드라이버 관리자의 새로운 기능입니다. 드라이버 인식 연결 풀링을 통해 드라이버 작성자는 ODBC 드라이버에서 연결 풀링 동작을 사용자 지정할 수 있습니다.  
  
> [!NOTE]  
>  드라이버 인식 연결 풀링은 커서 라이브러리에서 지원 되지 않습니다. 드라이버 인식 연결 풀링을 사용 하는 경우 응용 프로그램에서 SQLSetConnectAttr을 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.  
  
 드라이버 인식 연결 풀링을 통해 드라이버 관리자 연결 풀링과 관련 된 다음 문제를 해결할 수 있습니다.  
  
 **풀 조각화** 새 연결 요청의 연결 문자열과 정확히 일치 하는 경우에만 드라이버 관리자가 풀에서 연결을 반환 합니다.  드라이버 관리자가 정확 하 게 일치 해야 하는 한 가지 이유는 드라이버 관리자가 모든 드라이버별 연결 문자열 키워드와 해당 값을 이해 하지 못하는 것입니다.  그러나 드라이버가 새 연결을 여는 데 필요한 시간 보다 작게 데이터베이스를 변경할 수 있기 때문에 일부 연결 문자열 키워드 값 (예: 데이터베이스 이름)에 정확히 일치 하는 항목이 필요 하지 않을 수 있습니다 (정확한 시간 차이는 데이터 원본에 따라 달라 짐). 그리고 일부 연결 특성 (예: SQL_ATTR_CURRENT_CATALOG)의 차이점은 다른 특성 (예: SQL_ATTR_LOGIN_TIMEOUT)의 차이 보다 변경 하는 데 시간이 더 오래 걸릴 수 있습니다. 이로 인해 드라이버 관리자가 풀에서 재사용 가능한 가장 저렴 한 연결을 사용 하지 못할 수 있습니다. 드라이버에서 많은 새 연결을 만들어야 하는 경우 응용 프로그램의 성능이 저하 되 고 데이터 원본 확장성이 줄어들 수 있습니다. 드라이버가 연결 요청에 대해 풀에서 연결을 다시 사용 하는 비용을 보다 정확 하 게 예측할 수 있으므로 풀 조각화는 드라이버 인식 연결 풀링을 사용 하 여 줄일 수 있습니다.  
  
 **응용 프로그램 기본 설정 고려 안 함** 일부 데이터 원본에서는 몇 가지 특성을 다시 설정 하는 것과 비교 하 여 새 연결을 효율적으로 열 수 있으므로 응용 프로그램이 풀에서 약간 일치 하지 않는 연결을 다시 사용 하 고 일부 값을 다시 설정 하는 대신 새 연결을 열어야 할 수 있습니다 (연결 풀 초기화 구문 중에 속도가 느릴 수 있음). 하지만 일부 응용 프로그램은 서버 부하를 더 작게 유지 하 고 더 적은 수의 연결을 열 수 있습니다. 단, 올바른 동작의 불일치를 해결 하는 데 더 많은 비용이 발생할 수 있습니다. 드라이버 인식 연결 풀링을 사용 하지 않으면 드라이버 관리자가 모든 드라이버 관련 연결 특성을 인식 하지 못하기 때문에 이러한 종류의 기본 설정을 효과적으로 지정할 수 없습니다. 드라이버 인식 연결 풀링을 사용 하면 드라이버가 사용자 기본 설정 (SQLSetConnectAttr의 드라이버별 특성 사용)을 가져올 수 있으므로 사용자의 기본 설정에 따라 풀에서 연결을 다시 사용 하는 비용을 보다 정확 하 게 예측할 수 있습니다.  
  
 드라이버 인식 연결 풀링에 대 한 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)을 참조 하세요.  
  
## <a name="determining-driver-support"></a>드라이버 지원 확인  
 드라이버 인식 연결 풀링은 드라이버가 지원 하지 않을 수 있는 선택적 기능입니다. 드라이버가 지원 하는지 확인 하려면 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)의 SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* 를 사용 합니다.  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링을 사용 하도록 설정 하는 방법  
 응용 프로그램은 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)를 사용 하 여 SQL_CP_DRIVER_AWARE SQL_ATTR_CONNECTION_POOLING 특성을 설정 하 여 드라이버의 연결 풀링 인식 기능을 사용할 수 있습니다. 드라이버가 연결 풀 인식을 지원 하지 않는 경우 드라이버 관리자 연결 풀링이 사용 됩니다 (SQL_CP_DRIVER_AWARE 대신 SQL_CP_ONE_PER_HENV 지정 된 것과 동일). ODBC 2.x 및 2.x 응용 프로그램은이 기능을 사용 하도록 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
