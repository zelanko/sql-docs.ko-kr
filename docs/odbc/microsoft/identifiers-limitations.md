---
title: 식별자 제한 사항 | 마이크로 소프트 문서
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
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7154f2db09b69e6376b1fe3af1de3f2c646ee94e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286253"
---
# <a name="identifiers-limitations"></a>식별자 제한 사항
식별자가 공백이나 특수 기호를 포함하는 경우 식별자를 따옴표로 묶아야 합니다. 유효한 이름은 64자 이하의 문자열이며, 그 중 첫 번째 문자는 공백이 아니어야 합니다. 유효한 이름에는 컨트롤 문자 또는 다음과 같은 특수 문자 &#124;가 포함될 수 없습니다. [ ] . ! $ .  
  
 *ODBC 프로그래머* 참조(또는 이러한 예약된 단어의 약어 형식)의 SQL 문법에 나열된 예약된 단어를 다시 따옴표(')로 단어를 둘러싸지 않는 한 식별자(즉, 테이블 또는 열 이름)로 사용하지 마십시오.
