---
description: 64비트 정수 구조
title: 64 비트 정수 구조 | Microsoft Docs
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
ms.openlocfilehash: 13c57fc582b23c3ca10768c930d44ae758f1d3d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471246"
---
# <a name="64-bit-integer-structures"></a>64비트 정수 구조
Microsoft C 컴파일러의 SQL_C_SBIGINT 및 SQL_C_UBIGINT 데이터 형식 식별자에 대 한 C 형식은 _int64 됩니다. Microsoft® C 컴파일러 이외의 컴파일러를 사용 하는 경우 C 형식이 다를 수 있습니다. 컴파일러가 64 비트 정수를 기본적으로 지 원하는 경우 드라이버 또는 응용 프로그램은 ODBCINT64를 네이티브 64 비트 정수 형식으로 정의 해야 합니다. 컴파일러가 64 비트 정수를 기본적으로 지원 하지 않는 경우 응용 프로그램 또는 드라이버는 다음 구조를 정의 하 여이 데이터에 액세스할 수 있는지 확인할 수 있습니다.  
  
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
  
 64 비트 정수가 8 바이트 경계에 맞춰지도록 이러한 구조체는 8 바이트 경계에 정렬 되어야 합니다.
