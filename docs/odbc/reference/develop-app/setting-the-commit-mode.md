---
title: 커밋 모드 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efc999a3644a9146e7195f0bbbb07d130172d30d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62445935"
---
# <a name="setting-the-commit-mode"></a>커밋 모드 설정
응용 프로그램 연결 특성 SQL_ATTR_AUTOCOMMIT 사용 하 여 트랜잭션 모드를 지정합니다. 기본적으로 ODBC 트랜잭션 자동 커밋 모드에 있는 (하지 않는 한 **SQLSetConnectAttr** 하 고 **SQLSetConnectOption** 지원 되지 않습니다 가능성이 없는). 수동 커밋 모드에서 자동 커밋 모드로 전환 자동으로 연결에서 모든 열린 트랜잭션을 커밋합니다.
