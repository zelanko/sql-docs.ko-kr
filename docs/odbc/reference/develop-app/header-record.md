---
title: 헤더 레코드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- header records [ODBC]
- diagnostic records [ODBC]
ms.assetid: d0fff1ed-5616-422a-a394-7ea1d2486f89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7f5fe5cf6aae0d5953cc82b845396dd4164c7fa3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139020"
---
# <a name="header-record"></a>헤더 레코드
헤더 레코드의 필드는 반환 코드, 행 개수, 상태 레코드의 수 및 실행 하는 문 유형 등 함수 실행에 대 한 일반 정보를 포함 합니다. 헤더 레코드는 함수에서 SQL_INVALID_HANDLE을 반환 하지 않는 한 항상 만들어집니다. 헤더 레코드의 필드의 전체 목록은 참조 합니다 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명 합니다.
