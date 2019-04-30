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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c4147b1bfa5ffb1e379c3aa8be2c9ea2a9d2775
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240966"
---
# <a name="default-c-data-types"></a>기본 C 데이터 형식
응용 프로그램에서 SQL_C_DEFAULT를 지정 하는 경우 **SQLBindCol**를 **SQLGetData**, 또는 **SQLBindParameter**, 드라이버 가정 출력 또는 입력된 버퍼의 C 데이터 형식 열 또는 버퍼 바인딩되는 매개 변수의 SQL 데이터 형식에 해당 합니다.  
  
> [!IMPORTANT]  
>  상호 운용 가능한 응용 프로그램 SQL_C_DEFAULT를 사용 하지 마십시오. 대신 사용 하는 버퍼의 C 형식이 지정 항상 해야 합니다. 다음은 다음과 같은 이유로 드라이버 기본 C 형식을 항상 올바르게 확인할 수 없기 때문입니다.  
  
-   DBMS는 SQL 데이터 형식의 열 또는 매개 변수 승격, 드라이버 원본 SQL 데이터 형식의 열 또는 매개 변수를 확인할 수 없습니다. 따라서이 해당 기본 C 데이터 형식을 확인할 수 없습니다.  
  
-   드라이버를 확인할 수 없는 경우 서명할지 여부를 특정 열 이나 매개 변수를 종종 경우 처럼이 경우 드라이버를 확인할 수 없습니다 DBMS에 의해 처리 해당 기본 C 데이터 형식 인지 해야 서명 되거나 서명 되지 않은 합니다.  
  
     SQL_C_DEFAULT 프로그래밍 편의 위해 제공 하기 때문에 실제 C 데이터 형식을 지정 하는 경우 응용 프로그램 기능을 손실 되지 않습니다.  
  
 각 SQL 데이터 형식에 대 한 기본 C 데이터 형식을 표시 하는 테이블에 포함 되어 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)이 부록의 뒷부분에 나오는.
