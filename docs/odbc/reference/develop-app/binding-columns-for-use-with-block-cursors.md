---
title: 블록 커서와 함께 사용 하기 위해 열을 바인딩 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9bee14abc4bbdbad17360666d40a7d59af5480d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="binding-columns-for-use-with-block-cursors"></a>블록 커서와 함께 사용 하기 위해 열 바인딩
블록 커서 여러 행을 반환 하므로 사용 하는 응용 프로그램을 사용 하 여 변수의 배열을 단일 변수 대신 각 열에 바인딩해야 합니다. 이러한 배열은 이라고 통칭는 *행 집합 버퍼*합니다. 바인딩의 두 가지 스타일은 다음과 같습니다.  
  
-   배열을 각 열에 바인딩하십시오. 이 라고 *열 단위 바인딩을* 각 데이터 구조 (배열) 단일 열에 대 한 데이터를 포함 합니다.  
  
-   하는 전체 행에 대 한 데이터를 보유 하 고 이러한 구조의 배열을 바인딩할 구조를 정의 합니다. 이 라고 *행 단위 바인딩을* 각 데이터 구조는 단일 행에 대 한 데이터를 포함 합니다.  
  
 호출 응용 프로그램 열에 단일 변수를 바인딩할 때 **SQLBindCol** 배열을 열으로 바인딩할 합니다. 유일한 차이점은 전달 된 주소 않는다는 배열 주소, 하지 단일 변수 주소입니다. 응용 프로그램 열 단위 또는 행 단위 바인딩 사용 여부를 지정 하려면 SQL_BIND_BY_COLUMN 문 특성을 설정 합니다. 응용 프로그램 기본 설정 하기에 열 단위 또는 행 단위 바인딩을 사용 하도록 여부입니다. 응용 프로그램의 데이터 레이아웃을 더욱 긴밀 하 게 일치 수 행 단위 바인딩은,이 경우 더 나은 성능을 제공할 것 것입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [열 단위 바인딩](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [행 단위 바인딩](../../../odbc/reference/develop-app/row-wise-binding.md)
