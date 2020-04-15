---
title: 상태 전환 | 마이크로 소프트 문서
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
ms.openlocfilehash: 3a480b7ff8953ef94f0efc4886a09731730a61b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299696"
---
# <a name="state-transitions"></a>상태 전환
ODBC는 각 환경, 각 연결 및 각 문에 대한 불연속 *상태를* 정의합니다. 예를 들어 환경에는 할당되지 않은 상태(환경이 할당되지 않은 경우), 할당된 상태(환경이 할당되었지만 연결이 할당되지 않은 경우) 및 연결(환경 과 하나 이상의 연결이 할당됨)의 세 가지 상태가 있습니다. 연결에는 7개의 가능한 상태가 있습니다. 문에는 13개의 가능한 상태가 있습니다.  
  
 핸들로 식별된 특정 항목은 응용 프로그램이 특정 함수 또는 함수를 호출하고 핸들을 해당 항목에 전달할 때 한 상태에서 다른 상태로 이동합니다. 이러한 이동을 *상태 전환이라고*합니다. 예를 들어 **SQLAllocHandle을** 사용하여 환경 핸들을 할당하면 환경이 할당되지 않은 사용자에서 할당된 환경으로 이동하고 **SQLFreeHandle을** 사용하여 해당 핸들을 해제하면 할당된 사용자로부터 할당되지 않은 것으로 반환됩니다. ODBC는 제한된 수의 법적 상태 전환을 정의하며, 이는 함수를 특정 순서로 호출해야 한다는 또 다른 방법입니다.  
  
 **SQLGetConnectAttr과**같은 일부 함수는 상태에 전혀 영향을 주지 않습니다. 다른 함수는 단일 항목의 상태에 영향을 미칩니다. 예를 들어 **SQLDisconnect는** 연결 상태에서 할당된 상태로 연결을 이동합니다. 마지막으로 일부 함수는 두 개 이상의 항목의 상태에 영향을 미칩니다. 예를 들어 **SQLAllocHandle을** 사용하여 연결 핸들을 할당하면 할당되지 않은 상태에서 할당된 상태로 연결이 이동하고 환경이 할당된 상태에서 연결 상태로 이동합니다.  
  
 응용 프로그램에서 함수를 순서가 잘못 호출하면 함수는 *상태 전환 오류를*반환합니다. 예를 들어 환경이 연결 상태에 있고 응용 프로그램이 해당 환경 핸들을 사용하여 **SQLFreeHandle을** 호출하는 경우 **SQLFreeHandle은** 환경이 할당된 상태에 있을 때만 호출할 수 있으므로 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. ODBC는 이를 잘못된 상태 전환으로 정의하여 활성 연결이 있는 동안 응용 프로그램이 환경을 해제하지 못하도록 합니다.  
  
 일부 상태 전환은 ODBC 의 설계에 내재되어 있습니다. 예를 들어, 연결 핸들을 할당하는 함수에는 환경 핸들이 필요하기 때문에 환경 핸들을 먼저 할당하지 않고연결 핸들을 할당할 수 없습니다. 다른 상태 전환은 드라이버 관리자와 드라이버에 의해 적용됩니다. 예를 들어 **SQLExecute준비된** 문을 실행 합니다. 문 핸들이 준비된 상태가 아닌 경우 **SQLExecute는** SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다.  
  
 응용 프로그램의 관점에서 상태 전환은 일반적으로 간단합니다: 법적 상태 전환은 잘 작성된 응용 프로그램의 흐름과 함께 이동하는 경향이 있습니다. 상태 전환은 환경, 각 연결 및 각 문의 상태를 추적해야 하기 때문에 드라이버 관리자와 드라이버에 대해 더 복잡합니다. 이 작업의 대부분은 드라이버 관리자에 의해 수행됩니다. 드라이버가 수행해야 하는 대부분의 작업은 보류 중인 결과가 있는 명령문에서 발생합니다.  
  
 이 설명서의 1부와 2부("ODBC 소개" 및 "응용 프로그램 및 드라이버 개발")는 상태 전환을 명시적으로 언급하지 않는 경향이 있습니다. 대신 함수를 호출해야 하는 순서를 설명합니다. 예를 들어 "명령문 실행"은 **SQLExecute로**실행하기 전에 **SQLPrepare로** 문을 준비해야 합니다. 드라이버 관리자에서 검사하고 드라이버에서 확인해야 하는 전환을 포함하여 상태 및 상태 전환에 대한 전체 설명은 [부록 B: ODBC 상태 전환 테이블을](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조하십시오.
