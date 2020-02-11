---
title: 환경 핸들을 할당 하는 중 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077179"
---
# <a name="allocating-the-environment-handle"></a>환경 핸들 할당
ODBC 응용 프로그램에 대 한 첫 번째 작업은 드라이버 관리자를 로드 하는 것입니다. 이 작업을 수행 하는 방법은 운영 체제에 따라 다릅니다. 예를 들어 Microsoft® Windows NT® Server/Windows 2000 Server, Windows NT Workstation/Windows 2000 Professional 또는 Microsoft Windows® 95/98를 실행 하는 컴퓨터에서 응용 프로그램은 드라이버 관리자 라이브러리에 연결 하거나 **LoadLibrary** 를 호출 하 여 드라이버 관리자 DLL을 로드 합니다.  
  
 응용 프로그램이 다른 ODBC 함수를 호출 하기 전에 수행 해야 하는 다음 작업은 ODBC 환경을 초기화 하 고 다음과 같이 환경 핸들을 할당 하는 것입니다.  
  
1.  응용 프로그램은 SQLHENV 형식의 변수를 선언 합니다. 그런 다음 **SQLAllocHandle** 를 호출 하 고이 변수 및 SQL_HANDLE_ENV 옵션의 주소를 전달 합니다. 다음은 그 예입니다.  
  
    ```  
    SQLHENV henv1;  
  
    SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv1);  
    ```  
  
2.  드라이버 관리자는 환경에 대 한 정보를 저장 하는 구조를 할당 하 고 변수에서 환경 핸들을 반환 합니다.  
  
 드라이버 관리자는 호출할 드라이버를 알 수 없기 때문에 지금은 드라이버에서 **SQLAllocHandle** 를 호출 하지 않습니다. 응용 프로그램이 데이터 소스에 연결 하는 함수를 호출할 때까지 드라이버에서 **SQLAllocHandle** 를 호출 하는 것이 지연 됩니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [연결 프로세스에서 드라이버 관리자의 역할](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)을 참조 하세요.  
  
 응용 프로그램이 ODBC 사용을 마치면 **Sqlfreehandle**을 사용 하 여 환경 핸들을 해제 합니다. 환경을 해제 한 후에는 ODBC 함수 호출에서 환경의 핸들을 사용 하는 응용 프로그램 프로그래밍 오류가 발생 합니다. 이렇게 하면 정의 되지 않았지만 심각한 결과가 발생할 수 있습니다.  
  
 **Sqlfreehandle** 을 호출 하면 드라이버는 환경에 대 한 정보를 저장 하는 데 사용 되는 구조를 해제 합니다. 환경 핸들에 대 한 모든 연결 핸들을 해제 한 후에 야 환경 핸들에 대해 **Sqlfreehandle** 을 호출할 수 있습니다.  
  
 환경 핸들에 대 한 자세한 내용은 [환경 핸들](../../../odbc/reference/develop-app/environment-handles.md)을 참조 하세요.
