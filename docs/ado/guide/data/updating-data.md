---
title: 데이터를 업데이트 하는 중 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d593bd3ad745f316b833b375ceaae8b764d21ec2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828551"
---
# <a name="updating-data"></a>데이터 업데이트
업데이트 동작 및 기능 크게 의존 하는 모드 (잠금 유형), 커서 유형 및 커서 위치를 업데이트 합니다.  
  
 사용 하 여는 **업데이트** 의 현재 레코드에 대 한 변경 내용을 저장 하는 방법을 **레코드 집합** 호출 이후 개체를 **AddNew** 메서드 또는 필드 값 변경 후 기존 레코드입니다. 합니다 **레코드 집합** 개체 업데이트를 지원 해야 합니다.  
  
 경우는 **레코드 집합** 개체가 일괄 처리 업데이트를 지원, 호출할 때까지 로컬로 여러 변경 내용을 하나 이상의 레코드를 캐시할 수 있습니다 합니다 **UpdateBatch** 메서드. 현재 레코드를 편집 하거나 호출 하는 경우 새 레코드를 추가 하는 경우는 **UpdateBatch** 메서드를 ADO를 자동으로 호출 합니다 **업데이트** 하기 전에 현재 레코드에 보류 중인 변경 내용을 저장 하는 방법 공급자에 게 일괄 처리 된 변경 내용을 전송 합니다.  
  
 현재 레코드를 호출한 후 유지 합니다 **업데이트** 하거나 **UpdateBatch** 메서드.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [직접 실행 모드](../../../ado/guide/data/immediate-mode.md)  
  
-   [일괄 처리 모드](../../../ado/guide/data/batch-mode.md)  
  
-   [트랜잭션 처리](../../../ado/guide/data/transaction-processing.md)
