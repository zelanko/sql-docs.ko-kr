---
title: "매개 변수 바인딩 오프셋 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5b3fea1397710c5a65a03b3f829972f04cc63f5a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-binding-offsets"></a>매개 변수 바인딩 오프셋
응용 프로그램에서 오프셋 바인딩된 매개 변수 버퍼 주소 및 해당 길이/표시기 추가 되어 있는지를 지정할 수 때 버퍼 주소 **SQLExecDirect** 또는 **SQLExecute** 호출 됩니다. 추가 하는이 코드의 결과 이러한 작업에 사용 되는 주소를 결정 합니다.  
  
 바인딩 오프셋 하면 응용 프로그램 바인딩을 호출 하지 않고 변경할 **SQLBindParameter** 이전에 바인딩된 매개 변수입니다. 에 대 한 호출 **SQLBindParameter** 매개 변수를 바인딩할 버퍼 주소 및 길이/표시기 포인터를 변경 합니다. 기존 바인딩된 매개 변수 버퍼 주소 및 길이/표시기 버퍼 주소 오프셋을 단순히 추가 반면에 리바인딩, 오프셋을 사용 합니다. 오프셋을 사용 하는 바인딩이 지 응용 프로그램 버퍼 레이아웃 하는 방법의 "템플릿" 않으며 응용 프로그램 오프셋을 변경 하 여 메모리의 다른 영역 "템플릿"이 이동할 수 있습니다. 새 오프셋 언제 든 지 지정할 수 있으며은 항상 원래 바인딩된 값에 추가 합니다.  
  
 바인딩 오프셋을 지정 하려면 응용 프로그램 SQLINTEGER 버퍼의 주소를 SQL_ATTR_PARAM_BIND_OFFSET_PTR 문 특성을 설정 합니다. 응용 프로그램 바인딩을 사용 하는 함수를 호출 하기 전에 오프셋에에서 배치이 버퍼의 바이트 매개 변수 버퍼 주소 아니고 길이/표시기 버퍼 주소 0 이며 SQL 문에 바인딩된 매개 변수는 하기만 합니다. 주소와 오프셋의 합계에는 유효한 주소 여야 합니다. (이 좀 더 중 하나 또는 모두 오프셋 및 오프셋을 추가한 주소 수 있습니다 하지 유효 합계는 유효한 주소입니다.)  
  
> [!NOTE]  
>  바인딩 오프셋 ODBC 2에서 지원 되지 않습니다. *x* 드라이버입니다.

