---
title: "64 비트 정수 구조 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 15176629e0154b59c1dfadd9d58f755eb2c423ed
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="64-bit-integer-structures"></a>64 비트 정수 구조
Microsoft C 컴파일러에서 SQL_C_SBIGINT 및 SQL_C_UBIGINT 데이터 형식 식별자에 대 한 C 형식은 _int64 합니다. Microsoft® C 컴파일러 아닌 다른 컴파일러를 사용 하는 경우 C 형식 달라질 수 있습니다. 컴파일러에서는 64 비트 정수를 기본적으로 지원 드라이버 또는 응용 프로그램 ODBCINT64 네이티브 64 비트 정수 형식으로 정의 해야 합니다. 컴파일러가 64 비트 정수를 고유 하 게 지원 하지 않는 경우 응용 프로그램 또는 드라이버가이 데이터에 액세스할 수 있는지 확인 하는 다음 구조로 정의할 수 있습니다.  
  
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
  
 이러한 구조는 64 비트 정수는 8 바이트 경계에 맞춰집니다 때문에 8 바이트 경계에 맞춰야 합니다.
