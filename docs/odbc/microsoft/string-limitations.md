---
title: 문자열 제한 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f81ff3da882095a0a6c41bb5061addd497a5d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306064"
---
# <a name="string-limitations"></a>문자열 제한 사항
SQL 문 문자열의 최대 길이는 65,000자입니다.  
  
 Microsoft Access 드라이버를 사용하는 경우 SQL-92 문자열 상수(단일 따옴표가 아닌 이중 따옴표)만 지원됩니다.  
  
 파이프 문자(&#124;)는 문자가 따옴표로 둘러싸여 있는지 여부에 관계없이 문자열에서 사용할 수 없습니다.  
  
 최대 상호 운용성을 위해 응용 프로그램은 인용된 문자열을 전달하는 대신 매개 변수로 문자열을 전달해야 합니다.
