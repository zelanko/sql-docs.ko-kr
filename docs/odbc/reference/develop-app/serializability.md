---
title: 순차성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7972fb72607edca8c1599c2d028b073c184642
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63251484"
---
# <a name="serializability"></a>직렬화 가능성
트랜잭션 것 이상적 *serializable*합니다. 트랜잭션 같으면 트랜잭션이 동시에 실행 결과-순차적으로 실행의 결과로 직렬화 할 수 있다고 합니다. 즉, 다른 하나입니다. 중요 하지 않습니다 하는 트랜잭션 결과 트랜잭션의 모든 혼합을 반영 하지 않는 먼저 실행 합니다.  
  
 예를 들어 트랜잭션 A가 데이터 값 2로 곱하고 트랜잭션 B가 데이터 값에 1을 추가 합니다. 이제 데이터 값이 두는 것으로 가정 합니다. 0과 10입니다. 이러한 트랜잭션에 서로 실행 하는 경우 새 값 1, 21 트랜잭션 A가 먼저 실행 되는 경우 또는 2 및 22 경우 됩니다 트랜잭션 B는 먼저 실행 됩니다. 있지만 두 개의 트랜잭션이 실행 되는 순서는 각 값에 대해 다른 될까요? 첫 번째 값에서 첫 번째로 실행 되는 트랜잭션 및 트랜잭션 B에서 실행 되 면 첫 번째 두 번째 값을 새 값은 1과 22를 사용 합니다. 이 순서를 반대로 하는 경우 새 값은 2 및 21입니다. 트랜잭션은 serializable 22만 가능한 결과 1 개, 21 및 2를 하는 경우. 트랜잭션이 없습니다 1, 22 또는 2, 21 경우 직렬화 가능한 결과입니다.  
  
 따라서 이유는 순차성 바람직하지 무엇입니까? 즉, 이유는 하나의 트랜잭션이 나타나는지 중요는 완료 된 다음 트랜잭션이 시작 되기 전에? 다음 문제를 고려해 야 합니다. 영업 사원이 점원을 전송 하는 동시에 주문을 입력 합니다. 예를 들어는 영업 사원 Company-x의 주문을 입력 했는데, 커밋하지 않습니다 Company-x는 영업 사원은 지원 담당자에 여전히 사실을 알립니다. 클럭 열려 있는 모든 주문의 목록을 요청 및 Company-x의 순서를 검색 하 고 청구서를 보냅니다. 회사 X 담당자 결정 이제는 영업 사원 트랜잭션을 커밋하기 전에 변경 되므로 해당 순서를 변경 하려고 합니다. Company-x는 잘못 된 청구서를 가져옵니다.  
  
 영업 사원의 및 clerk의 트랜잭션을 직렬화 할 수 인 경우이 문제가 발생 하지 합니다. 올바른 청구서 아웃 클럭은 전송한 경우 clerk의 트랜잭션이 시작 되기 전에 완료는 영업 사원의 트랜잭션 또는 경우에 영업 사원 트랜잭션이 시작 되기 전에 clerk의 트랜잭션 완료는 클럭은 보내지 자재 명세서 Company-x에 전혀 합니다.
