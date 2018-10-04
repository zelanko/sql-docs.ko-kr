---
title: 간격 이스케이프 시퀀스 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81481db74d973da0e54bc6bf9e70550fa3cc0c81
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767821"
---
# <a name="interval-escape-sequences"></a>간격 이스케이프 시퀀스
ODBC 간격 리터럴에 대 한 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
 {*간격 리터럴*}  
  
 BNF 구문에 대 한 *간격 리터럴*를 참조 합니다 [간격 리터럴 구문](../../../odbc/reference/appendixes/interval-literal-syntax.md) 이 부록의 뒷부분에 나오는 섹션입니다.  
  
 간격 리터럴 이스케이프 시퀀스는 데이터 원본에서 interval 데이터 형식을 지 원하는 경우 사용할 수 있습니다. 응용 프로그램에서 호출 해야 **SQLGetTypeInfo** 이러한 데이터 형식이 지원 되는지 여부를 확인 하려면.
