---
description: 레코드 집합 관련 오류 정보
title: 레코드 집합 관련 오류 정보 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: rothja
ms.author: jroth
ms.openlocfilehash: 454c62b969ee69e6186792ce77873c8c8fbb5704
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979814"
---
# <a name="recordset-related-error-information"></a>레코드 집합 관련 오류 정보
일괄 처리 중에 **레코드** 집합 개체의 **Status** 속성은 **레코드 집합**의 개별 레코드에 대 한 정보를 제공 합니다. 일괄 처리 업데이트를 수행 하기 전에 레코드 **집합** 의 **Status** 속성은 추가, 변경 및 삭제할 레코드에 대 한 정보를 반영 합니다. **UpdateBatch** 를 호출한 후 **Status** 속성은 작업의 성공 또는 실패를 나타냅니다. 레코드 **집합**의 레코드에서 레코드로 이동할 때 **status** 속성의 값이 변경 되어 현재 레코드의 상태를 설명 합니다.
