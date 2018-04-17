---
title: 제한 사항 문자열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a8e90ace4e237b7945da4a43ad869b79c657ab2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="string-limitations"></a>문자열 제한 사항
SQL 문의 문자열의 최대 길이 65, 000 자입니다.  
  
 Microsoft Access 드라이버를 사용 하는 경우에 SQL 92 문자열 상수 (작은따옴표, 큰따옴표 사용 되지 않습니다) 지원 됩니다.  
  
 파이프 문자 (&#124;) 여부 백 따옴표로 문자가 포함 되어 있는지 여부를 문자열에 사용할 수 없습니다.  
  
 상호 운용성을 극대화 응용 프로그램 문자열 매개 변수를 전달 해야 보다는 전달은 따옴표로 묶을 문자열입니다.
