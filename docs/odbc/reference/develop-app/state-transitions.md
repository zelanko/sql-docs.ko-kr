---
description: 상태 전환
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 947be49fc0a77f94c1641bb7c735db3276b49f58
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476365"
---
# <a name="state-transitions"></a>상태 전환
ODBC는 각 환경, 각 연결 및 각 문에 대 한 불연속 *상태* 를 정의 합니다. 예를 들어 환경에는 할당 되지 않음 (환경이 할당 되지 않음), 할당 됨 (환경이 할당 되었지만 연결이 할당 되지 않음) 및 연결 (환경 및 하나 이상의 연결이 할당 됨)의 세 가지 상태가 있습니다. 연결에는 7 개의 가능한 상태가 있습니다. 문의 가능한 상태는 13입니다.  
  
 응용 프로그램이 특정 함수를 호출 하 고 해당 항목에 핸들을 전달 하는 경우 핸들에 의해 식별 되는 특정 항목은 한 상태에서 다른 상태로 이동 합니다. 이러한 이동을 *상태 전환*이라고 합니다. 예를 들어 **SQLAllocHandle** 를 사용 하 여 환경 핸들을 할당 하면 환경이 할당 되지 않음에서 할당 됨으로 이동 하 고, **sqlfreehandle** 을 사용 하 여 해당 핸들을 해제 하면 할당 되지 않은에서 할당 되지 않습니다 ODBC는 제한 된 수의 법적 상태 전환을 정의 합니다 .이는 함수를 특정 순서로 호출 해야 한다는 또 다른 방법입니다.  
  
 **SQLGetConnectAttr**와 같은 일부 함수는 상태에 영향을 주지 않습니다. 다른 함수는 단일 항목의 상태에 영향을 줍니다. 예를 들어 **Sqldisconnect** 는 연결 상태에서 할당 된 상태로 연결을 이동 합니다. 마지막으로, 일부 함수는 두 개 이상의 항목 상태에 영향을 줍니다. 예를 들어 **SQLAllocHandle** 를 사용 하 여 연결 핸들을 할당 하면 할당 되지 않은에서 할당 된 상태로 연결이 이동 되 고 할당 된에서 연결 상태로 환경이 이동 합니다.  
  
 응용 프로그램이 순서를 벗어난 함수를 호출 하는 경우이 함수는 *상태 전환 오류*를 반환 합니다. 예를 들어 환경이 연결 상태이 고 응용 프로그램이 해당 환경 핸들을 사용 하 여 **Sqlfreehandle** 을 호출 하는 경우 **Sqlfreehandle** 은 환경이 할당 된 상태에 있을 때만 호출 될 수 있으므로 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. ODBC는이를 잘못 된 상태 전환으로 정의 하 여 활성 연결이 있는 동안 응용 프로그램에서 환경을 해제 하지 못하도록 합니다.  
  
 일부 상태 전환은 ODBC 디자인에서 본질적으로 발생 합니다. 예를 들어 연결 핸들을 할당 하는 함수에는 환경 핸들이 필요 하기 때문에 먼저 환경 핸들을 할당 하지 않고 연결 핸들을 할당할 수 없습니다. 다른 상태 전환은 드라이버 관리자 및 드라이버에 의해 적용 됩니다. 예를 들어 **Sqlexecute** 는 준비 된 문을 실행 합니다. 전달 된 문 핸들이 준비 상태가 아닌 경우 **Sqlexecute** 는 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다.  
  
 응용 프로그램의 관점에서 볼 때 상태 전환은 일반적으로 잘 작성 된 응용 프로그램의 흐름과 매우 간단 합니다. 상태 전환은 환경, 각 연결 및 각 문에 대 한 상태를 추적 해야 하기 때문에 드라이버 관리자와 드라이버에 더 복잡 합니다. 이러한 작업의 대부분은 드라이버 관리자에 의해 수행 됩니다. 드라이버에서 수행 해야 하는 대부분의 작업은 보류 중인 결과가 포함 된 문에서 발생 합니다.  
  
 이 설명서의 1 부와 2 부 ("ODBC 소개" 및 "응용 프로그램 및 드라이버 개발")는 상태 전환을 명시적으로 언급 하지 않는 경향이 있습니다. 대신 함수를 호출 해야 하는 순서를 설명 합니다. 예를 들어 "문 실행"은 Sqlprepare **를 사용 하**여 문을 실행 하기 전에 **sqlprepare** 를 사용 하 여 문을 준비 해야 함을 설명 합니다. 드라이버 관리자에 의해 확인 되 고 드라이버에서 확인 해야 하는 전환을 비롯 하 여 상태 및 상태 전환에 대 한 자세한 설명은 [부록 B: ODBC 상태 전환 표](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)를 참조 하세요.
