---
title: 블록 커서에 사용할 열 바인딩 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 827f6ddca12f15ce0bce1773b9cbe26fae5069dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106228"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>블록 커서와 함께 사용하기 위해 열 바인딩
블록 커서는 여러 행을 반환 하므로이를 사용 하는 응용 프로그램은 단일 변수가 아니라 각 열에 변수 배열을 바인딩해야 합니다. 이러한 배열을 집합적으로 *행 집합 버퍼*라고 합니다. 바인딩의 두 가지 스타일은 다음과 같습니다.  
  
-   각 열에 배열을 바인딩합니다. 각 데이터 구조 (배열)는 단일 열에 대 한 데이터를 포함 하기 때문에이를 *열 단위 바인딩* 이라고 합니다.  
  
-   전체 행의 데이터를 포함 하는 구조체를 정의 하 고 이러한 구조체의 배열을 바인딩합니다. 각 데이터 구조는 단일 행에 대 한 데이터를 포함 하기 때문에이를 *행 단위 바인딩* 이라고 합니다.  
  
 응용 프로그램이 단일 변수를 열에 바인딩하는 것 처럼 **SQLBindCol** 를 호출 하 여 배열을 열에 바인딩합니다. 유일한 차이점은 전달 된 주소가 단일 변수 주소가 아니라 배열 주소 이기 때문입니다. 응용 프로그램은 SQL_BIND_BY_COLUMN statement 특성을 설정 하 여 열 단위 또는 행 단위 바인딩을 사용 하는지 여부를 지정 합니다. 열 단위 또는 행 단위 바인딩을 사용할지 여부는 주로 응용 프로그램 기본 설정에 따라 결정 됩니다. 행 단위 바인딩은 응용 프로그램의 데이터 레이아웃과 더 밀접 하 게 일치 하는 경우 성능을 향상 시킬 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [열 단위 바인딩](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [행 단위 바인딩](../../../odbc/reference/develop-app/row-wise-binding.md)
