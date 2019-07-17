---
title: 환경 핸들 할당 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 823ea02a2acb6a28f56c58bb40fe684a2589bd24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077179"
---
# <a name="allocating-the-environment-handle"></a>환경 핸들 할당
ODBC 응용 프로그램에 대 한 첫 번째 작업은 부하 드라이버 관리자입니다. 이 과정은 운영 체제 따라 다릅니다. 예를 들어, Microsoft® Windows NT® Server/Windows 2000 Server, Windows NT 워크스테이션/Windows 2000 Professional 또는 Microsoft Windows® 95/98을 실행 중인 컴퓨터에 응용 프로그램이 하거나 연결 드라이버 관리자 라이브러리나 호출  **LoadLibrary** 드라이버 관리자 DLL을 로드할 수 있습니다.  
  
 응용 프로그램에서 다른 ODBC 함수를 호출할 수 전에 수행 해야 합니다는 다음 태스크에서는 ODBC 환경을 초기화 환경 핸들을 다음과 같이 할당 하는 것입니다.  
  
1.  응용 프로그램 SQLHENV 형식의 변수를 선언합니다. 그런 다음 호출 **SQLAllocHandle** 주소 SQL_HANDLE_ENV 옵션과이 변수를 전달 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  드라이버 관리자는 환경에 대 한 정보를 저장 하는 구조체를 할당 하 고 변수에 환경 핸들을 반환 합니다.  
  
 드라이버 관리자를 호출 하지 않습니다 **SQLAllocHandle** 이 드라이버에서 호출 하는 드라이버를 알지 못하므로 시간입니다. 호출 하는 작업이 지연 **SQLAllocHandle** 드라이버 응용 프로그램 데이터 원본에 연결 하는 함수를 호출할 때까지 합니다. 자세한 내용은 [연결 프로세스에서 드라이버 관리자의 역할](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)이 섹션의 뒷부분에 나오는.  
  
 사용 하 여 환경 핸들 해제 ODBC를 사용 하 여 응용 프로그램이 완료 되 면 **SQLFreeHandle**합니다. 응용 프로그램 프로그래밍 오류는 ODBC 함수 호출에서 환경 핸들을 사용 하는 것 환경에서 확보 한 후 이렇게 하면에 정의 되지 않은 있지만 아마도 심각한 결과가 발생 합니다.  
  
 때 **SQLFreeHandle** 호출 구조를 환경에 대 한 정보를 저장 하는 데 드라이버 릴리스 합니다. 사실은 **SQLFreeHandle** 후 해당 환경 핸들의 모든 연결 핸들 해제 될 때까지 환경 핸들을 호출할 수 없습니다.  
  
 환경 핸들에 대 한 자세한 내용은 참조 하세요. [환경을 처리](../../../odbc/reference/develop-app/environment-handles.md)합니다.
