---
title: 식별자 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 251ae0e4e94cec903e2c4b5cf687ed9b8b41dfc8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952394"
---
# <a name="identifiers-limitations"></a>식별자 제한 사항
식별자는 공백이 나 특수 기호가 있으면 식별자 백 따옴표로 묶어야 합니다. 유효한 이름은는 첫 번째 문자 공백이 되지 않아야 하는 64 개 이상 문자의 문자열을 보여 줍니다. 유효한 이름은 제어 문자나 특수 문자를 포함할 수 없습니다. ' &#124; # *? [ ] . ! $ .  
  
 예약 된 단어의 부록 C에서 SQL 문법에 나열 된 사용 하지 마세요 합니다 *ODBC 프로그래머 참조* (또는 이러한 예약 된 단어의 축약형) 식별자 (즉, 테이블 또는 열 이름), 단어 뒤에 넣으면 하지 않는 한 작은따옴표 (')입니다.
