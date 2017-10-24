---
title: "오류 예측 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 359dc6c1bd396a0909aea36c5039a4ba5195f326
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="anticipating-errors"></a>오류 예측
오류가 발생 하지 않도록은 적어도 오류 처리 중요 합니다. 이 마지막 섹션에는 응용 프로그램 오류가 발생 하기 위해 취할 수 예방 조치의 짧은 목록을 포함 합니다.  
  
 값을 확인 하 여 개체의 상태를 확인는 **상태** 해당 개체를 사용 하는 작업을 실행 하기 전에 속성입니다. 예를 들어, 응용 프로그램 사용 전역 **연결**, 확인 해당 **상태** 속성을 호출 하기 전에 열려 이미 있는지 확인 하십시오는 **열고** 메서드.  
  
-   사용자 데이터를 허용 하는 프로그램 데이터 저장소에 보내기 전에 해당 데이터를 유효성 검사 코드를 포함 해야 합니다. 데이터 저장소, 공급자, ADO 또는 문제를 알려도 선택한 프로그래밍 언어에서 사용할 수 없습니다. 없는지를 확인 하는 데이터 형식이 올 바르 해당 필드에 대 한 필수 필드가 비어 있지 않으며 사용자가 입력 한 모든 바이트를 확인 해야 합니다.  
  
 데이터 저장소에 데이터를 작성 하려고 하기 전에 데이터를 확인 합니다. 이렇게 하는 가장 쉬운 방법은 처리 하기 위한 것은 **WillMove** 이벤트 또는 **WillUpdateRecordset** 이벤트입니다. ADO 이벤트 처리의 자세한 논의 알려면 [ADO 이벤트 처리](../../../ado/guide/data/handling-ado-events.md)합니다.  
  
 다음 사항을 확인 **레코드 집합** 개체의 경계를 넘어 않습니다는 **레코드 집합** 레코드 포인터를 이동 하기 전에. 하려고 하면 **MoveNext** 때 **EOF** 은 True 또는 **MovePrev** 때 **BOF** 가 True 이면 오류가 발생 합니다. 중 하나를 수행 하는 경우는 **이동** 메서드 때 둘 다 **EOF** 및 **BOF** true, 오류가 생성 됩니다.  
  
 또한 있으면 오류가 발생 합니다와 같은 작업을 수행 하려고 하면 **Seek** 및 **찾을** 빈 **레코드 집합**합니다.

