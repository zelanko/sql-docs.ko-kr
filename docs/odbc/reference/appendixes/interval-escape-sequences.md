---
title: 인터벌 이스케이프 시퀀스 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fe7f6941e9ec9fba8b6698faaa18a678732dd6f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304958"
---
# <a name="interval-escape-sequences"></a>간격 이스케이프 시퀀스
ODBC는 간격 리터럴에 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
 {*간격 리터럴*}  
  
 *인터벌 리터럴의*BNF 구문은 이 부록의 후반부 [리터럴 구문 간격](../../../odbc/reference/appendixes/interval-literal-syntax.md) 섹션을 참조하십시오.  
  
 간격 데이터 형식이 데이터 원본에서 지원되는 경우 간격 리터럴 이스케이프 시퀀스가 지원됩니다. 응용 프로그램은 **SQLGetTypeInfo를** 호출하여 이러한 데이터 형식이 지원되는지 확인해야 합니다.
