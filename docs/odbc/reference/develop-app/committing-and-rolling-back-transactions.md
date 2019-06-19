---
title: 트랜잭션 롤백 및 커밋 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 194a90482946814995ca1963f7c8fc4bce48d223
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126366"
---
# <a name="committing-and-rolling-back-transactions"></a>트랜잭션 커밋 및 롤백
응용 프로그램이 호출에서는 커밋하거나 수동 커밋 모드에서 트랜잭션을 롤백하려면 **SQLEndTran**합니다. 실행 하 여이 함수를 구현 하는 트랜잭션을 지 원하는 일반적으로 Dbms 용 드라이버를 **커밋** 또는 **롤백** 문. 드라이버 관리자를 호출 하지 않습니다 **SQLEndTran** 연결이 자동 커밋 모드의 경우 단순히 반환 SQL_SUCCESS, 응용 프로그램에서 트랜잭션을 롤백합니다 하려고 하는 경우에 합니다. 구현 하거나 트랜잭션을 지원 하지 않는 Dbms에 대 한 드라이버가 자동 커밋 모드에서 항상 이기 때문에 가능 **SQLEndTran** 아무 작업도 수행 하지 않고 관계 없이 SQL_SUCCESS를 반환 하거나 전혀 구현 하지 않습니다.  
  
> [!NOTE]  
>  응용 프로그램 하지 커밋할지 또는 실행 하 여 트랜잭션을 롤백합니다 **커밋** 하거나 **롤백** 문을 **SQLExecute** 또는 **SQLExecDirect**. 이 작업의 효과 정의 되지 않습니다. 가능한 문제에는 더 이상 트랜잭션이 활성 중일 때 알고 있으면 드라이버 및 트랜잭션을 지원 하지 않는 데이터 원본에 대해 실패 한 이러한 문이 포함 됩니다. 이러한 응용 프로그램을 호출 해야 **SQLEndTran** 대신 합니다.  
  
 응용 프로그램에 대 한 환경 핸들을 전달 하는 경우 **SQLEndTran** 하지만 드라이버 관리자 연결 핸들을 전달 하지 개념적 호출 **SQLEndTran** 각 드라이버에 대 한 환경 핸들을 포함 하는 하나 이상의 활성 연결 환경에 있습니다. 드라이버에는 다음 환경에서 각 연결에서 트랜잭션을 커밋합니다. 드라이버 아니고 드라이버 관리자는 환경에 연결 2 단계 커밋 수행 한다는 점에 주의 해야 하는 반면 이 단순히 프로그래밍의 편의를 위해 동시에 호출할 **SQLEndTran** 환경에서 모든 연결에 대 한 합니다.  
  
 (A *2 단계 커밋* 여러 데이터 소스에 분산 된 트랜잭션을 커밋하기 위해 일반적으로 사용 됩니다. 해당 첫 번째 단계에서는 데이터 소스는 트랜잭션의 해당 부분을 커밋할 수 있는지 여부에 대 한 간격으로 폴링됩니다. 두 번째 단계에서는 실제로 커밋될 때 모든 데이터 원본입니다. 모든 데이터 원본 첫 번째 단계에서는 트랜잭션을 커밋할 수 없습니다. 이러한을 회신 하는 경우 두 번째 단계는 발생 하지 않습니다.)
