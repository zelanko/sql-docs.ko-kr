---
title: "환경 핸들 할당 | Microsoft Docs"
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
- ODBC drivers [ODBC], environment handles
- allocating environment handles [ODBC]
- connecting to driver [ODBC], environment handles
- environment handles [ODBC]
- data sources [ODBC], environment handles
- connecting to data source [ODBC], environment handles
- handles [ODBC], environment
ms.assetid: 77b5d1d6-7eb7-428d-bf75-a5c5a325d25c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 322978a4006460fc61a438c6aff5ed8eca0c6c93
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="allocating-the-environment-handle"></a>환경 핸들 할당
모든 ODBC 응용 프로그램에 대 한 첫 번째 작업은 드라이버 관리자; 로드 이 과정은 운영 체제 따라 다릅니다. 예를 들어 Microsoft® Windows NT® 서버/Windows 2000 Server, Windows NT 워크스테이션/Windows 2000 Professional 또는 Microsoft Windows® 95/98을 실행 하는 컴퓨터에서 응용 프로그램 중 하나에 연결 드라이버 관리자 라이브러리 또는 호출  **LoadLibrary** 드라이버 관리자 DLL을 로드할 수 있습니다.  
  
 다음 태스크에서는 응용 프로그램이 다른 ODBC 함수를 호출할 수 전에 수행 해야, ODBC 환경을 초기화 다음과 같이 환경 핸들을 할당 하는 것입니다.  
  
1.  응용 프로그램 SQLHENV 형식의 변수를 선언합니다. 그런 다음 연속 호출 **SQLAllocHandle** 하 고이 변수 및 SQL_HANDLE_ENV 옵션의 주소를 전달 합니다. 예를 들어  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  드라이버 관리자는 환경에 대 한 정보를 저장 하는 구조를 할당 하 고 변수에 환경 핸들을 반환 합니다.  
  
 드라이버 관리자를 호출 하지 않습니다 **SQLAllocHandle** 이 드라이버에서 호출 하는 드라이버를 모르기 때문에 시간입니다. 전화를 연기 **SQLAllocHandle** 응용 프로그램 데이터 원본에 연결 하는 함수를 호출할 때까지 드라이버에서 합니다. 자세한 내용은 참조 [연결 과정에서 드라이버 관리자의 역할](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)이 섹션의 뒷부분에 나오는 합니다.  
  
 ODBC를 사용 하 여 응용 프로그램이 완료 되 면 환경 핸들을 해제 **SQLFreeHandle**합니다. 환경을 확보 한 후는 ODBC 함수;에 대 한 호출에서 환경 핸들을 사용 하려는 프로그래밍 오류 응용 프로그램 이렇게 하면 되므로 결과가 정의 되지 않은 있지만 아마도 심각한 됩니다.  
  
 때 **SQLFreeHandle** 호출 되는 드라이버 릴리스 구조는 환경에 대 한 정보를 저장 하는 데 사용 합니다. **SQLFreeHandle** 해당 환경 핸들의 모든 연결 핸들 해제 된 후까지 환경 핸들에 대해 호출할 수 없습니다.  
  
 환경 핸들에 대 한 자세한 내용은 참조 [환경 처리](../../../odbc/reference/develop-app/environment-handles.md)합니다.

