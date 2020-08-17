---
description: '5단계: 트랜잭션 커밋'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4cc3a73e5cfc564992795ab6b18759b1066288c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385899"
---
# <a name="step-5-commit-the-transaction"></a>5단계: 트랜잭션 커밋
다음 단계는 다음 그림과 같이 트랜잭션을 커밋하는 것입니다.  
  
 ![트랜잭션을 커밋하는 방법](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 다섯 번째 단계는 **Sqlendtran** 을 호출 하 여 트랜잭션을 커밋하거나 롤백해야 합니다. 응용 프로그램은 트랜잭션 커밋 모드를 수동 커밋으로 설정한 경우에만이 단계를 수행 합니다. 트랜잭션 커밋 모드가 기본값인 자동 커밋 인 경우 문이 실행 될 때 트랜잭션이 자동으로 커밋됩니다. 자세한 내용은 [트랜잭션](../../../odbc/reference/develop-app/transactions-odbc.md)을 참조하세요.  
  
 새 트랜잭션에서 문을 실행 하기 위해 응용 프로그램은 3 단계로 돌아옵니다. 데이터 원본에서 연결을 끊으려면 응용 프로그램이 6 단계로 진행 됩니다.
