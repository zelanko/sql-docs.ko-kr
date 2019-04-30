---
title: 프로시저 호출 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b33bc399646a6d274c875abd36d53219a2814e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200513"
---
# <a name="procedure-invocation"></a>프로시저 호출
프로시저를 사용 하 여 드라이버에서 호출할 수 Microsoft Access 드라이버를 사용 하는 경우는 **SQLExecDirect** 하거나 **SQLPrepare** 다음 구문 사용 하 여 함수: {호출 *프로시저 이름*  [(*매개 변수*[합니다*매개 변수*]...)]을 (를). 참고 식 호출된 된 프로시저에 매개 변수로 지원 되지 않습니다.  
  
 프로시저 이름에 대시를 포함 하는 경우 백 따옴표 (')를 사용 하 여 이름을 구분 해야 합니다.  
  
 매개 변수가 있는 쿼리는 이전 문을 사용 하 여 호출할 수 있습니다.
