---
title: 블록 커서와 함께 사용하기 위한 바인딩 열 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e527658a7d6945921510de898c648075c41fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284903"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>블록 커서와 함께 사용하기 위해 열 바인딩
블록 커서는 여러 행을 반환하므로 이를 사용하는 응용 프로그램은 단일 변수 대신 각 열에 변수 배열을 바인딩해야 합니다. 이러한 배열을 집합적으로 *행 집합 버퍼라고 합니다.* 다음은 바인딩의 두 가지 스타일입니다.  
  
-   배열을 각 열에 바인딩합니다. 각 데이터 구조(배열)에는 단일 열에 대한 데이터가 포함되어 있으므로 *열별 바인딩이라고* 합니다.  
  
-   전체 행에 대한 데이터를 보관하고 이러한 구조의 배열을 바인딩할 구조를 정의합니다. 각 데이터 구조에는 단일 행에 대한 데이터가 포함되어 있으므로 *행 별 바인딩이라고* 합니다.  
  
 응용 프로그램이 단일 변수를 열에 바인딩할 **때와 마찬가지로 SQLBindCol을** 호출하여 배열을 열에 바인딩합니다. 유일한 차이점은 전달된 주소가 단일 변수 주소가 아니라 배열 주소라는 것입니다. 응용 프로그램은 SQL_BIND_BY_COLUMN 문 특성을 설정하여 열 별 바인딩을 사용하고 있는지 또는 행별 바인딩을 사용하고 있는지 여부를 지정합니다. 열 별 바인딩을 사용할지 또는 행별 바인딩을 사용할지 여부는 주로 응용 프로그램 기본 설정의 문제입니다. 행 별 바인딩은 응용 프로그램의 데이터 레이아웃에 더 가깝게 대응할 수 있으며, 이 경우 더 나은 성능을 제공할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [열 별 바인딩](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [행 별 바인딩](../../../odbc/reference/develop-app/row-wise-binding.md)
