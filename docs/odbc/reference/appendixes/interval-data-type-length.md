---
title: 간격 데이터 형식 길이 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68bb4daa47cb58d5a0ff7b680a2d2154fb14b345
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284323"
---
# <a name="interval-data-type-length"></a>간격 데이터 형식 길이
다음 규칙은 문자의 간격 데이터 형식의 길이를 결정하는 데 사용됩니다. 길이는 문자 수로 표현됩니다. 바이트 수는 문자 집합에 따라 다릅니다. 길이에는 함께 추가된 다음 값이 포함됩니다.  
  
-   선행 필드가 아닌 간격의 모든 필드에 대해 두 문자입니다.  
  
-   선행 필드의 경우 express 또는 암시적 선행 정밀도인 문자 수입니다. 선행 정밀도를 지정하지 않으면 기본값은 2입니다.  
  
-   필드 사이의 구분 기호에 대한 하나의 문자입니다.  
  
-   하나 플러스 익스프레스 또는 내재 초 정밀도. 초 정밀도를 지정하지 않으면 기본값은 6입니다.  
  
 각 간격 데이터 형식에 대한 특정 열 길이 값은 [열 크기에](../../../odbc/reference/appendixes/column-size.md)포함되어 있습니다.
