---
title: 순차성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6e912ec51bc0b7c77d73aae1b473dee9242b3f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913628"
---
# <a name="serializability"></a>순차성
트랜잭션을 여야 가장 바람직합니다 *직렬화 가능*합니다. 에 트랜잭션을 동시에 실행의 결과 동일한 결과를 직렬로 실행 하는 경우 직렬화 가능 트랜잭션이 있다고-즉, 하나씩 있습니다. 중요 하지 않습니다 트랜잭션 실행 먼저는 결과 트랜잭션의 모든 혼합을 반영 하지 않습니다.  
  
 예를 들어 트랜잭션 A 데이터 값 2로 곱하고 트랜잭션 B는 데이터 값에 1을 추가 합니다. 이제 두 개의 데이터 값 된다고 가정해 봅니다. 0과 10입니다. 즉 이러한 트랜잭션이 실행 될 경우 새 값 됩니다 1, 21 트랜잭션 A는 먼저 실행 되는 경우 또는 2 및 22 트랜잭션 B는 처음 실행 되는 경우. 하지만 두 개의 트랜잭션이 실행 되는 순서는 각 값에 대해 다른 경우에 어떻게? 트랜잭션 A는 첫 번째 값에서 처음 실행 되 고 트랜잭션 B에서 실행 되 면 첫 번째, 두 번째 값을 새 값은 1과 22를 사용 합니다. 이 순서는 반대 되는 경우 새 값은 2 및 21입니다. 직렬화 가능 트랜잭션은 22만 가능한 결과 1, 21-2, 하는 경우. 트랜잭션을 하지 serializable 경우 1, 22 또는 2, 21은 결과입니다.  
  
 따라서 이유는 순차성 바람직한 무엇입니까? 즉, 이것은 왜 중요 한 해당 트랜잭션 나타나는지 완료 된 다음 트랜잭션이 시작 되기 전에? 다음 문제를 고려해 야 합니다. 영업 사원 청구서를 전송 하는 클럭을 동시에 주문 입력 됩니다. 예를 들어는 영업 사원이 주문을 회사 X에서 했는데 하며 커밋하지 않습니다 영업 사원 란을 대표 하는 회사 X에서 여전히 동작 합니다. 클럭 열려 있는 모든 주문의 목록을 요청 하 고, 회사 X에 대 한 순서를 검색 하 고, 청구서를 보냅니다. 이제 회사 X 담당자는 영업 사원 트랜잭션을 커밋하기 전에 변경의 순서를 변경 하려는 결정 합니다. 회사 X 잘못 청구서를 가져옵니다.  
  
 외판원의 및 담당자 트랜잭션을 직렬화 할 수 인 경우이 문제가 발생 하지 합니다. 쿼리에서 점원이 전송지 않습니다 올바른 청구서의 클럭 트랜잭션이 시작 되기 전에 외판원의 트랜잭션 완료가 또는 쿼리에서 영업 사원 트랜잭션이 시작 전에 클럭 트랜잭션 완료 것 중 하나는 점원은 보내지 청구서 회사 X에 전혀 합니다.
