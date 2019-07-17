---
title: 커서 설정 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c47e534f069f810948189f2668d4ecdfbfa4ad79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107539"
---
# <a name="setting-up-the-cursor"></a>커서 설정
응용 프로그램 설정 결과 만드는 문을 실행 하기 전에 커서 유형을 지정할 수 있습니다. SQL_ATTR_CURSOR_TYPE 문 특성을 사용 하 여 수행합니다. 응용 프로그램에서 형식을 명시적으로 지정 하지 않으면, 정방향 전용 커서 사용 됩니다. 혼합된 커서를 가져오려면 응용 프로그램 키 집합 커서를 지정 하지만 결과 집합 크기 보다 작은 키 집합 크기를 선언 합니다.  
  
 키 집합 커서와 혼합 커서에 대 한 응용 프로그램의 키 집합 크기를 지정할 수도 있습니다. SQL_ATTR_KEYSET_SIZE 문 특성을 사용 하 여 수행합니다. 키 집합 크기는 기본적으로 0으로 설정 된 경우에 결과 집합의 크기를 키 집합 크기 설정 되 고 키 집합 커서는. 커서가 열린 후 키 집합 크기를 변경할 수 있습니다.  
  
 응용 프로그램 행 집합 크기를 설정할 수도 자세한 내용은 [블록 커서를 사용 하 여](../../../odbc/reference/develop-app/using-block-cursors.md)이 섹션의 앞부분에 나오는.
