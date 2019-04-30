---
title: ODBC 문 핸들 할당 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9524f2e6b01d2a5827dcface3159b7c52a728c59
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287867"
---
# <a name="allocating-a-statement-handle-odbc"></a>명령문 핸들 ODBC 할당
응용 프로그램에서 문을 실행 하려면, 먼저 다음과 같이 문 핸들을 할당 해야 합니다.  
  
1.  응용 프로그램 HSTMT 형식의 변수를 선언합니다. 그런 다음 호출 **SQLAllocHandle** 하 고이 변수는 문 및 호출 하 여 옵션을 할당 하는 연결의 핸들의 주소를 전달 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  드라이버 관리자는 문 및 호출 하는 방법에 대 한 정보를 저장 하는 구조체를 할당 **SQLAllocHandle** 호출 하 여 옵션을 사용 하 여 합니다.  
  
3.  드라이버는 문에 대 한 정보를 저장 하는 고유한 구조를 할당 하 고 드라이버 관리자를 드라이버 문 핸들을 반환 합니다.  
  
4.  드라이버 관리자는 응용 프로그램 변수에서 응용 프로그램에 드라이버 관리자 문 핸들을 반환합니다.  
  
 문 핸들에는 ODBC 함수를 호출할 때 사용 하는 문을 식별 합니다. 문 핸들에 대 한 자세한 내용은 참조 하세요. [문 핸들](../../../odbc/reference/develop-app/statement-handles.md)합니다.
