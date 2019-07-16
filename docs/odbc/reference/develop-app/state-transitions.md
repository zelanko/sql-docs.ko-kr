---
title: 상태 전환 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2512d277980b071523cfea6cbe132f2a3861b7d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107295"
---
# <a name="state-transitions"></a>상태 전환
ODBC 정의 불연속 *상태* 각 환경, 각 연결 및 각 문에 대 한 합니다. 예를 들어, 환경에는 세 가지 가능한 상태에 있습니다. (환경이 할당 되는)에서 할당 되지 않은, 할당 된 (있는 환경에는 할당 되지만 연결 없이 할당 된) 및 연결 (있는 환경 및 하나 이상의 연결 된 할당 됨). 연결 있는 일곱 개의 가능한 상태입니다. 문에 13 가능한 상태 권한이 있습니다.  
  
 특정 항목을 해당 핸들로 식별 한 대로 이동 한 상태에서 다른 응용 프로그램 특정 함수 또는 함수를 호출 하 고 해당 항목에 핸들을 전달 하는 경우. 이러한 이동은 호출을 *상태 전환*합니다. 예를 들어, 사용 하 여 환경 핸들을 할당 **SQLAllocHandle** 할당 되지 않은 할당 된, 및 사용 하 여 해당 핸들을 해제 환경 이동 **SQLFreeHandle** 에 할당 된에서 반환 할당 되지 않은 합니다. ODBC는 말하면 특정 순서에 따라 함수를 호출 해야 하는 제한 된 수의 올바른 상태 전환 정의 합니다.  
  
 와 같은 일부 함수 **SQLGetConnectAttr**를 전혀 상태를 주지 않습니다. 다른 함수는 단일 항목의 상태를 영향을 줍니다. 예를 들어 **SQLDisconnect** 할당 된 상태로 연결 상태에서 연결을 이동 합니다. 마지막으로 일부 함수 둘 이상의 항목의 상태를 영향을 줍니다. 예를 들어, 사용 하 여 연결 핸들을 할당 **SQLAllocHandle** 할당 된 상태로 할당 되지 않은에서 연결을 이동 하 고는 할당 된 환경 연결 상태를 이동 합니다.  
  
 함수를 반환 하는 경우 응용 프로그램이 잘못 된 함수를 호출을 *전환 오류 상태*합니다. 예를 들어 환경은 연결 상태와 응용 프로그램 호출 **SQLFreeHandle** 해당 환경 핸들을 사용 하 여 **SQLFreeHandle** SQLSTATE HY010 반환 (함수 시퀀스 오류입니다.) 있으므로 환경은 할당 된 상태인 경우에 호출할 수 있습니다. 이는 잘못 된 상태 전환이으로 정의 하 여 ODBC 응용 프로그램에서 대 한 활성 연결이 하는 동안 환경 해제를 방지 합니다.  
  
 일부 상태 전이 ODBC의 디자인에 본질적으로 존재 합니다. 예를 들어 연결 핸들을 할당 하는 함수에는 환경 핸들이 필요 하기 때문에 첫 번째 환경 핸들을 할당 하지 않고 연결 핸들을 할당할 수 없는 합니다. 다른 상태 전환은 드라이버 관리자와 드라이버에서 적용 됩니다. 예를 들어 **SQLExecute** 준비 된 문을 실행 합니다. 문 핸들을 전달 하는 경우에 있지는 준비 상태 **SQLExecute** SQLSTATE HY010 반환 (함수 시퀀스 오류).  
  
 응용 프로그램의 관점에서 상태 전환을 일반적으로 단순 합니다. 유효한 상태 전환을 대개 손에서 직접 잘 작성 된 응용 프로그램의 흐름을 사용 합니다. 상태 전환 드라이버 관리자 및 드라이버에 대 한 더 복잡 한 되므로 환경, 각 연결 및 각 문에의 상태를 추적 해야 합니다. 이 작업의 대부분 드라이버 관리자에 의해; 이루어집니다 합니다. 드라이버에서 수행 해야 하는 작업의 대부분을 사용 하 여 보류 중인 결과가 문을 사용 하 여 발생 합니다.  
  
 이 설명서의 파트 1 및 2 ("ODBC 소개" 및 "응용 프로그램 및 드라이버 개발") 상태 전환을 명시적으로 언급 하지 않는 경향이 있습니다. 대신 이러한 함수를 호출 해야 하는 순서를 설명 합니다. 예를 들어, "문 실행" 상태는 문을 사용 하 여 준비 해야 합니다 **SQLPrepare** 사용 하 여 실행할 수 있습니다 **SQLExecute**합니다. 상태 및 상태 전환에는 전환에는 드라이버 관리자에 의해 검사 되 고 드라이버를 확인 해야 하는 포함 한 전체 설명을 참조 하세요. [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.
