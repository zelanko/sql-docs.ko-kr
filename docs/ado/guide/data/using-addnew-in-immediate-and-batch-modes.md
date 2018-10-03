---
title: 즉시에서 AddNew 및 일괄 처리 모드를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6295e4499a6f6f25f9111497012f2e9f1d6dc421
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616652"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>직접 실행 및 일괄 처리 모드에서 AddNew 사용
동작 합니다 **AddNew** 메서드의 업데이트 모드에 따라 달라 집니다 합니다 **레코드 집합** 개체를 전달 하는지 여부를 *FieldList* 및 *값*인수.  
  
 즉시 업데이트 모드에서는 (는 공급자 변경 기록의 데이터 원본에 호출 되 면를 **업데이트** 메서드)를 호출 합니다 **AddNew** 인수 집합이 없는 메서드는  **EditMode** 속성을 **adEditAdd 합니다.** 공급자 필드 값 변경 내용을 로컬로 캐시합니다. 호출 된 **업데이트** 메서드는 데이터베이스에 새 레코드를 게시 하 고 다시 설정 합니다 **EditMode** 속성을 **adEditNone 합니다.** 전달 하는 경우는 *FieldList* 하 고 *값* 인수, 게시 데이터베이스에 새 레코드를 즉시 ADO (없습니다 **업데이트** 호출 되기), **EditMode**  속성 값이 변경 되지 않습니다 (**adEditNone**).  
  
 일괄 업데이트 모드를 호출 합니다 **AddNew** 인수 집합이 없는 메서드는 **EditMode** 속성을 **adEditAdd**합니다. 공급자 필드 값 변경 내용을 로컬로 캐시합니다. 호출을 **업데이트** 메서드는 현재 새 레코드를 추가 합니다. **레코드 집합** 다시 설정 하 고는 **EditMode** 속성을 **adEditNone**, 하지만 공급자를 호출할 때까지 기본 데이터베이스에 변경 내용을 게시 하지 않습니다 합니다 **UpdateBatch** 메서드. 전달 하는 경우는 *FieldList* 및 *값* 인수를 ADO 저장소 캐시에 대 한 공급자에 게 새 레코드를 보냅니다; 호출 해야 합니다 **UpdateBatch** 새 게시 하는 방법 기본 데이터베이스에 기록 합니다. 에 대 한 자세한 내용은 **업데이트** 및 **UpdateBatch**를 참조 하십시오 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.
