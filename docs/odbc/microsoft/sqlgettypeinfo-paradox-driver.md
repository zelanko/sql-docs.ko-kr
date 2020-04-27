---
title: SQLGetTypeInfo (Paradox 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 693441c088865be85b18106a4c769a9f3f676f13
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "81295103"
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 **SQLGetTypeInfo** 에서 생성 된 테이블에 반환 되는 형식 (TYPE_NAME)의 이름은 데이터 원본에서 가장 일반적으로 사용 되는 이름입니다.  
  
 바이트, 카운터, Double, Single, Long 및 Short 데이터 형식에 대 한 검색 가능 열에 SQL_ALL_EXCEPT_LIKE 반환 됩니다. (ODBC 정식 변환 함수를 사용 하 여 값을 문자로 변환한 다음 비교를 수행 하 여 LIKE 기능을 구현할 수 있습니다.)
