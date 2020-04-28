---
title: 문 핸들을 할당 하는 중 ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288433"
---
# <a name="allocating-a-statement-handle-odbc"></a>명령문 핸들 ODBC 할당
응용 프로그램은 문을 실행 하기 전에 다음과 같이 문 핸들을 할당 해야 합니다.  
  
1.  응용 프로그램은 HSTMT 형식의 변수를 선언 합니다. 그런 다음 **SQLAllocHandle** 를 호출 하 고이 변수의 주소, 문을 할당할 연결의 핸들 및 SQL_HANDLE_STMT 옵션을 전달 합니다. 예를 들면 다음과 같습니다.  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  드라이버 관리자는 문에 대 한 정보를 저장 하 고 SQL_HANDLE_STMT 옵션을 사용 하 여 드라이버에서 **SQLAllocHandle** 를 호출 하는 구조를 할당 합니다.  
  
3.  드라이버는 문에 대 한 정보를 저장 하 고 드라이버 문 핸들을 드라이버 관리자에 반환 하는 자체 구조를 할당 합니다.  
  
4.  드라이버 관리자는 응용 프로그램 변수의 드라이버 관리자 문 핸들을 응용 프로그램에 반환 합니다.  
  
 문 핸들은 ODBC 함수를 호출할 때 사용할 문을 식별 합니다. 문 핸들에 대 한 자세한 내용은 [문 핸들](../../../odbc/reference/develop-app/statement-handles.md)을 참조 하십시오.
