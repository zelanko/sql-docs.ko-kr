---
title: ODBC 문 핸들 해제 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 638cf9fb3c7af73130cf1413559b9baee2a354c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069786"
---
# <a name="freeing-a-statement-handle-odbc"></a>명령문 핸들 ODBC 해제
앞에서 설명한 대로이를 삭제 하 고 새로 할당 보다 문을 다시 사용 하는 것이 효율적입니다. 문에서 새 SQL 문을 실행 하기 전에 응용 프로그램 현재 문 설정이 적절 하 게 있을 수 있습니다. 이러한 설정에는 문 특성, 매개 변수 바인딩 및 결과 집합 바인딩이 포함됩니다. 바인딩 해제 될 매개 변수 및 이전 SQL 문의 결과 집합을 해야 일반적으로 (호출한 **SQLFreeStmt** SQL_RESET_PARAMS 및 SQL_UNBIND 옵션과 함께) 및 새 SQL 문에 대 한 다시 합니다.  
  
 호출 응용 프로그램은 문을 사용 하 여 완료 되 면 **SQLFreeHandle** 에 해당 문을 해제 합니다. 응용 프로그램 프로그래밍 오류는 ODBC 함수 호출에서 문의 핸들을 사용 하는 것 문을 확보 한 후 이렇게 하면에 정의 되지 않은 있지만 아마도 심각한 결과가 발생 합니다.  
  
 때 **SQLFreeHandle** 호출 되는 문에 대 한 정보를 저장 하는 것을 데 구조 드라이버 릴리스 합니다.  
  
 **SQLDisconnect** 자동으로 연결 된 모든 문을 해제 합니다.
