---
title: 프로시저 호출 | Microsoft Docs
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
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d01859ee1b44f29c1109e976cc4a59302306444
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="procedure-invocation"></a>프로시저 호출
사용 하 여 드라이버에서 프로시저를 호출할 수 Microsoft Access 드라이버를 사용 하는 경우는 **SQLExecDirect** 또는 **SQLPrepare** 함수를 다음 구문과 함께: {호출 *프로시저 이름*  [(*매개 변수*[,*매개 변수*]...)]을 (를). 참고가 호출된 된 프로시저에 매개 변수로 식은 지원 되지 않습니다.  
  
 프로시저 이름에 대시를 포함 하는 경우 이름을 역 따옴표 (')로 구분 되어야 합니다.  
  
 매개 변수가 있는 쿼리는 이전 문을 사용 하 여 호출할 수 있습니다.
