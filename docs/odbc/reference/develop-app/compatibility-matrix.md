---
title: 호환성 매트릭스 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 273633532b9b9247ea7aa12fe90bfcc3c6f6bb81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083272"
---
# <a name="compatibility-matrix"></a>호환성 매트릭스
다음 표에서 응용 프로그램 및 드라이버를이 단원의 이전에 정의 된 유형의의 호환성을 설명 합니다.  
  
|응용 프로그램 유형<br /><br /> 및 버전|32 비트 ODBC<br /><br /> *2.x* 드라이버|ODBC *3.x*<br /><br /> 드라이버|ODBC 3.8 드라이버|ISO 및 열린 그룹 규격 드라이버|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 비트 응용 프로그램, 모든 버전|호환성|호환성|호환성|호환성|  
|순수 *2.x* 응용 프로그램|호환성|호환성|호환성|하지 호환 되는 [3]|  
|순수 *2.x* 응용 프로그램을 다시 컴파일|호환성|호환 되는 [1]|호환 되는 [1]|하지 호환 되는 [3]|  
|순수 *2.x* 유니코드 응용 프로그램|호환성|호환 되는 [1]|호환 되는 [1]|하지 호환 되는 [3]|  
|순수 Open Group 및 ISO 호환 응용 프로그램|호환 되지 않습니다.|호환 되는 [2]|호환 되는 [2]|호환 되는 [2]|  
|순수 3.0 응용 프로그램|호환 되지 않습니다.|호환성|호환성|하지 호환 [4]|  
|순수 3.5 응용 프로그램|호환 되지 않습니다.|호환성|호환성|하지 호환 [4]|  
|순수 3.8 (또는 이상) 응용 프로그램|하지 호환 [5]|하지 호환 [5]|호환성|하지 호환 [4]|  
|대체 응용 프로그램|호환성|호환성|호환성|하지 호환 되는 [3]|  
  
 [1] 응용 프로그램 (응용 프로그램을 유니코드 경우) 유니코드 옵션을 사용 하 여 ODBC 3.5 (또는 이상) 헤더를 사용 하 여 컴파일해야 ODBCVER 0x0250를 설정 해야 합니다.  
  
 [2]에서 응용 프로그램 ODBC 3.5 (또는 이상) 헤더를 사용 하 여 컴파일하고 하 고 ODBC 드라이버 관리자를 사용 하 여 연결 해야 합니다. 또한 ODBC_STD 헤더 플래그를 설정 합니다.  
  
 [3]이이 구성은 ODBC에는 기능이 하므로 실패할 가능성이 *2.x* 책갈피와 같은 표준에 없는 합니다.  
  
 [4]이이 구성은 ODBC에는 기능이 하므로 실패할 가능성이 *3.x* 책갈피와 같은 표준에 없는 합니다.  
  
 [5]이이 구성은 ODBC 2.x 또는 3.x와 같은 드라이버를 드라이버 관련 되지 않는 기능 ODBC 3.8에 있기 때문에 실패할 가능성이 [odbc에서 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.  
  
## <a name="driver-manager-compatibility"></a>드라이버 관리자 호환성  
 모든 드라이버 관리자 버전을 사용 하 여 작동 해야 하는 ODBC 3.0 응용 프로그램 시작 시 다음을 수행 해야 합니다.  
  
-   환경 핸들을 할당 합니다.  
  
-   SQL_OV_ODBC3_80를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 합니다. 드라이버 관리자는 SQL_ERROR를 반환 하면 드라이버 관리자 3.8 보다 오래 되었습니다. SQL_OV_ODBC3 또는 SQL_OV_ODBC2를 SQL_ATTR_ODBC_VERSION 적절 하 게 해당 드라이버 관리자를 다시 설정 합니다.  
  
-   연결 핸들을 할당 합니다.  
  
-   연결을 확인 합니다.  
  
-   드라이버 버전을 확인 하는 SQL_DRIVER_ODBC_VER에 대 한 SQLGetInfo를 호출 합니다. 드라이버는 ODBC 3.8 드라이버 경우 드라이버별 C 형식을 사용할 수 있습니다. 그렇지 않은 경우 드라이버 관련 C 데이터 형식을 사용 하지 마십시오.  
  
 다시 컴파일된 ODBC 3.x 응용 프로그램을 SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3_80 지정 하지 않고 드라이버별 C 형식 이외의 ODBC 3.8 기능을 사용할 수는 참고 합니다. 다시 컴파일된 ODBC 2.x 응용 프로그램을 ODBC 3.x 기능을 사용 하는 것과 비슷합니다.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>SQLCancelHandle 호환 모든 드라이버 관리자를 사용 하 여 가능한 응용 프로그램에서 사용 하 여  
 때문에 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 지원 되지 않습니다 Windows 7 이전에 릴리스된 드라이버 관리자에서 응용 프로그램에서에서 로드할 수 없습니다 이전 버전 Windows의 호출 하는 경우 **SQLCancelHandle** 직접. 드라이버 관리자의 모든 버전을 사용 하 여 사용 **SQLCancelHandle** 새 버전의 Windows에서는 응용 프로그램에서 호출 해야 **SQLCancelHandle** 사용 하 여 직접 **LoadLibrary** 고 **GetProcAddress 합니다.**  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
