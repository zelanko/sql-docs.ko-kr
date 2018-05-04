---
title: ODBC 문 핸들 할당 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d0f2bd2da071bb690443df9d5c0bdebb5a5e1e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="allocating-a-statement-handle-odbc"></a>ODBC 문 핸들 할당
응용 프로그램에서 문을 실행 하려면, 먼저 다음과 같이 문 핸들을 할당 해야 합니다.  
  
1.  응용 프로그램 HSTMT 형식의 변수를 선언합니다. 그런 다음 연속 호출 **SQLAllocHandle** 하 고이 변수는 문과 여 옵션을 할당할 수 있는 연결의 핸들의 주소를 전달 합니다. 예를 들어:  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  드라이버 관리자는 문 및 호출 하는 방법에 대 한 정보를 저장 하는 구조를 할당 **SQLAllocHandle** 여 옵션을 사용 하 여 드라이버에서 합니다.  
  
3.  문에 대 한 정보를 저장 하는 구조를 할당 하 고 드라이버 관리자를 드라이버 문 핸들을 반환 하는 드라이버.  
  
4.  드라이버 관리자는 응용 프로그램 변수에서 응용 프로그램에 드라이버 관리자 문 핸들을 반환합니다.  
  
 문 핸들에는 ODBC 함수를 호출할 때 사용 하는 문을 식별 합니다. 문 핸들에 대 한 자세한 내용은 참조 [문 핸들](../../../odbc/reference/develop-app/statement-handles.md)합니다.
