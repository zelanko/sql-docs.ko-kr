---
title: 기본 C 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdb787580e1c79df805f468416ab8993a1d32a26
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307054"
---
# <a name="default-c-data-types"></a>기본 C 데이터 형식
응용 프로그램에서 **SQLBindCol**, **SQLGetData**또는 **SQLBindParameter**의 SQL_C_DEFAULT 지정 하는 경우 드라이버는 출력 또는 입력 버퍼의 C 데이터 형식이 버퍼가 바인딩된 열 또는 매개 변수의 SQL 데이터 형식에 해당 하는 것으로 가정 합니다.  
  
> [!IMPORTANT]  
>  상호 운용 가능한 응용 프로그램은 SQL_C_DEFAULT를 사용 하면 안 됩니다. 대신 항상 사용 중인 버퍼의 C 형식을 지정 해야 합니다. 이는 다음과 같은 이유로 드라이버가 항상 기본 C 유형을 올바르게 결정할 수 없기 때문입니다.  
  
-   DBMS에서 열 또는 매개 변수의 SQL 데이터 형식을 승격 하는 경우 드라이버는 열 또는 매개 변수의 원래 SQL 데이터 형식을 확인할 수 없습니다. 따라서 해당 하는 기본 C 데이터 형식을 확인할 수 없습니다.  
  
-   드라이버가 특정 열 또는 매개 변수가 서명 되었는지 여부를 확인할 수 없는 경우에는 DBMS에서이를 처리 하는 경우가 종종 있으므로 드라이버는 해당 하는 기본 C 데이터 형식이 서명 되거나 서명 되지 않아야 하는지 여부를 확인할 수 없습니다.  
  
     SQL_C_DEFAULT은 프로그래밍 편의를 위해서만 제공 되므로 응용 프로그램은 실제 C 데이터 형식을 지정 하는 경우 기능을 손실 하지 않습니다.  
  
 각 SQL 데이터 형식에 대 한 기본 C 데이터 형식을 보여 주는 테이블은이 부록의 뒷부분에 나오는 [sql에서 c 데이터 형식으로 데이터를 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)하는 데 포함 됩니다.
