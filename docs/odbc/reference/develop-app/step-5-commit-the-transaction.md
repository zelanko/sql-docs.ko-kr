---
title: '5단계: 거래 커밋 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e348ce697e512f30db46d14535cf19bd6d530f61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283353"
---
# <a name="step-5-commit-the-transaction"></a>5단계: 트랜잭션 커밋
다음 단계는 다음 그림과 같이 트랜잭션을 커밋하는 것입니다.  
  
 ![트랜잭션을 커밋하는 방법](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 다섯 번째 단계는 **SQLEndTran을** 호출하여 트랜잭션을 커밋하거나 롤백하는 것입니다. 응용 프로그램은 트랜잭션 커밋 모드를 수동 커밋으로 설정한 경우에만 이 단계를 수행합니다. 트랜잭션 커밋 모드가 기본값인 자동 커밋인 경우 문이 실행될 때 트랜잭션이 자동으로 커밋됩니다. 자세한 내용은 [트랜잭션](../../../odbc/reference/develop-app/transactions-odbc.md)을 참조하세요.  
  
 새 트랜잭션에서 문을 실행하려면 응용 프로그램이 3단계로 돌아갑니다. 데이터 원본에서 연결을 끊기 위해 응용 프로그램은 6단계로 진행됩니다.
