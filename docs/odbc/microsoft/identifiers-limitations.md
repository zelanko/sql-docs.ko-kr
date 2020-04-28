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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7154f2db09b69e6376b1fe3af1de3f2c646ee94e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286253"
---
# <a name="identifiers-limitations"></a>식별자 제한 사항
식별자에 공백이 나 특수 기호가 포함 된 경우에는 식별자를 큰따옴표로 묶어야 합니다. 유효한 이름은 64 자 미만의 문자열 이며, 첫 번째 문자는 공백이 아니어야 합니다. 올바른 이름은 ' &#124; # *?와 같은 특수 문자를 포함할 수 없습니다. [ ] . ! $ .  
  
 백슬래시 (')로 단어를 둘러싸야 하지 않는 한 *ODBC 프로그래머 참조* 의 부록 C (또는 이러한 예약어의 축약 형태)에 나열 된 예약어를 식별자 (테이블 또는 열 이름)로 사용 하지 마십시오.
