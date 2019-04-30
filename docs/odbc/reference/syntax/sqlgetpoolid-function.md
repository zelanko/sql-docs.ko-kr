---
title: SQLGetPoolID 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39b3d3d1ecdc21acee8b238f56cede0a59146bd2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132704"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수 합니다. ODBC  
  
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
 [입력] 모든 연결 정보를 포함 하는 토큰 핸들입니다.  
  
 *pPoolID*  
 [출력] 서로 교환해 서 사용할 수 있는 연결 집합을 식별 하는 데 사용 되는 풀 ID (추가 재설정 필요할 수도 있음).  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetPoolID** 반환 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 드라이버 관리자를 사용 하 여를 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN의와 **처리** 의*hDbcInfoToken*합니다.  
  
## <a name="remarks"></a>Remarks  
 **SQLGetPoolID** 연결 정보 집합이 지정 된 풀 ID를 가져오는 데 사용 됩니다 (에서 **SQLSetConnectAttrForDbcInfo**하십시오 **SQLSetDriverConnectInfo**, 및  **SQLSetConnectInfo**). ID는 서로 교환해 서 사용할 수 있는 연결 집합을 식별 하는이 풀 (추가 재설정 필요할 수도 있음). 풀 ID 연결의 해당 그룹에 대 한 연결 풀 식별에 사용 됩니다.  
  
 드라이버는 SQL_ERROR 또는 SQL_INVALID_HANDLE 반환 될 때마다 응용 프로그램에 드라이버 관리자 오류를 반환 합니다 (에서 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 하거나 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)).  
  
 드라이버에서 SQL_SUCCESS_WITH_INFO를 반환할 때마다 드라이버 관리자에서 진단 정보를 가져옵니다 *hDbcInfoToken*, 응용 프로그램에 SQL_SUCCESS_WITH_INFO를 반환 하 고 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)하 고 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)합니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발을 위한 sqlspi.h 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
