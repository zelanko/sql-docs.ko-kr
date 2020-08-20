---
description: 호환성 매트릭스
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bafe3d85e1f4dc1c18acb057fe8c00e4ca0b36d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461565"
---
# <a name="compatibility-matrix"></a>호환성 매트릭스
다음 표에서는이 섹션에서 이전에 정의 된 응용 프로그램 및 드라이버 형식의 호환성에 대해 설명 합니다.  
  
|애플리케이션 종류<br /><br /> 및 버전|32 비트 ODBC<br /><br /> *2.x* 2.x 드라이버|ODBC *3.x*<br /><br /> 요소|ODBC 3.8 드라이버|ISO 및 오픈 그룹 호환 드라이버|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 비트 응용 프로그램, 모든 버전|호환 가능|호환 가능|호환 가능|호환 가능|  
|순수형 *2.x* 응용 프로그램|호환 가능|호환 가능|호환 가능|호환 되지 않음 [3]|  
|순수 *2.x* 다시 컴파일된 응용 프로그램|호환 가능|호환 [1]|호환 [1]|호환 되지 않음 [3]|  
|순수한 *2.X* 유니코드 응용 프로그램|호환 가능|호환 [1]|호환 [1]|호환 되지 않음 [3]|  
|순수 개방 그룹 및 ISO 규격 응용 프로그램|호환되지 않음|호환 [2]|호환 [2]|호환 [2]|  
|순수한 3.0 응용 프로그램|호환되지 않음|호환 가능|호환 가능|호환 되지 않음 [4]|  
|순수한 3.5 응용 프로그램|호환되지 않음|호환 가능|호환 가능|호환 되지 않음 [4]|  
|순수한 3.8 이상 응용 프로그램|호환 되지 않음 [5]|호환 되지 않음 [5]|호환 가능|호환 되지 않음 [4]|  
|바뀐 응용 프로그램|호환 가능|호환 가능|호환 가능|호환 되지 않음 [3]|  
  
 [1] 응용 프로그램은 유니코드 옵션 (유니코드 응용 프로그램의 경우)을 사용 하 여 ODBC 3.5 이상 헤더를 사용 하 여 다시 컴파일한 다음 ODBCVER를 0x0250으로 설정 해야 합니다.  
  
 [2] 응용 프로그램은 odbc 3.5 이상 헤더를 사용 하 여 컴파일하고 ODBC 드라이버 관리자와 연결 해야 합니다. 또한 헤더 플래그 ODBC_STD 설정 해야 합니다.  
  
 [3]이 구성은 책갈피와 같이 표준에 있지 *않은 ODBC 2.x* 의 기능이 있기 때문에 잠재적으로 작동 하지 않을 수 있습니다.  
  
 [4]이 구성은 책갈피와 같이 표준에 있지 *않은 ODBC 3.x* 의 기능이 있기 때문에 잠재적으로 작동 하지 않을 수 있습니다.  
  
 [5] odbc의 드라이버 관련 [C 데이터 형식과](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)같은 odbc 3.8 또는 2.x 드라이버가 아닌 odbc의 기능이 있으므로이 구성은 잠재적으로 실패할 수 있습니다.  
  
## <a name="driver-manager-compatibility"></a>드라이버 관리자 호환성  
 모든 드라이버 관리자 버전에서 작동 해야 하는 ODBC 3.0 응용 프로그램은 시작 시 다음을 수행 해야 합니다.  
  
-   환경 핸들을 할당 합니다.  
  
-   SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC3_80로 설정 합니다. 드라이버 관리자가 SQL_ERROR 반환 하는 경우 드라이버 관리자는 3.8 보다 이전 버전입니다. 드라이버 관리자에 해당 하는 SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3 또는 SQL_OV_ODBC2으로 다시 설정 합니다.  
  
-   연결 핸들을 할당 합니다.  
  
-   연결을 설정 합니다.  
  
-   SQL_DRIVER_ODBC_VER에 대해 SQLGetInfo를 호출 하 여 드라이버 버전을 확인 합니다. 드라이버가 ODBC 3.8 드라이버 이면 드라이버 특정 C 유형을 사용할 수 있습니다. 그렇지 않으면 드라이버 관련 C 데이터 형식을 사용 하지 마십시오.  
  
 다시 컴파일된 ODBC 3(sp3) 응용 프로그램은 SQL_ATTR_ODBC_VERSION에 대 한 SQL_OV_ODBC3_80를 지정 하지 않고 드라이버 관련 C 형식 이외의 ODBC 3.8 기능을 사용할 수 있습니다. 이는 ODBC 3.x 기능을 사용 하 여 다시 컴파일된 ODBC 2.x 응용 프로그램과 유사 합니다.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>모든 드라이버 관리자와 호환 되는 응용 프로그램에서 SQLCancelHandle 사용  
 Windows 7 이전에 릴리스된 드라이버 관리자에서는 [Sqlcancelhandle 함수가](../../../odbc/reference/syntax/sqlcancelhandle-function.md) 지원 되지 않으므로 **sqlcancelhandle** 을 직접 호출 하는 경우에는 이전 버전의 Windows에서 응용 프로그램을 로드할 수 없습니다. 모든 버전의 드라이버 관리자를 사용 하 여 새 버전의 Windows에서 **Sqlcancelhandle** 을 사용 하려면 응용 프로그램이 **LoadLibrary** 및 GetProcAddress를 사용 하 여 간접적으로 **sqlcancelhandle** 을 호출 해야 합니다 **.**  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
