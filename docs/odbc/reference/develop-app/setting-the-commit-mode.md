---
title: "커밋 모드 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 50fbb6064cdf8e36143958d9ef0d6558beeeab21
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="setting-the-commit-mode"></a>커밋 모드를 설정합니다.
응용 프로그램 연결 특성 SQL_ATTR_AUTOCOMMIT 사용 트랜잭션 모드를 지정 합니다. 기본적으로 ODBC 트랜잭션 자동 커밋 모드에 있는 (하지 않는 한 **SQLSetConnectAttr** 및 **SQLSetConnectOption** 지원 되지 않으며, 가능성이있지 않습니다). 자동으로 자동 커밋 모드를 수동 커밋 모드에서 전환 된 연결에서 모든 열린 트랜잭션을 커밋합니다.
