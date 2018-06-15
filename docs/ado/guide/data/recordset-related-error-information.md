---
title: 레코드 집합 관련 오류 정보 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55f64646050eba8c76432c68c39b36b0daa9f4be
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272352"
---
# <a name="recordset-related-error-information"></a>레코드 집합 관련 오류 정보
일괄 처리 하는 동안는 **상태** 속성은 **레코드 집합** 의 개별 레코드에 대 한 정보를 제공 하는 개체는 **레코드 집합**합니다. 일괄 업데이트 이루어지기 전에 **상태** 의 속성은 **레코드 집합** 레코드를 추가, 변경 및 삭제 하는 방법에 대 한 정보를 반영 합니다. 후 **UpdateBatch** 호출한 다음에 **상태** 속성은 작업의 성공 여부를 나타냅니다. 레코드를 이동 하면는 **레코드 집합**의 값은 **상태** 현재 레코드의 상태를 설명 하기 위해 속성 변경 합니다.
