---
title: "식별자 제한 사항 | Microsoft Docs"
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
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ec32697030d2ad4ede765879f83956692ed49914
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="identifiers-limitations"></a>식별자 제한 사항
식별자에 공백 또는 특수 기호가 있으면, 식별자 백 따옴표로 묶어야 합니다. 유효한 이름은는 첫 번째 문자 공백이 되지 않아야 하는 최대 64 자의 문자열입니다. 유효한 이름은 제어 문자 또는 특수 문자를 포함할 수 없습니다. ' &#124; # * ? [ ] . ! $ .  
  
 예약 된 단어의 부록 C에서 SQL 문법에 나열 된 사용 하지 마십시오는 *ODBC Programmer's Reference* (또는 이러한 예약 된 단어의 약식) 식별자 (즉, 테이블 또는 열 이름), 단어 뒤에 입력 하지 않으면 따옴표 (')입니다.
