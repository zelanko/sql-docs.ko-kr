---
title: SQLSetCursorName (데스크톱 데이터베이스 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e433e6aee341085965f361992fc8ea9ac8744353
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305626"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName(데스크톱 데이터베이스 드라이버)
드라이버 위치 지정된 업데이트를 지원 하지 않거나는 WHERE CURRENT OF에서 삭제 되므로 *cursorname* 구문을 **SQLSetCursorName** 지원 되지만 위치 지정된 업데이트에 사용할 수 없습니다. 응용 프로그램을 사용 하 고 커서 라이브러리를 사용 하도록 설정 하는 경우에 사용 수 있습니다 **SQLExtendedFetch**합니다.
