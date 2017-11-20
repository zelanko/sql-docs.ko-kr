---
title: "기본 C 데이터 형식 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83040ffdab8b9715fc8caeb024bec6a9fc05d4d4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="default-c-data-types"></a>기본 C 데이터 형식
응용 프로그램에서 SQL_C_DEFAULT를 지정 하는 경우 **SQLBindCol**, **SQLGetData**, 또는 **SQLBindParameter**, 드라이버는 출력 또는 입력된 버퍼의 C 데이터 형식을 가정 열 또는 매개 변수 버퍼 바인딩되는 변수의 SQL 데이터 형식에 해당 합니다.  
  
> [!IMPORTANT]  
>  상호 운용 가능한 응용 프로그램 SQL_C_DEFAULT를 사용 해야 합니다. 대신, 사용 하는 버퍼의 C 형식의 항상 지정 해야 합니다. 다음은 다음과 같은 이유로 드라이버 기본 C 형식을 항상 올바르게 확인할 수 없기 때문입니다.  
  
-   DBMS에서 SQL 데이터 형식 열 또는 매개 변수를 승격 하는 경우 드라이버는 원래 SQL 데이터 형식의 열 또는 매개 변수는 확인할 수 없습니다. 따라서 그는 해당 기본 C 데이터 형식을 확인할 수 없습니다.  
  
-   드라이버 확인할 수 없는 경우 특정 열 또는 매개 변수는 서명 되었는지를, 종종의 경우 처럼이 드라이버를 확인할 수 없습니다는 DBMS에 의해 처리 해당 기본 C 데이터 형식 인지 해야 수 서명 되거나 서명 되지 않은 합니다.  
  
     SQL_C_DEFAULT 프로그래밍 편의 위해 제공 하기 때문에 실제 C 데이터 형식을 지정 하는 경우 응용 프로그램 기능을 손실 하지 않습니다.  
  
 각 SQL 데이터 형식에 대 한 기본 C 데이터 형식을 표시 하는 테이블에 포함 되어 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)이 부록의 뒷부분에 나오는 합니다.

