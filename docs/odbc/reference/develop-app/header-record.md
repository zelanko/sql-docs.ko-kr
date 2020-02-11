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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139020"
---
# <a name="header-record"></a>헤더 레코드
헤더 레코드의 필드에는 반환 코드, 행 개수, 상태 레코드 수 및 실행 된 문의 유형을 포함 하 여 함수 실행에 대 한 일반 정보가 포함 됩니다. 함수에서 SQL_INVALID_HANDLE를 반환 하지 않는 경우 항상 헤더 레코드가 만들어집니다. 헤더 레코드의 전체 필드 목록은 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 함수 설명을 참조 하세요.
