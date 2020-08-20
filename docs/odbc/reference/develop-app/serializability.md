---
description: 직렬화 가능성
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b627d24b16e0bae4a117dba38de8cc1755feadac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476445"
---
# <a name="serializability"></a>직렬화 가능성
이상적으로는 트랜잭션을 *직렬화*할 수 있어야 합니다. 트랜잭션이 동시에 실행 된 결과와 동일 하 게 실행 되는 경우 트랜잭션을 직렬화 할 수 있는 것으로 간주 합니다. 즉, 트랜잭션을 차례로 실행 한 결과와 동일 합니다. 트랜잭션이 먼저 실행 되는 것은 중요 하지 않으며 결과가 트랜잭션 혼합을 반영 하지 않습니다.  
  
 예를 들어 트랜잭션 A가 데이터 값을 2로 곱하고 트랜잭션 B가 데이터 값에 1을 추가 한다고 가정 합니다. 이제 0과 10 이라는 두 가지 데이터 값이 있다고 가정 합니다. 이러한 트랜잭션이 다른 트랜잭션에서 실행 되는 경우 새 값은 1과 21 (트랜잭션 A가 먼저 실행 되는 경우), 2, 22 (트랜잭션 B가 먼저 실행 되는 경우)가 됩니다. 그러나 두 트랜잭션이 실행 되는 순서는 각 값 마다 다를 수 있습니다. 첫 번째 값에서 트랜잭션 A를 먼저 실행 하 고 두 번째 값에서 트랜잭션 B를 먼저 실행 하는 경우 새 값은 1과 22입니다. 이 순서를 반대로 하는 경우 새 값은 2 및 21입니다. 1, 21 및 2, 22 인 경우에만 트랜잭션을 직렬화 할 수 있습니다. 1, 22 또는 2 인 경우 트랜잭션을 직렬화 할 수 없습니다.  
  
 순차성 바람직한 이유는 무엇 인가요? 즉, 다음 트랜잭션이 시작 되기 전에 하나의 트랜잭션이 완료 되는 것이 중요 한 이유는 무엇 인가요? 다음 문제를 고려 하십시오. 외판원는 주문이 청구서를 전송 하는 동시에 주문을 입력 합니다. 외판원가 회사 X에서 주문을 입력 하지만 커밋하지 않는 경우를 가정 합니다. 외판원는 여전히 회사 X에서 담당자와 통신 하 고 있습니다. 이 클럭은 모든 오픈 주문의 목록을 요청 하 고 회사 X에 대 한 주문을 검색 한 후 청구서를 보냅니다. 이제 회사 X의 담당자가 주문을 변경 하기로 결정 하므로 트랜잭션을 커밋하기 전에 외판원 변경 됩니다. 회사 X에서 잘못 된 청구서를 가져옵니다.  
  
 외판원의 및 클럭 트랜잭션이 serializable 인 경우이 문제가 발생 하지 않습니다. 외판원의 트랜잭션이 시작 된 후에는 클럭 트랜잭션이 시작 되기 때문에,이 경우에는 클럭이 올바른 청구서를 전송 하거나, 외판원의 트랜잭션이 시작 되기 전에 클럭의 트랜잭션이 완료 될 수 있습니다 .이 경우에는 클럭이 회사 X로 청구서를 전송 하지 않습니다.
