---
title: 여러 트랜잭션 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], multiple
- multiple transactions
ms.assetid: c3664a94-be89-40c0-a3a0-84b74a7fedbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1c922fb612faca72e9f9381990dc777301185cb1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176583"
---
# <a name="multiple-transactions"></a>여러 트랜잭션
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지 내의 관련 없는 트랜잭션을 한 개의 패키지가 포함하는 것이 가능합니다. 중첩 컨테이너 계층 중간의 컨테이너가 트랜잭션을 지원하지 않으면 위 또는 아래에 위치한 컨테이너에서 별도의 트랜잭션을 시작합니다(트랜잭션을 지원하도록 구성된 경우). 트랜잭션은 중첩 컨테이너 계층의 가장 안쪽 태스크부터 순서대로 패키지에 커밋 또는 롤백합니다. 그러나 내부 트랜잭션이 커밋한 후에는 외부 트랜잭션이 중단되더라도 롤백하지 않습니다.

## <a name="illustration-of-multiple-transactions"></a>다중 트랜잭션의 그림
 예를 들어 한 패키지가 두 개의 Foreach 루프 컨테이너를 포함하고 각 컨테이너가 다시 두 개의 SQL 실행 태스크를 포함하는 경우 시퀀스 컨테이너는 트랜잭션을 지원하지만 Foreach 루프 컨테이너는 지원하지 않고 SQL 실행 태스크는 지원합니다. 이 예에서 각 SQL 실행 태스크는 자체 트랜잭션을 시작하며 시퀀스 태스크에서 트랜잭션이 중단된 경우에도 롤백하지 않습니다.

 시퀀스 컨테이너, Foreach 루프 컨테이너 및 SQL 실행 태스크의 TransactionOption 속성은 다음과 같이 설정됩니다.

-   시퀀스 컨테이너의 TransactionOption 속성은 **Required**로 설정됩니다.

-   Foreach 루프 컨테이너의 TransactionOption 속성은 **NotSupported**로 설정됩니다.

-   SQL 실행 태스크의 TransactionOption 속성은 **Required**로 설정됩니다.

 다음 다이어그램에서는 패키지 내의 관련 없는 트랜잭션 다섯 개를 보여 줍니다. 한 개의 트랜잭션은 시퀀스 컨테이너에서 시작되며 네 개의 트랜잭션은 SQL 실행 태스크에서 시작됩니다.

 ![다중 트랜잭션 구현](media/mw-dts-trans2.gif "다중 트랜잭션 구현")

## <a name="related-tasks"></a>관련 작업
 [트랜잭션을 사용하도록 패키지 구성](../relational-databases/native-client-ole-db-transactions/transactions.md)


