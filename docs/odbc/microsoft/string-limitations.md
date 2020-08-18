---
description: 문자열 제한 사항
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c21d86a3c626ced52c6b7915d3cfbd9322fb596e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449135"
---
# <a name="string-limitations"></a>문자열 제한 사항
SQL 문 문자열의 최대 길이는 65000 자입니다.  
  
 Microsoft Access 드라이버를 사용 하는 경우에는 큰따옴표를 사용 하지 않고 작은따옴표로 묶은 SQL-92 문자열 상수만 지원 됩니다.  
  
 파이프 문자 (&#124;)는 문자를 큰따옴표로 묶어야 하는지 여부에 관계 없이 문자열에 사용할 수 없습니다.  
  
 상호 운용성을 최대화 하기 위해 응용 프로그램은 따옴표로 묶은 문자열을 전달 하는 대신 매개 변수에서 문자열을 전달 해야 합니다.
