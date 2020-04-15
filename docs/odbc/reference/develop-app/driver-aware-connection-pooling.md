---
title: 드라이버 인식 연결 풀링 | 마이크로 소프트 문서
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
ms.openlocfilehash: 70b70c841f37bd69179137c807c0dadcfd932d2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287603"
---
# <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링
드라이버 인식 연결 풀링은 Windows 8의 드라이버 관리자의 새로운 기능입니다. 드라이버 인식 연결 풀링을 사용하면 드라이버 작성자가 ODBC 드라이버에서 연결 풀링 동작을 사용자 지정할 수 있습니다.  
  
> [!NOTE]  
>  드라이버 인식 연결 풀링은 커서 라이브러리에서 지원되지 않습니다. 드라이버 인식 연결 풀링이 활성화된 경우 SQLSetConnectAttr을 통해 커서 라이브러리를 사용하도록 설정하려고 하면 응용 프로그램이 오류 메시지를 받게 됩니다.  
  
 드라이버 인식 연결 풀링은 드라이버 관리자 연결 풀링과 관련된 다음과 같은 문제를 해결합니다.  
  
 **풀 조각화** 드라이버 관리자는 새 연결 요청의 연결 문자열과 정확히 일치하는 경우에만 풀에서 연결을 반환합니다.  드라이버 관리자가 정확한 일치를 요구하는 한 가지 이유는 드라이버 관리자가 모든 드라이버 관련 연결 문자열 키워드와 해당 값을 이해하지 못하기 때문입니다.  그러나 일부 연결 문자열 키워드 값(예: 데이터베이스 이름)은 드라이버가 새 연결을 여는 데 필요한 시간보다 적은 시간 이내에 데이터베이스를 변경할 수 있기 때문에 정확한 일치가 필요하지 않을 수 있습니다(정확한 시간 차이는 데이터 원본에 따라 다름). 또한 일부 연결 특성(예: SQL_ATTR_CURRENT_CATALOG)의 차이는 다른 특성(예: SQL_ATTR_LOGIN_TIMEOUT)의 차이보다 변경하는 데 더 많은 시간이 걸릴 수 있습니다. 이렇게 하면 드라이버 관리자가 풀에서 가장 저렴한 재사용 가능한 연결을 사용하지 못할 수 있습니다. 드라이버가 많은 새 연결을 만들어야 하는 경우 응용 프로그램의 성능이 저하되고 데이터 원본 확장성이 저하될 수 있습니다. 드라이버가 연결 요청에 대해 풀에서 연결을 재사용하는 비용을 더 잘 예측할 수 있으므로 드라이버 인식 연결 풀링을 사용하여 풀 조각화를 줄일 수 있습니다.  
  
 **응용 프로그램 기본 설정 고려 없음** 일부 데이터 원본은 새 연결을 효율적으로 열 수 있으므로(일부 특성을 재설정하는 경우) 응용 프로그램은 풀에서 약간 일치하지 않는 연결을 재사용하고 일부 값을 재설정하는 대신 새 연결을 여는 것을 선호할 수 있습니다(연결 풀 초기화 구에서는 속도가 느려질 수 있음). 그러나 일부 응용 프로그램은 올바른 동작에 대한 불일치를 해결하는 데 더 큰 비용이 들 수 있지만 서버 로드를 줄이고 연결을 더 적게 열 수 있습니다. 드라이버 인식 연결 풀링이 없으면 드라이버 관리자가 모든 드라이버 별 연결 특성을 인식하지 않으므로 이러한 종류의 기본 설정을 효과적으로 지정할 수 없습니다. 드라이버 인식 연결 풀링을 사용하면 드라이버가 사용자 기본 설정(SQLSetConnectAttr의 드라이버 별 특성 사용)을 얻을 수 있으므로 사용자의 기본 설정에 따라 풀에서 연결을 다시 사용하는 비용을 더 잘 예측할 수 있습니다.  
  
 드라이버 인식 연결 풀링에 대한 자세한 내용은 [ODBC 드라이버에서 연결-풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)을 참조하십시오.  
  
## <a name="determining-driver-support"></a>드라이버 지원 결정  
 드라이버 인식 연결 풀링은 드라이버가 지원하지 않을 수 있는 선택적 기능입니다. 드라이버가 지원하는지 확인하려면 [SQLGetInfo의](../../../odbc/reference/syntax/sqlgetinfo-function.md) *SQL_DRIVER_AWARE_POOLING_SUPPORTED InfoType을* 사용합니다.  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링을 활성화하는 방법  
 응용 프로그램은 [SQLSetEnvAttr을](../../../odbc/reference/syntax/sqlsetenvattr-function.md)사용하여 SQL_CP_DRIVER_AWARE SQL_ATTR_CONNECTION_POOLING 특성을 설정하여 드라이버의 연결 풀링 인식을 사용할 수 있습니다. 드라이버가 연결 풀 인식을 지원하지 않는 경우 드라이버 관리자 연결 풀링이 사용됩니다(SQL_CP_DRIVER_AWARE 대신 SQL_CP_ONE_PER_HENV 지정된 것과 동일). ODBC 2.x 및 3.x 응용 프로그램에서이 기능을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
