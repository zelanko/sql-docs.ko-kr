---
title: 트랜잭션 커밋 및 롤백 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c272d60242d31622452c4dcb0f6a16c4838768f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299113"
---
# <a name="committing-and-rolling-back-transactions"></a>트랜잭션 커밋 및 롤백
수동 커밋 모드에서 트랜잭션을 커밋하거나 롤백하려면 응용 프로그램이 **SQLEndTran을**호출합니다. 트랜잭션을 지원하는 DBMS용 드라이버는 일반적으로 **COMMIT** 또는 **ROLLBACK** 문을 실행하여 이 기능을 구현합니다. 연결이 자동 커밋 모드에 있을 때 드라이버 관리자는 **SQLEndTran을** 호출하지 않습니다. 응용 프로그램이 트랜잭션을 롤백하려고 해도 SQL_SUCCESS 단순히 반환합니다. 트랜잭션을 지원하지 않는 DBMS용 드라이버는 항상 자동 커밋 모드이므로 **SQLEndTran을** 구현하여 아무 것도 하지 않고 SQL_SUCCESS 반환하거나 전혀 구현하지 않을 수 있습니다.  
  
> [!NOTE]  
>  응용 프로그램은 **SQLExecute** 또는 **SQLExecDirect** **COMMIT** . **ROLLBACK** 이 작업을 수행하는 효과는 정의되지 않습니다. 가능한 문제로는 트랜잭션이 활성화된 시기를 더 이상 알지 못하는 드라이버와 트랜잭션을 지원하지 않는 데이터 원본에 대해 이러한 명령문이 실패하는 문제가 있습니다. 이러한 응용 프로그램은 대신 **SQLEndTran을** 호출해야 합니다.  
  
 응용 프로그램이 환경 핸들을 **SQLEndTran에** 전달하지만 연결 핸들을 통과하지 못하는 경우 드라이버 관리자는 환경에서 하나 이상의 활성 연결이 있는 각 드라이버에 대해 환경 핸들을 사용하여 **SQLEndTran을** 개념적으로 호출합니다. 그런 다음 드라이버는 환경의 각 연결에 트랜잭션을 커밋합니다. 그러나 드라이버나 드라이버 관리자는 환경의 연결에 대해 2단계 커밋을 수행하지 않는다는 것을 깨닫는 것이 중요합니다. 이는 환경의 모든 연결에 대해 **SQLEndTran을** 동시에 호출하는 프로그래밍 편의에 불과합니다.  
  
 *2단계 커밋은* 일반적으로 여러 데이터 원본에 분산된 트랜잭션을 커밋하는 데 사용됩니다. 첫 번째 단계에서 데이터 원본은 트랜잭션의 일부를 커밋할 수 있는지 여부에 대해 폴링됩니다. 두 번째 단계에서트랜잭션은 실제로 모든 데이터 원본에서 커밋됩니다. 첫 번째 단계에서 트랜잭션을 커밋할 수 없는 데이터 원본이 회신하면 두 번째 단계가 발생하지 않습니다.
