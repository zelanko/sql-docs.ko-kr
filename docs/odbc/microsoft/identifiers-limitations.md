---
title: 식별자 제한 사항 | Microsoft Docs
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
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 087d7ba056a5da10ae8d191592f06c312583b62b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="identifiers-limitations"></a>식별자 제한 사항
식별자에 공백 또는 특수 기호가 있으면, 식별자 백 따옴표로 묶어야 합니다. 유효한 이름은는 첫 번째 문자 공백이 되지 않아야 하는 최대 64 자의 문자열입니다. 유효한 이름은 제어 문자 또는 특수 문자를 포함할 수 없습니다: ' &#124; # *? [ ] . ! $ .  
  
 예약 된 단어의 부록 C에서 SQL 문법에 나열 된 사용 하지 마십시오는 *ODBC Programmer's Reference* (또는 이러한 예약 된 단어의 약식) 식별자 (즉, 테이블 또는 열 이름), 단어 뒤에 입력 하지 않으면 따옴표 (')입니다.
