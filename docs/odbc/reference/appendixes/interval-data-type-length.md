---
title: 간격 데이터 형식 길이 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a456db12ddb2594dc7b4c9e4f5c26e9cb4245621
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947593"
---
# <a name="interval-data-type-length"></a>간격 데이터 형식 길이
다음 규칙은 문자에서 간격 데이터 형식의 길이 확인 하는 데 사용 됩니다. 길이 문자의 수로 표시 됩니다. 문자 집합을 따라 바이트 수가 달라 집니다. 길이 함께 추가 하는 다음과를 같습니다.  
  
-   선행 필드가 없는 간격의 모든 필드에 대해 두 문자입니다.  
  
-   명시적 또는 암시적 문자 수가 선행 필드의 경우 전체 자릿수를 유도 합니다. 선행 정밀도 지정 하지 않은 경우 기본값은 2입니다.  
  
-   하나의 필드 사이의 구분 기호 문자입니다.  
  
-   1을 더한 값 명시적 또는 묵시적 초 전체 자릿수입니다. 초 전체 자릿수를 지정 하지 않으면 기본값은 6입니다.  
  
 각 간격 데이터 형식에 대 한 특정 열 길이 값에 포함 된 [열 크기](../../../odbc/reference/appendixes/column-size.md)합니다.
