---
title: 열 바인딩 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78a87884e075e4cbe3dcb914335994aba2e4159
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="binding-columns"></a>열 바인딩
데이터 원본에서 인출 되는 데이터는이 목적을 위해 응용 프로그램에서 할당 하는 변수에서 응용 프로그램에 반환 됩니다. 이 수행할 수 있습니다, 전에 응용 프로그램 연결 해야 합니다 또는 *바인딩할*, 결과의 열에 이러한 변수 설정; 개념적으로이 프로세스는 문 매개 변수를 응용 프로그램 변수 바인딩와 동일 합니다. 응용 프로그램 변수를 바인딩할 때 결과 집합 열, 변수를 설명-주소, 데이터 형식 등에-driver. 드라이버는 해당 문에 대 한 유지 관리 하 고 행을 인출할 때 열에서 값을 반환 하는 정보를 사용 하 여 구조에이 정보를 저장 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [바인딩 결과 집합 열](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [SQLBindCol 사용](../../../odbc/reference/develop-app/using-sqlbindcol.md)
