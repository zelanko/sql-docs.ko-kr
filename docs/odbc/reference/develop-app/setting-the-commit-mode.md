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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094219"
---
# <a name="setting-the-commit-mode"></a>커밋 모드 설정
응용 프로그램은 SQL_ATTR_AUTOCOMMIT 연결 특성을 사용 하 여 트랜잭션 모드를 지정 합니다. 기본적으로 ODBC 트랜잭션은 자동 커밋 모드에 있습니다 ( **SQLSetConnectAttr** 및 **SQLSetConnectOption** 가 지원 되지 않는 경우). 수동 커밋 모드에서 자동 커밋 모드로 전환 하면 연결에서 열려 있는 트랜잭션이 자동으로 커밋됩니다.
