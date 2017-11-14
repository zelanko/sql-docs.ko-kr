---
title: "데이터 업데이트 및 지속 | Microsoft Docs"
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
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c08f7bfbb813bb3e2041f350a2e4397d9aff6ffd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updating-and-persisting-data"></a>업데이트 및 데이터 유지
데이터 원본에 가져올 데이터에 ADO를 사용 하는 방법, 데이터를 이동 하는 방법 및 데이터를 편집 하는 방법에도 이전 장에서 살펴보았습니다. 물론, 응용 프로그램의 목표는 데이터를 변경할 수 있도록 하려는 경우, 이러한 변경 내용을 저장 하는 방법을 이해 해야 합니다. 하거나 유지할 수 있습니다는 **레코드 집합** 로 사용 하 여 파일 변경는 **저장** 하거나 메서드를 사용 하 여 저장소에 대 한 데이터 소스에 변경 내용을 다시 보낼 수는 **업데이트** 또는  **UpdateBatch** 메서드.  
  
 여러 행에서 데이터 변경 이전 장에서 **레코드 집합**합니다. ADO를 추가, 삭제 및 수정할 데이터 행에 관련 된 두 가지 기본 개념을 지원 합니다.  
  
 첫 번째 개념은 변경 내용을에 바로 적용 되지 않습니다는 **레코드 집합**대신 내부 내용이 *복사 버퍼*합니다. 변경 내용을 않도록 결정 한 경우에 수정 복사 버퍼에 삭제 됩니다. 복사 버퍼에 변경 내용이에 적용 한 변경 내용을 유지 하려는 경우는 **레코드 집합**합니다.  
  
 둘째는 방식으로 작업 행에 대해 완료를 선언 하면 변경 내용이 데이터 소스에 전파 하거나 되 (즉, *즉시* 모드), 행 집합의 모든 변경 내용 집합에 대 한 작업을 선언할 때까지 수집 된 또는 완료 (즉, *일괄 처리* 모드). **LockType** 속성 기본 데이터 원본에 변경 내용이 적용 시기를 결정 합니다. **adLockOptimistic** 또는 **adLockPessimistic** 직접 실행 모드를 지정 하는 동안 **adLockBatchOptimistic** 일괄 처리 모드를 지정 합니다. **앞** 속성 영향을 줄 수 있는 **LockType** 설정을 사용할 수 있습니다. 예를 들어,는 **adLockPessimistic** 경우 설정을 지원 하지 않습니다는 **앞** 속성이 **adUseClient**합니다.  
  
 직접 실행 모드의 각 호출에서는 **업데이트** 메서드 데이터 소스에 변경 내용을 전파 합니다. 호출할 때마다 일괄 처리 모드로 **업데이트** 만 복사 버퍼에 변경 내용을 저장 하는 현재 행 위치 또는 **UpdateBatch** 메서드 데이터 소스에 변경 내용을 전파 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 업데이트](../../../ado/guide/data/updating-data.md)  
  
-   [데이터 유지](../../../ado/guide/data/persisting-data.md)

