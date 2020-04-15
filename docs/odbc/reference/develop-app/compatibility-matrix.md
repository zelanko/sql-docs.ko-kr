---
title: 호환성 매트릭스 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0406599e1657a900d1669861572ff13834cec670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307456"
---
# <a name="compatibility-matrix"></a>호환성 매트릭스
다음 표에서는 이 섹션에서 이전에 정의한 응용 프로그램 및 드라이버 유형의 호환성에 대해 설명합니다.  
  
|애플리케이션 종류<br /><br /> 및 버전|32비트 ODBC<br /><br /> *2.x* 드라이버|ODBC *3.x*<br /><br /> 드라이버|ODBC 3.8 드라이버|ISO 및 개방형 그룹 준수 드라이버|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 비트 응용 프로그램, 모든 버전|호환 가능|호환 가능|호환 가능|호환 가능|  
|순수 *2.x* 응용 프로그램|호환 가능|호환 가능|호환 가능|호환되지 않음[3]|  
|순수 *2.x* 다시 컴파일된 응용 프로그램|호환 가능|호환[1]|호환[1]|호환되지 않음[3]|  
|순수 *2.x* 유니코드 응용 프로그램|호환 가능|호환[1]|호환[1]|호환되지 않음[3]|  
|순수 개방형 그룹 및 ISO 준수 애플리케이션|호환되지 않음|호환[2]|호환[2]|호환[2]|  
|퓨어 3.0 애플리케이션|호환되지 않음|호환 가능|호환 가능|호환되지 않음[4]|  
|순수 3.5 응용 프로그램|호환되지 않음|호환 가능|호환 가능|호환되지 않음[4]|  
|순수 3.8(이상) 애플리케이션|호환되지 않음 [5]|호환되지 않음 [5]|호환 가능|호환되지 않음 [4]|  
|대체된 응용 프로그램|호환 가능|호환 가능|호환 가능|호환되지 않음[3]|  
  
 [1] 응용 프로그램은 UNICODE 옵션(유니코드 응용 프로그램인 경우)을 사용하여 ODBC 3.5(또는 그 이상) 헤더를 사용하여 다시 컴파일해야 하며 ODBCVER를 0x0250으로 설정해야 합니다.  
  
 [2] 응용 프로그램은 ODBC 3.5(또는 그 이상) 헤더를 사용하여 컴파일하고 ODBC 드라이버 관리자와 연결해야 합니다. 또한 헤더 플래그를 ODBC_STD 설정해야 합니다.  
  
 [3] ODBC *2.x에는* 책갈피와 같은 표준에 없는 기능이 있기 때문에 이 구성이 작동하지 않을 수 있습니다.  
  
 [4] ODBC *3.x에는* 책갈피와 같은 표준에 없는 기능이 있기 때문에 이 구성이 작동하지 않을 수 있습니다.  
  
 [5] ODBC 2.x 또는 3.x 드라이버에 없는 ODBC 3.8 또는 ODBC의 드라이버별 C 데이터 유형과 같은 기능이 있기 때문에 이 [구성이 실패할](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)수 있습니다.  
  
## <a name="driver-manager-compatibility"></a>드라이버 관리자 호환성  
 모든 드라이버 관리자 버전에서 작동해야 하는 ODBC 3.0 응용 프로그램은 시작 시 다음을 수행해야 합니다.  
  
-   환경 핸들을 할당합니다.  
  
-   SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC3_80 설정합니다. 드라이버 관리자가 SQL_ERROR 반환하는 경우 드라이버 관리자는 3.8보다 오래됩니다. 드라이버 관리자에 해당하도록 SQL_OV_ODBC3 또는 SQL_OV_ODBC2 SQL_ATTR_ODBC_VERSION 재설정합니다.  
  
-   연결 핸들을 할당합니다.  
  
-   연결을 만드십시오.  
  
-   드라이버 버전을 확인 하려면 SQL_DRIVER_ODBC_VER 대 한 SQLGetInfo 를 호출 합니다. 드라이버가 ODBC 3.8 드라이버인 경우 드라이버별 C 유형을 사용할 수 있습니다. 그렇지 않으면 드라이버 별 C 데이터 형식을 사용하지 마십시오.  
  
 다시 컴파일된 ODBC 3.x 응용 프로그램은 SQL_ATTR_ODBC_VERSION 대한 SQL_OV_ODBC3_80 지정하지 않고 드라이버별 C 유형 이외의 ODBC 3.8 기능을 사용할 수 있습니다. 이는 ODBC 3.x 기능을 사용하여 다시 컴파일된 ODBC 2.x 응용 프로그램과 유사합니다.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>모든 드라이버 관리자와 호환되는 응용 프로그램에서 SQLCancelHandle 사용  
 [SQLCancelHandle 함수는](../../../odbc/reference/syntax/sqlcancelhandle-function.md) Windows 7 이전에 릴리스된 드라이버 관리자에서 지원되지 않으므로 **SQLCancelHandle을** 직접 호출하는 경우 이전 버전의 Windows에서 응용 프로그램을 로드할 수 없습니다. 모든 버전의 드라이버 관리자와 함께 작업하고 새 버전의 Windows에서 **SQLCancelHandle을** 사용하려면 응용 프로그램이 **LoadLibrary** 및 **GetProcAddress를** 사용하여 **SQLCancelHandle을** 간접적으로 호출해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
