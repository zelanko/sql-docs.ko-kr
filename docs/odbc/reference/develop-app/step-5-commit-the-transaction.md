---
title: "5 단계: 트랜잭션을 커밋하는 | Microsoft Docs"
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
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ac53209063a1204b57e7183501b5901dc8ea248
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="step-5-commit-the-transaction"></a>5 단계: 트랜잭션 커밋
다음 단계는 다음 그림에 나와 있는 것 처럼, 트랜잭션 커밋입니다.  
  
 ![트랜잭션을 커밋하는 방법을 보여 줍니다](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 다섯 번째 단계는 호출 하는 **SQLEndTran** 커밋하거나 트랜잭션을 롤백합니다. 응용 프로그램이 트랜잭션 커밋 모드 수동 커밋;로 설정 하는 경우에이 단계를 수행 트랜잭션 커밋 모드는 자동 커밋의 기본 설정인 문이 실행 될 때 트랜잭션이 자동으로 커밋될 때. 자세한 내용은 참조 [트랜잭션을](../../../odbc/reference/develop-app/transactions-odbc.md)합니다.  
  
 새 트랜잭션에 문을 실행 하려면 응용 프로그램 3 단계를 반환 합니다. 데이터 원본에서 연결을 끊을 응용 프로그램은 6 단계로 진행 됩니다.

