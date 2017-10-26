---
title: "커밋 및 트랜잭션을 롤백하면 | Microsoft Docs"
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
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4090e609063b74fdcbef694c400272ee6af090c5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="committing-and-rolling-back-transactions"></a>커밋 및 트랜잭션 롤백
응용 프로그램이 호출 커밋하거나 수동 커밋 모드에서 트랜잭션을 롤백하려면 **SQLEndTran**합니다. 실행 하 여이 함수를 구현 하는 트랜잭션을 지 원하는 일반적으로 Dbms에 대 한 드라이버는 **커밋** 또는 **롤백** 문을 합니다. 드라이버 관리자가 호출 하지 않으면 **SQLEndTran** 자동 커밋 모드에 연결 된 경우 단순히 반환 SQL_SUCCESS, 응용 프로그램에서 트랜잭션을 하려고 하는 경우에 합니다. 구현 하거나 수 트랜잭션을 지원 하지 않는 Dbms에 대 한 드라이버가 자동 커밋 모드에서 항상 되므로 **SQLEndTran** 아무 작업도 수행 하지 않고 관계 없이 SQL_SUCCESS를 반환 하거나 전혀 구현 하지 않습니다.  
  
> [!NOTE]  
>  응용 프로그램 하지 커밋할지 아니면를 실행 하 여 트랜잭션을 롤백할 **커밋** 또는 **롤백** 으로 문을 **SQLExecute** 또는 **SQLExecDirect**. 이 작업의 효과 정의 되지 않습니다. 가능한 문제는 더 이상 트랜잭션이 활성화 되어 알고 있으면 드라이버 및 트랜잭션을 지원 하지 않는 데이터 원본에 대해 실패 하는 이러한 문을 포함 됩니다. 이러한 응용 프로그램 호출 해야 **SQLEndTran** 대신 합니다.  
  
 응용 프로그램에 대 한 환경 핸들을 전달 하는 경우 **SQLEndTran** 하지만 불합격 드라이버 관리자 연결 핸들을 개념적으로 호출지 않습니다 **SQLEndTran** 각 드라이버에 대 한 환경 핸들을 포함 하는 환경에서에 하나 이상의 활성 연결이 합니다. 드라이버에는 다음 환경에서 각 연결에서 트랜잭션을 커밋합니다. 그러나 되기 드라이버 아니고 드라이버 관리자는 환경에 연결에 대해 2 단계 커밋 수행 방법 이 단지 프로그래밍의 편의를 위해 동시에 호출할 **SQLEndTran** 환경에서 모든 연결에 대 한 합니다.  
  
 (A *2 단계 커밋* 분산 되는 여러 데이터 원본 트랜잭션을 커밋하기 위해 일반적으로 사용 됩니다. 첫 번째 단계에서 데이터 원본 트랜잭션의 해당 부분을 커밋할 수 있는지 여부에 대 한 폴링을 수행 합니다. 두 번째 단계에서는 모든 데이터 원본에는 트랜잭션이 커밋 실제로 합니다. 모든 데이터 원본 첫 번째 단계에서는 트랜잭션을 커밋할 수 없습니다 것을 회신 하는 경우 두 번째 단계가 발생 하지 않습니다.)

