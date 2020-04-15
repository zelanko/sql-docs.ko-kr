---
title: 64비트 정수 구조 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ecbe4dae4c1bd21ac3d542ee0d9b18169df0116
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307514"
---
# <a name="64-bit-integer-structures"></a>64비트 정수 구조
Microsoft C 컴파일러의 SQL_C_SBIGINT 및 SQL_C_UBIGINT 데이터 형식 식별자에 대한 C 형식은 _int64. Microsoft® C 컴파일러 이외의 컴파일러를 사용하는 경우 C 형식이 다를 수 있습니다. 컴파일러가 기본적으로 64비트 정수를 지원하는 경우 드라이버 또는 응용 프로그램은 ODBCINT64를 기본 64비트 정수 유형으로 정의해야 합니다. 컴파일러가 기본적으로 64비트 정수를 지원하지 않는 경우 응용 프로그램 이나 드라이버는 다음 구조를 정의하여 이 데이터에 액세스할 수 있는지 확인할 수 있습니다.  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 64비트 정수는 8바이트 경계에 정렬되므로 이러한 구조는 8바이트 경계에 정렬되어야 합니다.
