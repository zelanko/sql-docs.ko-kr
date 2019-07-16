---
title: 문자열 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7faab41bd52397ac0d352e04a9ec153571e93f1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948769"
---
# <a name="string-limitations"></a>문자열 제한 사항
SQL 문 문자열의 최대 길이 65,000 개 문자입니다.  
  
 Microsoft Access 드라이버를 사용 하는 경우에 SQL-92 문자열 상수 (작은따옴표를 큰따옴표로 표시 되지 않습니다) 지원 됩니다.  
  
 파이프 문자 (&#124;) 아닌지 백 따옴표에서 문자가 포함 되어 있는지 여부를 문자열에서 사용할 수 없습니다.  
  
 최대 상호 운용성을 위해 응용 프로그램 매개 변수에서 문자열을 전달 해야 것이 아니라 전달 quoted 문자열.
