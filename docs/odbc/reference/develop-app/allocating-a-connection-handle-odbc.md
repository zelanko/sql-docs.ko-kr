---
title: 연결 핸들 할당 ODBC | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 83964bf1e76eef5c7c4ba4121b0c581e8d8a406b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288322"
---
# <a name="allocating-a-connection-handle-odbc"></a>연결 핸들 ODBC 할당
응용 프로그램에 연결할 수는 데이터 원본이 나 드라이버 전에 다음과 같이 연결 핸들을 할당 해야 합니다.  
  
1.  응용 프로그램 SQLHDBC 형식의 변수를 선언합니다. 그런 다음 호출 **SQLAllocHandle** 하 고이 변수를 SQL_HANDLE_DBC 옵션과 연결을 할당 하는 환경의 핸들의 주소를 전달 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    SQLHDBC hdbc1;  
  
    SQLAllocHandle(SQL_HANDLE_DBC, henv1, &hdbc1);  
    ```  
  
2.  드라이버 관리자는 문에 대 한 정보를 저장 하는 구조체를 할당 하 고 변수에 연결 핸들을 반환 합니다.  
  
 드라이버 관리자를 호출 하지 않습니다 **SQLAllocHandle** 이 드라이버에서 호출 하는 드라이버를 알지 못하므로 시간입니다. 호출 하는 작업이 지연 **SQLAllocHandle** 드라이버 응용 프로그램 데이터 원본에 연결 하는 함수를 호출할 때까지 합니다. 자세한 내용은 [연결 프로세스에서 드라이버 관리자의 역할](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)이 섹션의 뒷부분에 나오는.  
  
 연결 핸들을 할당 하는 드라이버 로드와 동일 하 게 하는 것이 반드시 합니다. 드라이버는 연결 함수를 호출할 때까지 로드 되지 않습니다. 따라서 연결 핸들을 할당 한 후 드라이버 또는 데이터 원본에 연결 하기 전에, 함수만 응용 프로그램 연결 핸들을 사용 하 여 호출할 수와 **SQLSetConnectAttr**, **SQLGetConnectAttr**, 또는 **SQLGetInfo** SQL_ODBC_VER 옵션을 사용 합니다. 와 같은 연결 핸들을 사용 하 여 다른 함수를 호출 **SQLEndTran**, SQLSTATE 08003 (열려 있지 않은 연결)를 반환 합니다. 자세한 내용은 참조 하세요. [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
 연결 핸들에 대 한 자세한 내용은 참조 하세요. [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)합니다.
