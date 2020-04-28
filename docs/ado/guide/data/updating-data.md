---
title: 데이터 업데이트 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bd3b72e897b8ae12441c7cf28d1995eb45318d1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923698"
---
# <a name="updating-data"></a>데이터 업데이트
업데이트 동작 및 기능은 주로 업데이트 모드 (잠금 유형), 커서 유형 및 커서 위치에 따라 달라 집니다.  
  
 **AddNew** 메서드를 호출 하거나 기존 레코드의 필드 값을 변경한 후에는 **Update** 메서드를 사용 하 여 **레코드 집합** 개체의 현재 레코드에 대 한 변경 내용을 저장할 수 있습니다. **레코드 집합** 개체는 업데이트를 지원 해야 합니다.  
  
 **레코드 집합** 개체가 일괄 처리 업데이트를 지 원하는 경우 **UpdateBatch** 메서드를 호출할 때까지 하나 이상의 레코드에 대 한 여러 변경 내용을 로컬로 캐시할 수 있습니다. 현재 레코드를 편집 하거나 **UpdateBatch** 메서드를 호출할 때 새 레코드를 추가 하는 경우, ADO는 일괄 처리 된 변경 내용을 공급자에 전송 하기 전에 **업데이트** 메서드를 자동으로 호출 하 여 현재 레코드에 대 한 보류 중인 변경 내용을 저장 합니다.  
  
 **업데이트** 또는 **UpdateBatch** 메서드를 호출한 후 현재 레코드는 현재 상태로 유지 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [직접 실행 모드](../../../ado/guide/data/immediate-mode.md)  
  
-   [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)  
  
-   [트랜잭션 처리](../../../ado/guide/data/transaction-processing.md)
