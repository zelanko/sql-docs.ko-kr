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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32617cdb753f5fc1b9c52520cb609d2902137b54
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81290774"
---
# <a name="procedure-invocation"></a>프로시저 호출
Microsoft Access 드라이버를 사용 하는 경우 다음 구문을 사용 하 여 **Sqlexecdirect** 또는 **sqlprepare** 함수를 사용 하 여 드라이버에서 프로시저를 호출할 수 있습니다. {CALL *procedure-name* [(*parameter*[,*parameter*] ...)]}. 식은 호출 된 프로시저에 대 한 매개 변수로 지원 되지 않습니다.  
  
 프로시저 이름에 대시가 포함 되어 있으면 이름을 백슬래시 (')로 구분 해야 합니다.  
  
 매개 변수가 있는 쿼리는 이전 문을 사용 하 여 호출할 수 있습니다.
