---
title: ODBC 를 처리하는 명령문 할당 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9a15bc4622b15afa9838327edd90383a812270
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288433"
---
# <a name="allocating-a-statement-handle-odbc"></a>명령문 핸들 ODBC 할당
응용 프로그램이 문을 실행하기 전에 다음과 같이 문 핸들을 할당해야 합니다.  
  
1.  응용 프로그램은 HSTMT 형식의 변수를 선언합니다. 그런 다음 **SQLAllocHandle을** 호출하고 이 변수의 주소, 문을 할당할 연결의 핸들 및 SQL_HANDLE_STMT 옵션을 전달합니다. 다음은 그 예입니다.  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  드라이버 관리자는 명령문에 대한 정보를 저장하는 구조를 할당하고 SQL_HANDLE_STMT 옵션을 사용하여 드라이버에 **SQLAllocHandle을** 호출합니다.  
  
3.  드라이버는 문에 대한 정보를 저장하는 자체 구조를 할당하고 드라이버 문 핸들을 드라이버 관리자에게 반환합니다.  
  
4.  드라이버 관리자는 드라이버 관리자 문 핸들을 응용 프로그램 변수의 응용 프로그램에 반환합니다.  
  
 명령문 핸들은 ODBC 함수를 호출할 때 사용할 문을 식별합니다. 명령문 핸들에 대한 자세한 내용은 [명령문 핸들 을](../../../odbc/reference/develop-app/statement-handles.md)참조하십시오.
