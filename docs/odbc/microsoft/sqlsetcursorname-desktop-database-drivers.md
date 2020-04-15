---
title: SQLSetCursorName (데스크톱 데이터베이스 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301484"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName(데스크톱 데이터베이스 드라이버)
드라이버는 WHERE CURRENT OF *커서이름* 구문에 의해 위치 된 업데이트 또는 삭제를 지원 하지 않습니다 때문에 **SQLSetCursorName** 지원 되지만 위치 된 업데이트에 사용할 수 없습니다. 커서 라이브러리를 사용하도록 설정하고 응용 프로그램에서 **SQLExtendedFetch**를 사용하는 경우에만 사용할 수 있습니다.
