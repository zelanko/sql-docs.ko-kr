---
title: "데이터 업데이트 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85a34b6343f5f6251ab6f43f6802acd27bee4a3c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="updating-data"></a>데이터 업데이트
Update 동작 및 기능 크게 의존 하는 모드 (잠금 유형), 커서 유형 및 커서 위치를 업데이트 합니다.  
  
 사용 하 여는 **업데이트** 의 현재 레코드에 대 한 변경 내용을 저장 하는 메서드는 **레코드 집합** 호출 이후 개체는 **AddNew** 메서드 모든 필드 값을 변경 이후 또는 기존 레코드입니다. **레코드 집합** 개체 업데이트를 지원 해야 합니다.  
  
 경우는 **레코드 집합** 를 호출 하기 전에 로컬로 하나 이상의 레코드의 여러 변경 내용을 캐시할 수 있습니다, 개체 지원 일괄 처리 업데이트는 **UpdateBatch** 메서드. 현재 레코드를 편집 하거나 호출 하는 경우 새 레코드를 추가 하는 경우는 **UpdateBatch** 메서드, ADO를 자동으로 호출 된 **업데이트** 하기 전에 현재 레코드에 보류 중인 변경 내용을 저장 하는 메서드 공급자에 게 일괄 처리 된 변경 내용을 전송 합니다.  
  
 호출한 후에 현재 레코드가 남아는 **업데이트** 또는 **UpdateBatch** 메서드.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [직접 실행 모드](../../../ado/guide/data/immediate-mode.md)  
  
-   [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)  
  
-   [트랜잭션 처리](../../../ado/guide/data/transaction-processing.md)
