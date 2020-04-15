---
title: 매개변수 바인딩 오프셋 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de67b230883f3cf8a582e73ce82e8c4bd7d21ad0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282498"
---
# <a name="parameter-binding-offsets"></a>매개 변수 바인딩 오프셋
응용 프로그램은 오프셋이 바인딩된 매개 변수 버퍼 주소에 추가되도록 지정하고 **SQLExecDirect** 또는 **SQLExecute가** 호출될 때 해당 길이/표시기 버퍼 주소를 지정할 수 있습니다. 이러한 추가의 결과 이러한 작업에 사용 되는 주소를 결정 합니다.  
  
 바인딩 오프셋을 사용하면 응용 프로그램이 이전에 바인딩된 매개 변수에 대해 **SQLBindParameter를** 호출하지 않고 바인딩을 변경할 수 있습니다. 매개 변수를 다시 바인딩하는 **SQLBindParameter를** 호출하여 버퍼 주소와 길이/표시기 포인터를 변경합니다. 반면오프셋으로 다시 바인딩하면 기존 바운드 매개 변수 버퍼 주소와 길이/표시기 버퍼 주소에 오프셋이 추가됩니다. 오프셋을 사용할 때 바인딩은 응용 프로그램 버퍼가 배치되는 방식의 "템플릿"이며 응용 프로그램은 오프셋을 변경하여 이 "템플릿"을 다른 메모리 영역으로 이동할 수 있습니다. 새 오프셋은 언제든지 지정할 수 있으며 항상 원래 바인딩된 값에 추가됩니다.  
  
 바인드 오프셋을 지정하기 위해 응용 프로그램은 SQL_ATTR_PARAM_BIND_OFFSET_PTR 문 특성을 SQLINTEGER 버퍼의 주소로 설정합니다. 응용 프로그램이 바인딩을 사용하는 함수를 호출하기 전에 매개 변수 버퍼 주소나 길이/표시기 버퍼 주소가 0이고 바인딩된 매개 변수가 SQL 문에 있는 한 이 버퍼에 오프셋을 바이트로 배치합니다. 주소와 오프셋의 합계는 유효한 주소여야 합니다. 즉, 합계가 유효한 주소인 한 오프셋과 오프셋이 추가된 주소중 하나 또는 둘 다 유효하지 않을 수 있습니다.  
  
> [!NOTE]  
>  바인딩 오프셋은 ODBC 2에서 지원되지 않습니다. *x* 드라이버.
