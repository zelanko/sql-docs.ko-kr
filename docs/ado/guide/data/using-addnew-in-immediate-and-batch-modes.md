---
title: "즉시에서 AddNew 및 일괄 처리 모드를 사용 하 여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f22ae3e595c68b52e7eca449557e647c3bedae78
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>즉시에서 AddNew 및 일괄 처리 모드를 사용 하 여
동작은 **AddNew** 방법은의 업데이트 모드에 따라는 **레코드 집합** 개체와 전달 하는지 여부를 *FieldList* 및 *값*인수입니다.  
  
 즉시 업데이트 모드에서 (있는 공급자 변경 기록의 데이터 원본에 호출한 후의 **업데이트** 메서드)를 호출는 **AddNew** 인수 없이 메서드는  **EditMode** 속성을 **adEditAdd 합니다.** 공급자에는 필드 값 변경 내용을 로컬로 캐시합니다. 호출 된 **업데이트** 데이터베이스에 새 레코드에 게시 하 고 다시 설정 하는 메서드는 **EditMode** 속성을 **adEditNone 합니다.** 전달 하는 경우는 *FieldList* 및 *값* 인수, 게시 데이터베이스에 새 레코드 즉시 ADO (없음 **업데이트** 메서드), **EditMode**  속성 값이 변경 되지 않습니다 (**adEditNone**).  
  
 일괄 업데이트 모드에서 호출 하는 **AddNew** 인수 없이 메서드는 **EditMode** 속성을 **adEditAdd**합니다. 공급자에는 필드 값 변경 내용을 로컬로 캐시합니다. 호출의 **업데이트** 현재 새 레코드를 추가 하는 메서드 **레코드 집합** 다시 설정 하 고는 **EditMode** 속성을 **adEditNone**, 하지만 공급자가 기본 데이터베이스에 변경 내용을 게시 하지 않는 호출 하기 전에 **UpdateBatch** 메서드. 전달 하는 경우는 *FieldList* 및 *값* 인수, ADO는 캐시에 저장 하기 위해 공급자에 새 레코드를 보냅니다;를 호출 해야는 **UpdateBatch** 새 게시 하는 메서드 내부 데이터베이스에 기록 합니다. 에 대 한 자세한 내용은 **업데이트** 및 **UpdateBatch**, 참조 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.
