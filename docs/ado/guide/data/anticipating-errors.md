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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925981"
---
# <a name="anticipating-errors"></a>오류 예측
오류 방지는 적어도 오류 처리 만큼 중요 합니다. 이 최종 섹션에서는 응용 프로그램 오류가 발생할 가능성이 적습니다 확인 하기 위해 취할 수 예방 조치의 짧은 목록을 포함 합니다.  
  
 값을 확인 하 여 개체의 상태를 확인 합니다 **상태** 해당 개체를 사용 하 여 작업을 수행 하기 전에 속성입니다. 예를 들어 응용 프로그램에서 전역 사용 **연결**를 확인 해당 **상태** 속성을 호출 하기 전에 열린 이미 있는지 확인 합니다 **엽니다** 메서드.  
  
-   사용자 데이터를 허용 하는 프로그램에는 데이터 저장소로 보내기 전에 해당 데이터를 유효성을 검사 하는 코드를 포함 해야 합니다. 문제에 대해 하기 위해 데이터 저장소, 공급자, ADO, 또는 프로그래밍 언어 에서도 사용할 수 없습니다. 없는지를 확인 하는 데이터 형식이 올 바르 해당 필드에 대 한 필수 필드가 비어 있지 않은 사용자가 입력 한 모든 바이트를 확인 해야 합니다.  
  
 데이터 저장소에 데이터를 작성 하기 전에 데이터를 확인 합니다. 이렇게 하는 가장 쉬운 방법은 처리 하는 것은 **WillMove** 이벤트 또는 **WillUpdateRecordset** 이벤트입니다. ADO 이벤트를 처리 하는 자세한 내용은 참조 하세요. [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)합니다.  
  
 했는지 **레코드 집합** 개체의 경계를 넘어서 되지 합니다 **레코드 집합** 레코드 포인터를 이동 하기 전에 합니다. 하려고 하면 **MoveNext** 때 **EOF** 은 True 또는 **MovePrev** 때 **BOF** 가 True 이면 오류가 발생 합니다. 중 하나를 수행 하는 경우는 **이동** 메서드 때 둘 다 **EOF** 하 고 **BOF** true, 오류가 생성 됩니다.  
  
 오류는 경우에 같은 작업을 수행 하려고 하면 **Seek** 하 고 **찾을** 빈 **레코드 집합**.
