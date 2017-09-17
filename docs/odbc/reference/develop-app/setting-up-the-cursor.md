---
title: "커서를 설정 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0e7fda4fa942519384b2837f6f3f70a880dee74f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setting-up-the-cursor"></a>커서 설정
응용 프로그램 집합 결과 만드는 문을 실행 하기 전에 커서 유형을 지정할 수 있습니다. SQL_ATTR_CURSOR_TYPE 문 특성으로 수행합니다. 응용 프로그램에서 형식을 명시적으로 지정 하지 않으면, 정방향 전용 커서가 사용 됩니다. 혼합된 커서를 가져오려면 응용 프로그램 키 집합 커서를 지정 하지만 결과 집합 크기 보다 작은 키 집합 크기를 선언 합니다.  
  
 키 집합 커서와 혼합 커서에 대 한 응용 프로그램 키 집합 크기를 지정할 수도 있습니다. SQL_ATTR_KEYSET_SIZE 문 특성으로 수행합니다. 키 집합 크기의 기본 설정인 0으로 설정 된 경우 키 집합 크기는 결과 집합의 크기를 설정 되 고 키 집합 커서는 데 사용 됩니다. 커서가 열린 후 키 집합 크기를 변경할 수 있습니다.  
  
 응용 프로그램 행 집합 크기를 설정할 수도 자세한 내용은 참조 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md)이 섹션의 앞부분에 나오는 합니다.
