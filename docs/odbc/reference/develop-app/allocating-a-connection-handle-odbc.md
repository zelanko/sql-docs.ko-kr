---
title: ODBC 연결 핸들을 할당 하는 중 Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- allocating connection handles [ODBC]
- data sources [ODBC], connection handles
- connecting to data source [ODBC], connection handles
- ODBC drivers [ODBC], connection handles
- connecting to driver [ODBC], connection handles
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: c99a8159-7693-4f97-8dcf-401336550e77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bd3a44fe4f0466dfcf11a72fa0377564c1cf02f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077198"
---
# <a name="allocating-a-connection-handle-odbc"></a>연결 핸들 ODBC 할당
응용 프로그램은 데이터 원본 또는 드라이버에 연결 하기 전에 다음과 같이 연결 핸들을 할당 해야 합니다.  
  
1.  응용 프로그램은 SQLHDBC 형식의 변수를 선언 합니다. 그런 다음 **SQLAllocHandle** 를 호출 하 고이 변수의 주소, 연결을 할당할 환경의 핸들 및 SQL_HANDLE_DBC 옵션을 전달 합니다. 다음은 그 예입니다.  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  드라이버 관리자는 문에 대 한 정보를 저장 하는 구조를 할당 하 고 해당 연결 핸들을 변수에 반환 합니다.  
  
 드라이버 관리자는 호출할 드라이버를 알 수 없기 때문에 지금은 드라이버에서 **SQLAllocHandle** 를 호출 하지 않습니다. 응용 프로그램이 데이터 소스에 연결 하는 함수를 호출할 때까지 드라이버에서 **SQLAllocHandle** 를 호출 하는 것이 지연 됩니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [연결 프로세스에서 드라이버 관리자의 역할](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)을 참조 하세요.  
  
 연결 핸들 할당은 드라이버를 로드 하는 것과는 다릅니다. 연결 함수가 호출 될 때까지 드라이버가 로드 되지 않습니다. 따라서 연결 핸들을 할당 한 후 드라이버 또는 데이터 원본에 연결 하기 전에 응용 프로그램에서 호출할 수 있는 함수는 SQL_ODBC_VER 옵션을 사용 하는 **SQLSetConnectAttr**, **SQLGetConnectAttr**또는 **SQLGetInfo** 입니다. **Sqlendtran**과 같이 연결 핸들을 사용 하 여 다른 함수를 호출 하면 SQLSTATE 08003 (연결이 열려 있지 않음)이 반환 됩니다. 자세한 내용은 [부록 B: ODBC 상태 전환 표](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)를 참조 하세요.  
  
 연결 핸들에 대 한 자세한 내용은 [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)을 참조 하십시오.
