---
title: SQLGetPoolID 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec2da5abd62e659529eb364c7673317c86f4c97e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLGetPoolID** 풀 ID를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>인수  
 *hDbcInfoToken*  
 [입력] 모든 연결 정보가 포함 된 토큰 핸들입니다.  
  
 *pPoolID*  
 [출력] 풀 ID를 교대로 사용 될 수 있는 연결의 집합을 식별 하는 데 사용 됩니다 (추가 재설정 해야 할 수)입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetPoolID** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 드라이버 관리자는를 사용 하 여 한 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의 및 **처리** 의*hDbcInfoToken*합니다.  
  
## <a name="remarks"></a>주의  
 **SQLGetPoolID** 연결 정보 집합이 제공 된 풀 ID를 가져오는 데 사용 됩니다 (에서 **SQLSetConnectAttrForDbcInfo**, **SQLSetDriverConnectInfo**, 및  **SQLSetConnectInfo**). ID를 사용 하 여 교대로 사용 될 수 있는 연결의 집합을 식별 하는이 풀 (추가 재설정 해야 할 수)입니다. 연결의 해당 그룹에 대 한 연결 풀을 식별 하는 풀 ID 사용 됩니다.  
  
 드라이버 관리자 응용 프로그램에 오류를 반환 하는 드라이버 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 (에서 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 또는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 드라이버 관리자의 진단 정보를 가져옵니다는 드라이버에서 SQL_SUCCESS_WITH_INFO를 반환할 때마다 *hDbcInfoToken*, 응용 프로그램에 sql_success_with_info가 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)및 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지원 되는 ODBC 드라이버가이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발에 대 한 sqlspi.h를 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
