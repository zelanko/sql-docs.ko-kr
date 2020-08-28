---
title: 직접 실행 모드 및 일괄 처리 모드에서 AddNew 사용 | Microsoft Docs
description: 직접 실행 모드와 일괄 처리 모드에서 AddNew를 사용 하는 방법을 설명 합니다.
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 689b8fbc6c8bb9446adfeb9fec98d53d59b28917
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979054"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>직접 실행 및 일괄 처리 모드에서 AddNew 사용
**AddNew** 메서드의 동작은 **레코드 집합** 개체의 업데이트 모드와 *fieldlist)* 및 *Values* 인수를 전달 하는지 여부에 따라 달라 집니다.  
  
 **업데이트** 메서드를 호출 하면 공급자가 기본 데이터 소스에 변경 내용을 쓰는 즉시 업데이트 모드에서 인수 없이 **AddNew** 메서드를 호출 하면 **EditMode** 속성이 adEditAdd로 설정 **됩니다.** 공급자는 필드 값 변경 내용을 로컬로 캐시 합니다. **Update** 메서드를 호출 하면 새 레코드가 데이터베이스에 게시 되 고 **EditMode** 속성이 adEditNone로 다시 설정 **됩니다.** *Fieldlist)* 및 *Values* 인수를 전달 하는 경우 ADO는 새 레코드를 데이터베이스에 즉시 게시 합니다 ( **업데이트** 호출이 필요 하지 않음). **EditMode** 속성 값은 변경 되지 않습니다 (**adEditNone**).  
  
 일괄 업데이트 모드에서 인수 없이 **AddNew** 메서드를 호출 하면 **EditMode** 속성이 **adEditAdd**로 설정 됩니다. 공급자는 필드 값 변경 내용을 로컬로 캐시 합니다. **Update** 메서드를 호출 하면 현재 **레코드 집합** 에 새 레코드가 추가 되 고 **EditMode** 속성이 **adEditNone**로 다시 설정 되지만, **UpdateBatch** 메서드를 호출할 때까지 공급자는 기본 데이터베이스에 변경 내용을 게시 하지 않습니다. *Fieldlist)* 및 *Values* 인수를 전달 하는 경우 ADO는 캐시에 저장 하기 위해 새 레코드를 공급자에 게 보냅니다. 새 레코드를 기본 데이터베이스에 게시 하려면 **UpdateBatch** 메서드를 호출 해야 합니다. **업데이트** 및 **UpdateBatch**에 대 한 자세한 내용은 [데이터 업데이트 및 유지](../../../ado/guide/data/updating-and-persisting-data.md)를 참조 하세요.
