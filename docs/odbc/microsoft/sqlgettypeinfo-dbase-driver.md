---
title: SQLGetTypeInfo (dBASE 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 711652e22318d089b02fe8e79cb592f0a42dfff9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295133"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo(dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 **SQLGetTypeInfo에서** 생성한 테이블에서 반환되는 형식(TYPE_NAME)의 이름은 데이터 원본에서 가장 일반적으로 사용되는 이름입니다.  
  
 SQL_ALL_EXCEPT_LIKE 바이트, 카운터, 더블, 단일, 긴 및 짧은 데이터 형식에 대한 검색 가능한 열에 반환됩니다. (LIKE 기능은 ODBC 표준 변환 함수를 사용하여 값을 문자로 변환한 다음 비교를 수행하여 달성할 수 있습니다.)
