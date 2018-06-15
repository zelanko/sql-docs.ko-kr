---
title: 드라이버 인식 연결 풀링 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2efa24f11f174c77ebe7f289019b0544f65d0c2d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912680"
---
# <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링
드라이버 인식 연결 풀링는 Windows 8의 드라이버 관리자의 새로운 기능입니다. 드라이버 인식 연결 풀링 드라이버 작성자를 풀링 동작의 ODBC 드라이버에서 연결을 사용자 지정할 수 있습니다.  
  
> [!NOTE]  
>  커서 라이브러리 드라이버 인식 연결 풀링 지원 되지 않습니다. 응용 프로그램이 드라이버 인식 연결 풀링을 사용할 때 SQLSetConnectAttr 통해 커서 라이브러리를 사용 하도록 설정 하려고 하면 오류 메시지가 표시 됩니다.  
  
 드라이버 관리자 연결 풀에 관련 된 다음과 같은 문제가 드라이버 인식 연결 풀링 주소:  
  
 **풀 조각화** The 드라이버 관리자는 반환 연결 풀에서 새 연결 요청의 연결 문자열과 함께 정확히 일치 하는 경우.  하나의 이유 정확 하 게 일치 하는 값을 요구 하도록 드라이버 관리자에 대 한 모든 드라이버 관련 연결 문자열 키워드와 해당 값은 드라이버 관리자를 인식 하지 못하는입니다.  그러나 일부 연결 문자열 키워드 값 (예: 데이터베이스의 이름) 드라이버 (정확한 시간 차이 데이터 원본에 따라 다름) 새 연결을 열어야 하는 데 필요한 시간 이내에 데이터베이스를 변경할 수 있으므로 정확 하 게 일치 하는 필요 하지 않을 수 있습니다. 및 일부 연결 특성 SQL_ATTR_CURRENT_CATALOG) (등의 차이는 다른 특성 (예: SQL_ATTR_LOGIN_TIMEOUT)의 차이 보다 변경 하는 데 시간이 더 걸릴 수 있습니다. 이 너무, 않으려면 드라이버 관리자 최저 비용, 다시 사용할 수 있는 연결 풀에서 사용 하 여 합니다. 드라이버에 있는 많은 새 연결을 만드는 경우 응용 프로그램의 성능이 떨어질 수 있습니다 및 데이터 원본 확장 가능성을 줄일 수 있습니다. 드라이버 인식 연결 풀링을 드라이버는 연결 요청에 대 한 풀에서 연결을 다시 사용의 비용을 예측 더 잘 수 있으므로 풀 조각화를 줄일 수 있습니다.  
  
 **응용 프로그램 기본 설정에 고려** 일부 데이터 원본의 수 효율적으로 새 연결을 엽니다 (일부 특성을 다시 설정에 비해), 하므로, 응용 프로그램을 약간 일치 하지 않는 다시 사용 하려고 하는 대신 새 연결을 열려는 것이 적절할 수 연결 풀에서 다시 설정 (느린 연결 풀 초기화 구 하는 동안 수 있음) 되지만 일부 값입니다. 하지만 일부 응용 프로그램 서버 부하를 더 작게 유지 하 고 올바른 동작에 대 한 불일치를 해결 하려면 더 큰 비용 있을 수 있지만 적은 수의 연결을 열 수 있습니다. 드라이버 인식 연결 풀링 없이 지정할 수 없습니다 이러한 유형의 기본 설정으로 효율적으로 드라이버 관리자는 모든 드라이버별 연결 특성을 인식 하지 않으므로 합니다. 드라이버 인식 연결 풀링 드라이버를를 사용자의 기본 설정에 따라 풀에서 연결이 다시 사용의 비용을 예상 보다 잘 수 있도록 (SQLSetConnectAttr의 드라이버별 특성)을 가진 사용자 기본 설정을 가져올 수 있습니다.  
  
 드라이버 인식 연결 풀링 하는 방법에 대 한 자세한 내용은 참조 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
## <a name="determining-driver-support"></a>드라이버 지원 여부 확인  
 드라이버 인식 연결 풀링 드라이버 지원 되지 않을 수 있는 선택적 기능입니다. SQL_DRIVER_AWARE_POOLING_SUPPORTED 사용 경우 드라이버에서 지 원하는 확인 하려면 *정보 항목* 의 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)합니다.  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링을 사용 하는 방법  
 응용 프로그램 צ ְ ײ는 드라이버 인식 연결 풀링으로 SQL_CP_DRIVER_AWARE를 SQL_ATTR_CONNECTION_POOLING 특성을 설정 하 여 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)합니다. 드라이버 인식 연결 풀을 지원 하지 않으면 드라이버 관리자 연결 풀링 사용 됩니다 (SQL_CP_ONE_PER_HENV 지정 된, SQL_CP_DRIVER_AWARE 대신 하는 경우 같음). ODBC 2.x 및 3.x 응용 프로그램에서는이 기능을 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
