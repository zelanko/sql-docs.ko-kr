---
title: "레코드 집합 관련 오류 정보 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 279fcc0564f433234cbac730465e2af06a7eb5e7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-related-error-information"></a>레코드 집합 관련 오류 정보
일괄 처리 하는 동안는 **상태** 속성은 **레코드 집합** 의 개별 레코드에 대 한 정보를 제공 하는 개체는 **레코드 집합**합니다. 일괄 업데이트 이루어지기 전에 **상태** 의 속성은 **레코드 집합** 레코드를 추가, 변경 및 삭제 하는 방법에 대 한 정보를 반영 합니다. 후 **UpdateBatch** 호출한 다음에 **상태** 속성은 작업의 성공 여부를 나타냅니다. 레코드를 이동 하면는 **레코드 집합**의 값은 **상태** 현재 레코드의 상태를 설명 하기 위해 속성 변경 합니다.

