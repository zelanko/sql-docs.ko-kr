---
title: 오류 예측 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d92d96e3b8cdfea5cacea35d852e8859de65dbd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925981"
---
# <a name="anticipating-errors"></a>오류 예측
오류 방지는 최소한 오류 처리 만큼 중요 합니다. 이 마지막 섹션에는 오류 발생 가능성을 줄일 수 있도록 응용 프로그램에서 수행할 수 있는 간단한 주의 사항 목록이 포함 되어 있습니다.  
  
 해당 개체를 사용 하 여 작업을 수행 하기 전에 **상태** 속성의 값을 확인 하 여 개체의 상태를 확인 합니다. 예를 들어 응용 프로그램에서 전역 **연결**을 사용 하는 경우 **open** 메서드를 호출 하기 전에 해당 **State** 속성을 확인 하 여 이미 열려 있는지 확인 합니다.  
  
-   사용자의 데이터를 허용 하는 모든 프로그램은 데이터를 데이터 저장소에 보내기 전에 유효성을 검사 하는 코드를 포함 해야 합니다. 데이터 저장소, 공급자, ADO 또는 프로그래밍 언어를 사용 하 여 문제를 알릴 수 없습니다. 사용자가 입력 한 모든 바이트를 확인 하 여 해당 필드에 대 한 데이터가 올바른 형식이 고 필수 필드가 비어 있지 않은지 확인 해야 합니다.  
  
 데이터를 데이터 저장소에 쓰기 전에 데이터를 확인 하십시오. 이 작업을 수행 하는 가장 쉬운 방법은 **WillMove** 이벤트 또는 **WillUpdateRecordset** 이벤트를 처리 하는 것입니다. ADO 이벤트를 처리 하는 방법에 대 한 자세한 설명은 [Ado 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)를 참조 하세요.  
  
 레코드 포인터를 이동 하기 **전에 레코드 집합 개체가 레코드** **집합** 의 경계를 넘지 않는지 확인 합니다. **EOF** 가 true 일 때 **MoveNext** 를 시도 하거나 **BOF** 가 true 일 때 **MovePrev** 오류가 발생 하면 오류가 발생 합니다. **EOF** 와 **BOF** 가 모두 True 인 경우 **Move** 메서드를 수행 하면 오류가 생성 됩니다.  
  
 빈 **레코드 집합**에서 **Seek** 및 **Find** 와 같은 작업을 수행 하려고 하는 경우에도 오류가 발생 합니다.
