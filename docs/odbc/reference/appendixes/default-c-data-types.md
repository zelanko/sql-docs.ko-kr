---
title: 기본 C 데이터 유형 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307054"
---
# <a name="default-c-data-types"></a>기본 C 데이터 형식
응용 프로그램이 **SQLBindCol,** **SQLGetData**또는 **SQLBindParameter에서**SQL_C_DEFAULT 지정하는 경우 드라이버는 출력 또는 입력 버퍼의 C 데이터 형식이 버퍼가 바인딩된 열 또는 매개 변수의 SQL 데이터 형식에 해당한다고 가정합니다.  
  
> [!IMPORTANT]  
>  상호 운용 가능한 응용 프로그램은 SQL_C_DEFAULT 사용해서는 안 됩니다. 대신 사용 중인 버퍼의 C 형식을 항상 지정해야 합니다. 이는 드라이버가 다음과 같은 이유로 항상 기본 C 유형을 올바르게 결정할 수 없기 때문입니다.  
  
-   DBMS가 열 또는 매개 변수의 SQL 데이터 형식을 승격하는 경우 드라이버는 열 또는 매개 변수의 원래 SQL 데이터 형식을 확인할 수 없습니다. 따라서 해당 기본 C 데이터 형식을 확인할 수 없습니다.  
  
-   드라이버가 특정 열이나 매개 변수가 서명되었는지 여부를 확인할 수 없는 경우( 종종 DBMS에서 이 열을 처리하는 경우) 드라이버는 해당 기본 C 데이터 형식의 서명 또는 서명되지 않았는지 여부를 결정할 수 없습니다.  
  
     SQL_C_DEFAULT 프로그래밍 편의를 위해서만 제공되므로 응용 프로그램은 실제 C 데이터 형식을 지정할 때 기능을 잃지 않습니다.  
  
 각 SQL 데이터 형식에 대한 기본 C 데이터 형식을 보여 미치는 테이블은 이 부록의 후반부에서 [SQL에서 C 데이터 유형으로 데이터를 변환하는 데](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)포함됩니다.
