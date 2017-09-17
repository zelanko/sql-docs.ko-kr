---
title: "ODBC 문 핸들 해제 | Microsoft Docs"
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
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b33d262c846d9ef8a41bf9440802664ac7d4b75f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="freeing-a-statement-handle-odbc"></a>ODBC 문 핸들 해제
앞서 언급 했 듯이 스키마를 삭제 하는 보다 새로 할당 문을 다시 사용 하려면 더 효율적입니다. 문에서 새 SQL 문을 실행 하기 전에 응용 프로그램에서 현재 문 설정이 적절 한지 있을 수 있습니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 일반적으로 매개 변수 및 결과 집합에 대 한 이전 SQL 문의 해야 바인딩 해제 될 (호출 하 여 **SQLFreeStmt** SQL_RESET_PARAMS 및 SQL_UNBIND 옵션과 함께) 하 고 새 SQL 문에 대 한 다시 합니다.  
  
 호출 응용 프로그램에서 문을 사용 하 여 완료 되 면 **SQLFreeHandle** 를 해당 문을 해제 합니다. 문을 확보 한 후는 ODBC 함수;에 대 한 호출에서 해당 문 핸들을 사용 하려는 프로그래밍 오류 응용 프로그램 이렇게 하면 되므로 결과가 정의 되지 않은 있지만 아마도 심각한 됩니다.  
  
 때 **SQLFreeHandle** 호출 되는 드라이버 릴리스 구조 문에 대 한 정보를 저장 하는 데 사용 합니다.  
  
 **SQLDisconnect** 자동으로 연결 된 모든 문을 해제 합니다.
