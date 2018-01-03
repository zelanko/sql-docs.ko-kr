---
title: "상태 전환 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6795a0e730f1b927b7921863714a2a9db55551e4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="state-transitions"></a>상태 전환
ODBC에 정의 되어 불연속 *상태* 각 환경, 각 연결 및 각 문에 대 한 합니다. 예를 들어 환경에 가능한 상태는 세: (할당 되는 환경이)에 할당 되지 않은, 할당 된 (있는 환경 할당 되었지만 연결이 없는 할당) 및 (중인 환경 및 하나 이상의 연결을 연결 할당 됨). 연결 있는 7 가지 가능한 상태입니다. 문은 사항이 13 가능한 상태입니다.  
  
 특정 항목을 해당 핸들로 식별 한 대로 이동 한 상태에서 다른 응용 프로그램 특정 함수 또는 함수를 호출 하 고 해당 항목에 핸들을 전달 하는 경우. 이러한 이동 라고는 *상태 전환*합니다. 예를 들어 있는 환경 핸들을 할당 **SQLAllocHandle** 할당 되지 않은 할당 된, 하 고 해당 핸들을 해제 환경을 이동 **SQLFreeHandle** 에 할당 된에서 반환 할당 되지 않은 경우. ODBC는 말하면 특정 순서에 따라 함수를 호출 해야 하는 제한 된 수의 올바른 상태 전환 정의 합니다.  
  
 와 같은 일부 함수가 **SQLGetConnectAttr**, 상태 적용 되지 않습니다. 다른 함수는 단일 항목의 상태에 영향을 합니다. 예를 들어 **SQLDisconnect** 할당 된 상태로 연결 상태에서 연결을 이동 합니다. 마지막으로 일부 함수에 둘 이상의 항목의 상태에 영향을 합니다. 와 연결 핸들을 할당 하는 예를 들어 **SQLAllocHandle** 연결은 할당 되지 않은 할당 된 상태로 이동한 연결 상태에는 할당 된에서 환경을 이동 합니다.  
  
 함수 반환 하는 경우 응용 프로그램이 정렬 되지 않은 함수 호출는 *상태 전환 오류*합니다. 예를 들어, 환경 연결 상태와 응용 프로그램에 있으면 호출 **SQLFreeHandle** 이 환경 핸들을 가진 **SQLFreeHandle** SQLSTATE HY010 반환 (함수 시퀀스 오류입니다.) 하므로 환경이 할당 된 상태에 있을 때에 호출할 수 있습니다. 이 잘못 된 상태 전환을으로 정의 하 여 ODBC에서 활성 연결이 있을 때는 환경을 해제 응용 프로그램을 방지 합니다.  
  
 일부 상태 전환을 ODBC의 디자인에 본질적으로 존재 합니다. 예를 들어 연결 핸들을 할당 하는 함수에는 환경 핸들이 필요 하기 때문에 첫 번째 환경 핸들을 할당 하지 않고 연결 핸들을 할당 수 없으면입니다. 다른 상태 전환은 드라이버 관리자와 드라이버에서 적용 됩니다. 예를 들어 **SQLExecute** 준비 된 문을 실행 합니다. 문 핸들에 전달 하는 경우에 없는 준비 된 상태 **SQLExecute** SQLSTATE HY010 반환 (함수 시퀀스 오류).  
  
 응용 프로그램의 관점에서 상태 전환을 일반적으로 간단: 손에서 직접 이동 하는 경향이 법적 상태 전환 잘 작성 된 응용 프로그램의 흐름. 상태 전환 드라이버 관리자와 드라이버에 대 한 보다 복잡 한 되므로의 환경, 각 연결과 각 문의 상태를 추적 해야 합니다. 이 작업의 대부분 드라이버 관리자; 이루어진다는 합니다. 드라이버에서 수행 해야 하는 작업의 대부분 보류 중인 결과와 문과 함께 발생 합니다.  
  
 이 설명서의 파트 1 및 2 ("ODBC 소개" 및 "응용 프로그램 및 드라이버 개발") 명시적으로 언급 되어 상태 전환을 하지 않습니다. 대신,이 개체 함수를 호출 해야 하는 순서를 설명 합니다. 예를 들어, "문 실행" 문을 사용 하 여 준비 해야 하에 따르면 **SQLPrepare** 으로 실행 될 수 **SQLExecute**합니다. 상태 및 상태 전이 어떤 변환에는 드라이버 관리자에서 확인 되 고 드라이버에서 확인 해야 합니다를 비롯 한 자세한 내용은 참조 하십시오. [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.
