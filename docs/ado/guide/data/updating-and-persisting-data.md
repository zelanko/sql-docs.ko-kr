---
description: 데이터 업데이트 및 유지
title: 데이터 업데이트 및 유지 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: rothja
ms.author: jroth
ms.openlocfilehash: 19e281e6108005279cd807e5ee76d383437b8814
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452655"
---
# <a name="updating-and-persisting-data"></a>데이터 업데이트 및 유지
위의 장에서는 ADO를 사용 하 여 데이터 원본의 데이터를 가져오는 방법, 데이터에서 이동 하는 방법 및 데이터를 편집 하는 방법에 대해 설명 했습니다. 물론 응용 프로그램의 목표가 사용자가 데이터를 변경할 수 있도록 허용 하는 경우 해당 변경 내용을 저장 하는 방법을 이해 해야 합니다. **Save** 메서드를 사용 하 여 파일에 대 한 **레코드 집합** 변경 내용을 유지 하거나 **업데이트** 또는 **UpdateBatch** 메서드를 사용 하 여 변경 내용을 저장소에 대 한 데이터 원본으로 다시 보낼 수 있습니다.  
  
 이전 단원에서는 **레코드 집합**의 여러 행에서 데이터를 변경 했습니다. ADO는 데이터 행의 추가, 삭제 및 수정과 관련 된 두 가지 기본 개념 지원 합니다.  
  
 첫 번째 개념은 변경 내용이 **레코드 집합**에 즉시 적용 되지 않는 것입니다. 대신, 내부 *복사 버퍼*에 적용 됩니다. 변경을 원하지 않는 경우에는 복사 버퍼의 수정 내용이 삭제 됩니다. 변경 내용을 유지 하도록 결정 하면 복사 버퍼의 변경 내용이 **레코드 집합**에 적용 됩니다.  
  
 두 번째 개념은 행에 대 한 작업을 선언 하는 즉시 (즉, *직접 실행* 모드) 변경 내용이 데이터 원본에 전파 되 고, 집합에 대 한 작업 (즉, *일괄 처리* 모드)을 선언할 때까지 행 집합에 대 한 모든 변경 내용이 수집 되는 것입니다. **LockType** 속성은 기본 데이터 원본에 변경 내용이 적용 되는 시기를 결정 합니다. **adlockoptimistic** 또는 **adlockoptimistic** 은 직접 실행 모드를 지정 하는 반면 **adlockbatch낙관적** 은 일괄 처리 모드를 지정 합니다. **CursorLocation** 속성은 사용할 수 있는 **LockType** 설정에 영향을 줄 수 있습니다. 예를 들어 **CursorLocation** 속성이 **adUseClient**로 설정 된 경우 **adlockpessimistic** 설정이 지원 되지 않습니다.  
  
 직접 실행 모드에서는 **Update** 메서드를 호출할 때마다 변경 내용이 데이터 소스에 전파 됩니다. 일괄 처리 모드에서는 현재 행 위치를 **업데이트** 하거나 이동 하는 각 호출이 복사 버퍼에 대 한 변경 내용을 저장 하지만, **UpdateBatch** 메서드만이 변경 내용을 데이터 원본으로 전파 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 업데이트](../../../ado/guide/data/updating-data.md)  
  
-   [데이터 유지](../../../ado/guide/data/persisting-data.md)
