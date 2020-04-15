---
title: 커서 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 805d8076c853513d86f9a3a92d9342d1224226c9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299803"
---
# <a name="setting-up-the-cursor"></a>커서 설정
응용 프로그램은 결과 집합을 만드는 문을 실행하기 전에 커서 유형을 지정할 수 있습니다. SQL_ATTR_CURSOR_TYPE 문 특성을 사용하면 이 작업을 수행합니다. 응용 프로그램에서 형식을 명시적으로 지정하지 않으면 정방향 전용 커서가 사용됩니다. 혼합 커서를 얻으려면 응용 프로그램은 키 집합 기반 커서를 지정하지만 결과 집합 크기보다 작은 키 집합 크기를 선언합니다.  
  
 키 집합 기반 및 혼합 커서의 경우 응용 프로그램에서 키 집합 크기를 지정할 수도 있습니다. SQL_ATTR_KEYSET_SIZE 문 특성을 사용하면 이 작업을 수행합니다. 키 집합 크기가 기본값인 0으로 설정된 경우 키 집합 크기는 결과 집합 크기로 설정되고 키 집합 기반 커서가 사용됩니다. 커서를 연 후 키 집합 크기를 변경할 수 있습니다.  
  
 응용 프로그램은 행 집합 크기를 설정할 수도 있습니다. 자세한 내용은 이 섹션의 앞에서 [블록 커서 사용(블록 커서 사용)을](../../../odbc/reference/develop-app/using-block-cursors.md)참조하십시오.
