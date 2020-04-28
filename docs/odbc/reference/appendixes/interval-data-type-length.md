---
title: Interval 데이터 형식 길이 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284323"
---
# <a name="interval-data-type-length"></a>간격 데이터 형식 길이
다음 규칙은 문자에서 간격 데이터 형식의 길이를 확인 하는 데 사용 됩니다. 길이는 문자 수로 표시 됩니다. 바이트 수는 문자 집합에 따라 달라 집니다. 길이는 함께 추가 되는 다음 값을 포함 합니다.  
  
-   선행 필드가 아닌 간격의 모든 필드에 대해 두 개의 문자  
  
-   선행 필드의 경우에는 express 또는 암시적인 선행 전체 자릿수에 해당 하는 문자 수입니다. 선행 전체 자릿수가 지정 되지 않은 경우 기본값은 2입니다.  
  
-   필드 사이의 구분 기호에 대 한 문자 하나입니다.  
  
-   하나는 express 또는 묵시적 초 전체 자릿수를 더한 값입니다. 초의 전체 자릿수가 지정 되지 않은 경우 기본값은 6입니다.  
  
 각 interval 데이터 형식에 대 한 특정 열 길이 값은 [열 크기](../../../odbc/reference/appendixes/column-size.md)에 포함 되어 있습니다.
