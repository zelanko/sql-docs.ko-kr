---
title: 절차 호출 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32617cdb753f5fc1b9c52520cb609d2902137b54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290774"
---
# <a name="procedure-invocation"></a>프로시저 호출
Microsoft Access 드라이버를 사용할 때 다음 구문으로 **SQLExecDirect** 또는 **SQLPrepare** 함수를 사용하여 드라이버에서 프로시저를 호출할*parameter*수 있습니다. *procedure-name* *parameter* 식은 호출된 프로시저의 매개 변수로 지원되지 않습니다.  
  
 프로시저 이름에 대시가 포함된 경우 이름은 따옴표(')로 구분되어야 합니다.  
  
 매개 변수화된 쿼리는 이전 문을 사용하여 호출할 수 있습니다.
