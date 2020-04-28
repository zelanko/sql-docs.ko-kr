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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f05aaca2349a612cda7c5b6b257e7a1d5a5ea9c5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299823"
---
# <a name="setting-the-commit-mode"></a>커밋 모드 설정
응용 프로그램은 SQL_ATTR_AUTOCOMMIT 연결 특성을 사용 하 여 트랜잭션 모드를 지정 합니다. 기본적으로 ODBC 트랜잭션은 자동 커밋 모드에 있습니다 ( **SQLSetConnectAttr** 및 **SQLSetConnectOption** 가 지원 되지 않는 경우). 수동 커밋 모드에서 자동 커밋 모드로 전환 하면 연결에서 열려 있는 트랜잭션이 자동으로 커밋됩니다.
