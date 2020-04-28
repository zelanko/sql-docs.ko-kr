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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d618a7f845a87394c2fc3c7978a7aef5716e21f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301484"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName(데스크톱 데이터베이스 드라이버)
드라이버가 WHERE CURRENT OF *cursorname* 구문을 사용 하 여 위치 지정 업데이트 또는 삭제를 지원 하지 않기 때문에 **SQLSetCursorName** 는 지원 되지만 위치 지정 업데이트에는 사용할 수 없습니다. 커서 라이브러리를 사용 하도록 설정 하 고 응용 프로그램에서 **Sqlextendedfetch**를 사용 하는 경우에만 사용할 수 있습니다.
