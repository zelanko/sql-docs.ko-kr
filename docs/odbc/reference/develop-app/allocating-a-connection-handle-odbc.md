---
title: "ODBC 연결 핸들 할당 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678ba0fa4e256402e9fc25e2e4e60ba4877c6c44
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="allocating-a-connection-handle-odbc"></a>ODBC 연결 핸들 할당
응용 프로그램은 데이터 원본이 나 드라이버에 연결할 수, 먼저 다음과 같이 연결 핸들을 할당 해야 합니다.  
  
1.  응용 프로그램 SQLHDBC 형식의 변수를 선언합니다. 그런 다음 연속 호출 **SQLAllocHandle** 하 고이 변수를 sql_handle_dbc 라는 옵션 및 연결을 할당 하는 환경 핸들의 주소를 전달 합니다. 예를 들어  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  드라이버 관리자는 문에 대 한 정보를 저장 하는 구조를 할당 하 고 변수에 연결 핸들을 반환 합니다.  
  
 드라이버 관리자를 호출 하지 않습니다 **SQLAllocHandle** 이 드라이버에서 호출 하는 드라이버를 모르기 때문에 시간입니다. 전화를 연기 **SQLAllocHandle** 응용 프로그램 데이터 원본에 연결 하는 함수를 호출할 때까지 드라이버에서 합니다. 자세한 내용은 참조 [연결 과정에서 드라이버 관리자의 역할](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)이 섹션의 뒷부분에 나오는 합니다.  
  
 연결 핸들을 할당 하는 드라이버 로드와 동일 하 게 하는 것이 유용 합니다. 연결 함수를 호출할 때까지 드라이버가 로드 되지 않습니다. 따라서 연결 핸들을 할당 한 후와 드라이버 또는 데이터 원본에 연결 하기 전에 응용 프로그램 연결 핸들 사용 하 여 호출할 수의 유일한 함수는, **SQLSetConnectAttr**, **SQLGetConnectAttr**, 또는 **SQLGetInfo** SQL_ODBC_VER 옵션을 사용 합니다. 와 같은 연결 핸들을 사용 하 여 다른 함수를 호출 **SQLEndTran**, SQLSTATE 08003 (열려 있지 않습니다. 연결)를 반환 합니다. 자세한 내용은 참조 하십시오. [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
 연결 핸들에 대 한 자세한 내용은 참조 [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)합니다.

