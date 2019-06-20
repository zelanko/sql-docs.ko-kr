---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b251da97fe14abb8b10abe974c40b9adf0b37898
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699889"
---
# <a name="updating-and-persisting-data"></a>데이터 업데이트 및 유지
데이터 원본에서 데이터를 이동 하려면 ADO를 사용 하는 방법, 데이터를 이동 하는 방법 및 데이터를 편집 하는 방법에도 이전 장에서 살펴보았습니다. 물론, 응용 프로그램의 목적은 사용자가 데이터를 변경할 수 있도록 하는 경우 해당 변경 내용을 저장 하는 방법을 이해 해야 합니다. 하거나 유지할 수 있습니다 합니다 **레코드 집합** 사용 하 여 파일 변경 합니다 **저장** 하거나 메서드를 사용 하 여 저장소에 대 한 데이터 원본에 변경 내용을 다시 보낼 수는 **업데이트** 또는  **UpdateBatch** 메서드.  
  
 이전 장에서 여러 행의 데이터를 변경 합니다 **레코드 집합**합니다. ADO와 관련 된 추가, 삭제 및 데이터의 행 수정 하는 두 가지 기본 개념을 지원 합니다.  
  
 첫 번째 개념은 변경 내용을 즉시 하려고 하지는 **Recordset**대신 내부에 적용 됩니다 *복사 버퍼*합니다. 변경 하지 않으려면 복사 버퍼에서 수정 내용이 삭제 됩니다. 복사 버퍼에서 변경 내용을 적용할 변경 내용을 유지 하려는 경우는 **레코드 집합**합니다.  
  
 두 번째 개념은 작업 행에 대해 완료를 선언 하는 즉시 변경 내용을 데이터 원본에 전파 하거나 됩니다 (즉, *즉시* 모드), 행 집합의 모든 변경 집합에 대 한 작업을 선언할 때까지 수집 된 또는 전체 (즉, *일괄 처리* 모드). 합니다 **LockType** 속성 원본으로 사용 하는 데이터 원본 변경 시기를 결정 합니다. **adLockOptimistic** 나 **adLockPessimistic** 직접 실행 모드를 지정 하는 동안 **adLockBatchOptimistic** 일괄 처리 모드를 지정 합니다. 합니다 **CursorLocation** 속성이 영향을 줄 수 있는 **LockType** 설정을 사용할 수 있습니다. 예를 들어 합니다 **adLockPessimistic** 경우 설정은 지원 되지 않습니다는 **CursorLocation** 속성이로 설정 되어 **adUseClient**합니다.  
  
 직접 실행 모드에서는 각 호출을 **업데이트** 메서드는 데이터 원본에 변경 내용을 전파 합니다. 일괄 처리 모드에서는 각 호출 **업데이트** 만 복사 버퍼에서 변경 내용을 저장 하는 현재 행 위치 또는 합니다 **UpdateBatch** 메서드는 데이터 원본에 변경 내용을 전파 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 업데이트](../../../ado/guide/data/updating-data.md)  
  
-   [데이터 유지](../../../ado/guide/data/persisting-data.md)
