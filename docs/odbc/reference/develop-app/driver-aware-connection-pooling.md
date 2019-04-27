---
title: 드라이버 인식 연결 풀링 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ea4643354990ad416ac3975467c5991842adacc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62658263"
---
# <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링
드라이버 인식 연결 풀링는 Windows 8의 드라이버 관리자의 새로운 기능입니다. 드라이버 인식 연결 풀링 드라이버 작성자를 연결 풀링 해당 ODBC 드라이버의 동작을 사용자 지정할 수 있습니다.  
  
> [!NOTE]  
>  커서 라이브러리를 사용 하 여 드라이버 인식 연결 풀링을 지원 되지 않습니다. 응용 프로그램 드라이버 인식 연결 풀링을 사용할 때 SQLSetConnectAttr 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.  
  
 다음과 같은 문제가 드라이버 관리자 연결 풀링 관련이 드라이버 인식 연결 풀링 주소:  
  
 **풀 조각화** The 드라이버 관리자만 돌아갑니다 연결 풀에서 새 연결 요청을의 연결 문자열을 사용 하 여 정확히 일치 하는 경우.  이유 중 하나를 정확 하 게 일치 해야 드라이버 관리자에 대 한 모든 드라이버 관련 연결 문자열 키워드 및 해당 값은 드라이버 관리자 알지 못하는 경우  그러나 일부 연결 문자열 키워드 값 (예: 데이터베이스의 이름) 드라이버 (정확한 시간 차이 데이터 원본에 따라 다름) 새 연결을 열어야 하는 데 필요한 시간 이내에 데이터베이스를 변경 될 수 있으므로 정확한 일치를 하지 필요할 수 있습니다. 및 일부 연결 특성 (예: 여 SQL_ATTR_CURRENT_CATALOG)의 차이점 (예: SQL_ATTR_LOGIN_TIMEOUT) 다른 특성의 차이 보다 변경 하는 데 시간이 더 걸릴 수 있습니다. 최저 비용, 재사용 가능한 연결 풀에서 사용 하 여 드라이버 관리자 방지도이 있습니다. 드라이버에 많은 새 연결을 만드는 경우 응용 프로그램의 성능이 떨어질 수 있습니다 및 데이터 원본 확장 가능성을 줄일 수 있습니다. 드라이버 인식 연결 풀링을 드라이버 풀 연결 요청에 대 한 연결을 다시 사용할 비용을 더 효과적으로 산정 수 있으므로 풀 조각화를 줄일 수 있습니다.  
  
 **응용 프로그램 기본 설정 없음 고려** 일부 데이터 원본의 수 효율적으로 새 연결을 엽니다 (일부 특성을 재설정에 비해), 따라서, 응용 프로그램 약간 일치 하지 않는 다시 사용 하려고 하는 대신 새 연결을 열 수도 있습니다. 느린 연결 풀 초기화 구 중 수 있음) (하지만 일부 값 재설정 확인 하 고 풀에서 연결 합니다. 하지만 일부 응용 프로그램 서버 부하를 작게 유지 하 고 올바른 동작에 대 한 불일치를 해결 하는 데 큰 비용이 있을 수 있지만 더 적은 수의 연결을 열고 수 있습니다. 드라이버 인식 연결 풀링 없이 지정할 수 없습니다이 유형의 기본 설정 효과적으로 드라이버 관리자는 모든 드라이버별 연결 특성을 인식 하지 않습니다. 드라이버 인식 연결 풀링 드라이버를를 사용자의 기본 설정에 따라 풀에서 연결을 다시 사용할의 비용을 예상 보다 잘 수 있도록 (SQLSetConnectAttr의 드라이버별 특성)을 가진 사용자 기본 설정을 가져올 수 있습니다.  
  
 드라이버 인식 연결 풀링 하는 방법에 대 한 자세한 내용은 참조 하십시오 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
## <a name="determining-driver-support"></a>드라이버 지원 확인  
 드라이버 인식 연결 풀링 드라이버를 지원 하지 않을 수 있는 선택적 기능입니다. 경우 드라이버에서 지 원하는 확인 하려면 사용 된 SQL_DRIVER_AWARE_POOLING_SUPPORTED *정보 항목* 의 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)합니다.  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링을 사용 하도록 설정 하는 방법  
 응용 프로그램을 사용 하 여 SQL_CP_DRIVER_AWARE SQL_ATTR_CONNECTION_POOLING 특성을 설정 하 여 드라이버 인식 연결 풀링를 사용할 수 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)합니다. 드라이버는 연결 풀 인식을 지원 하지 않으면 드라이버 관리자 연결 풀링 사용 됩니다 (동일한 SQL_CP_ONE_PER_HENV 지정 된 것을 SQL_CP_DRIVER_AWARE 대신 처럼). ODBC 2.x 및 3.x 응용 프로그램은이 기능을 설정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
