---
title: 연결 핸들 ODBC 할당 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12e9f65ee81612e269c1f86ebabd049588443cb8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288523"
---
# <a name="allocating-a-connection-handle-odbc"></a>연결 핸들 ODBC 할당
응용 프로그램이 데이터 원본 또는 드라이버에 연결하려면 다음과 같이 연결 핸들을 할당해야 합니다.  
  
1.  응용 프로그램은 SQLHDBC 형식의 변수를 선언합니다. 그런 다음 **SQLAllocHandle을** 호출하고 이 변수의 주소, 연결을 할당할 환경의 핸들 및 SQL_HANDLE_DBC 옵션을 전달합니다. 다음은 그 예입니다.  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  드라이버 관리자는 명령문에 대한 정보를 저장하는 구조를 할당하고 변수에 연결 핸들을 반환합니다.  
  
 드라이버 관리자는 호출할 드라이버를 알 수 없으므로 현재 드라이버에서 **SQLAllocHandle을** 호출하지 않습니다. 응용 프로그램이 데이터 원본에 연결하는 함수를 호출할 때까지 드라이버에서 **SQLAllocHandle** 호출이 지연됩니다. 자세한 내용은 [연결 프로세스의 드라이버 관리자 역할,](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)이 섹션의 다음 을 참조하십시오.  
  
 연결 핸들을 할당하는 것은 드라이버 로드와 다다. 연결 함수가 호출될 때까지 드라이버가 로드되지 않습니다. 따라서 연결 핸들을 할당하고 드라이버 또는 데이터 원본에 연결하기 전에 응용 프로그램이 연결 핸들과 함께 호출할 수 있는 유일한 함수는 **SQLSetConnectAttr,** **SQLGetConnectAttr**또는 SQL_ODBC_VER 옵션을 사용하여 **SQLGetInfo입니다.** **SQLEndTran과**같은 연결 핸들을 가진 다른 함수를 호출하면 SQLSTATE 08003(연결이 열리지 않음)이 반환됩니다. 자세한 내용은 [부록 B: ODBC 상태 전환 테이블을](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조하십시오.  
  
 연결 핸들에 대한 자세한 내용은 [연결 핸들을](../../../odbc/reference/develop-app/connection-handles.md)참조하십시오.
