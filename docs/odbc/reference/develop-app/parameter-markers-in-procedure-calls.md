---
title: 프로시저 호출에 매개 변수 표식을 | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 744c9d8a7c75df66439794f1b461112800094ba7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-markers-in-procedure-calls"></a>프로시저 호출에 매개 변수 표식
매개 변수를 허용 하는 프로시저를 호출할 때 상호 운용 가능한 응용 프로그램 리터럴 매개 변수 값 대신 매개 변수 표식을 사용 해야 합니다. 일부 데이터 원본 프로시저 호출에 리터럴 매개 변수 값의 사용을 지원 하지 않습니다. 매개 변수에 대 한 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다. 프로시저를 호출 하는 방법에 대 한 자세한 내용은 참조 [프로시저 호출](../../../odbc/reference/develop-app/procedure-calls.md)이 섹션의 뒷부분에 나오는 합니다.
