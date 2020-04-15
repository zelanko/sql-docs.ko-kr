---
title: 환경 핸들 할당 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e33b850b2786960a368720deaf89a2203c7dd159
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303006"
---
# <a name="allocating-the-environment-handle"></a>환경 핸들 할당
ODBC 응용 프로그램의 첫 번째 작업은 드라이버 관리자를 로드하는 것입니다. 운영 체제에 따라 다릅니다. 예를 들어 Microsoft® Windows NT® 서버/Windows 2000 서버, Windows NT 워크스테이션/Windows 2000 전문가 또는 Microsoft Windows® 95/98을 실행하는 컴퓨터에서 응용 프로그램은 드라이버 관리자 라이브러리에 연결되거나 **로드 라이브러리를** 호출하여 드라이버 관리자 DLL을 로드합니다.  
  
 응용 프로그램이 다른 ODBC 함수를 호출하기 전에 수행해야 하는 다음 작업은 다음과 같이 ODBC 환경을 초기화하고 환경 핸들을 할당하는 것입니다.  
  
1.  응용 프로그램은 SQLHENV 형식의 변수를 선언합니다. 그런 다음 **SQLAllocHandle을** 호출하고이 변수의 주소와 SQL_HANDLE_ENV 옵션을 전달합니다. 다음은 그 예입니다.  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  드라이버 관리자는 환경에 대한 정보를 저장할 구조를 할당하고 변수에서 환경 핸들을 반환합니다.  
  
 드라이버 관리자는 호출할 드라이버를 알 수 없으므로 현재 드라이버에서 **SQLAllocHandle을** 호출하지 않습니다. 응용 프로그램이 데이터 원본에 연결하는 함수를 호출할 때까지 드라이버에서 **SQLAllocHandle** 호출이 지연됩니다. 자세한 내용은 [연결 프로세스의 드라이버 관리자 역할,](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)이 섹션의 다음 을 참조하십시오.  
  
 응용 프로그램이 ODBC 를 사용하여 완료되면 **SQLFreeHandle**을 사용하여 환경 핸들을 해제합니다. 환경을 해제한 후 ODBC 함수를 호출할 때 환경의 핸들을 사용하는 응용 프로그램 프로그래밍 오류입니다. 이렇게 하면 정의되지 않았지만 치명적인 결과가 있을 수 있습니다.  
  
 **SQLFreeHandle이** 호출되면 드라이버는 환경에 대한 정보를 저장하는 데 사용되는 구조를 해제합니다. **SQLFreeHandle** 해당 환경 핸들에 대 한 모든 연결 핸들을 해제 될 때까지 환경 핸들에 대 한 호출할 수 없습니다.  
  
 환경 핸들에 대한 자세한 내용은 [환경 핸들을](../../../odbc/reference/develop-app/environment-handles.md)참조하십시오.
