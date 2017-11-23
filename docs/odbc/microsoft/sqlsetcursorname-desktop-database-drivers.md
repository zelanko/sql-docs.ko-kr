---
title: "(데스크톱 데이터베이스 드라이버) SQLSetCursorName | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eb398e51768ea9261e360c3ce7088b4ee30ec128
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (데스크톱 데이터베이스 드라이버)
드라이버 위치 지정된 업데이트를 지원 하지 않거나는 WHERE CURRENT OF으로 삭제 하기 때문에 *m e* 구문 **SQLSetCursorName** 지원 되지만 위치 지정된 업데이트에 사용할 수 없습니다. 응용 프로그램을 사용 하 고 커서 라이브러리를 사용할 수 있는 경우에 사용할 수 있습니다 **SQLExtendedFetch**합니다.
