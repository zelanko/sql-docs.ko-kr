---
title: 바인딩 열 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fca4cfb1455c91ca57f7b1769266e2040d6a3511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301824"
---
# <a name="binding-columns"></a>열 바인딩
데이터 원본에서 가져온 데이터는 응용 프로그램이 이 용도로 할당한 변수로 응용 프로그램에 반환됩니다. 이렇게 하기 전에 응용 프로그램은 결과 집합의 열에 이러한 변수를 연결하거나 *바인딩해야*합니다. 개념적으로 이 프로세스는 문 매개 변수에 바인딩하는 응용 프로그램 변수와 동일합니다. 응용 프로그램이 변수를 결과 집합 열에 바인딩하면 해당 변수(주소, 데이터 형식 등)를 드라이버에 설명합니다. 드라이버는 이 정보를 해당 명령문에 대해 유지 관리하는 구조에 저장하고 이 정보를 사용하여 행을 가져올 때 열에서 값을 반환합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [바인딩 결과 집합 열](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [SQLBindCol 사용](../../../odbc/reference/develop-app/using-sqlbindcol.md)
