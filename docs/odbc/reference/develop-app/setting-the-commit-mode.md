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
ms.openlocfilehash: a43a78ad9453f65d9b12595851bd622f720b409a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094219"
---
# <a name="setting-the-commit-mode"></a>커밋 모드 설정
응용 프로그램 연결 특성 SQL_ATTR_AUTOCOMMIT 사용 하 여 트랜잭션 모드를 지정합니다. 기본적으로 ODBC 트랜잭션 자동 커밋 모드에 있는 (하지 않는 한 **SQLSetConnectAttr** 하 고 **SQLSetConnectOption** 지원 되지 않습니다 가능성이 없는). 수동 커밋 모드에서 자동 커밋 모드로 전환 자동으로 연결에서 모든 열린 트랜잭션을 커밋합니다.
