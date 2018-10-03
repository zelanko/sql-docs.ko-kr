---
title: '5 단계: 트랜잭션 커밋 | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 341f34afa1dbe65f4b83a46f461bb93f4fb4f4c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844300"
---
# <a name="step-5-commit-the-transaction"></a>5단계: 트랜잭션 커밋
다음 그림에 표시 된 대로 트랜잭션 커밋에 다음 단계가입니다.  
  
 ![트랜잭션을 커밋하는 방법을 보여 줍니다](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 다섯 번째 단계는 호출 하는 것 **SQLEndTran** 커밋 또는 트랜잭션을 롤백합니다. 응용 프로그램이 트랜잭션 커밋 모드를 수동 커밋;로 설정 하는 경우에이 단계를 수행 트랜잭션 커밋 모드가 자동으로 커밋되므로, 기본적으로는 문이 실행 될 때 트랜잭션이 자동으로 커밋될 때. 자세한 내용은 [트랜잭션을](../../../odbc/reference/develop-app/transactions-odbc.md)합니다.  
  
 새 트랜잭션에 문을 실행 하려면 응용 프로그램 3 단계를 반환 합니다. 데이터 원본에서 연결을 끊으려면 응용 프로그램은 6 단계로 진행 됩니다.
