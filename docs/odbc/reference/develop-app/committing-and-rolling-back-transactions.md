---
title: 트랜잭션 커밋 및 롤백 | Microsoft Docs
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
ms.openlocfilehash: c7c028ca7e89378e959b11f59cad4119cef5086a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083314"
---
# <a name="committing-and-rolling-back-transactions"></a>트랜잭션 커밋 및 롤백
수동 커밋 모드에서 트랜잭션을 커밋하거나 롤백하려면 응용 프로그램이 **Sqlendtran**을 호출 합니다. 트랜잭션을 지 원하는 Dbms 용 드라이버는 일반적으로 **COMMIT** 또는 **ROLLBACK** 문을 실행 하 여이 함수를 구현 합니다. 연결이 자동 커밋 모드일 때 드라이버 관리자는 **Sqlendtran** 을 호출 하지 않습니다. 응용 프로그램이 트랜잭션을 롤백하려고 시도 하는 경우에도 SQL_SUCCESS 반환 됩니다. 트랜잭션을 지원 하지 않는 Dbms 용 드라이버는 항상 자동 커밋 모드 이므로 아무것도 수행 하지 않거나 전혀 구현 하지 않고 SQL_SUCCESS 반환 하도록 **Sqlendtran** 을 구현할 수 있습니다.  
  
> [!NOTE]  
>  응용 프로그램은 **Sqlexecute** 또는 **sqlexecdirect**를 사용 하 여 **commit** 또는 **ROLLBACK** 문을 실행 하 여 트랜잭션을 커밋하거나 롤백해야 합니다. 이 작업의 결과는 정의 되지 않습니다. 트랜잭션이 활성 상태이 고 이러한 문이 트랜잭션을 지원 하지 않는 데이터 원본에 대해 실패 하는 경우 드라이버가 더 이상 알지 못하는 문제가 발생할 수 있습니다. 이러한 응용 프로그램은 대신 **Sqlendtran** 을 호출 해야 합니다.  
  
 응용 프로그램이 환경 핸들을 **Sqlendtran** 에 전달 하지만 연결 핸들을 전달 하지 않는 경우 드라이버 관리자는 환경에서 하나 이상의 활성 연결이 있는 각 드라이버에 대해 환경 핸들을 사용 하 여 **sqlendtran** 을 개념적으로 호출 합니다. 그러면 드라이버는 환경의 각 연결에서 트랜잭션을 커밋합니다. 그러나 드라이버와 드라이버 관리자는 환경의 연결에 대해 2 단계 커밋을 수행 하지 않습니다. 이는 환경의 모든 연결에 대해 **Sqlendtran** 을 동시에 호출 하는 프로그래밍 상의 편리한 방법일 뿐입니다.  
  
 ( *2 단계 커밋은* 일반적으로 여러 데이터 원본에 걸쳐 분산 된 트랜잭션을 커밋하는 데 사용 됩니다. 첫 번째 단계에서는 데이터 원본이 트랜잭션 부분을 커밋할 수 있는지 여부에 맞게 폴링됩니다. 두 번째 단계에서는 트랜잭션이 실제로 모든 데이터 원본에 커밋됩니다. 첫 번째 단계에서 트랜잭션을 커밋할 수 없는 데이터 원본이 회신 하는 경우 두 번째 단계가 발생 하지 않습니다.
