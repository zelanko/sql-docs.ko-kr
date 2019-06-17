---
title: 매개 변수 바인딩 오프셋 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1fd069336a52b0a27ae927880f749c02d2c1d43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62998928"
---
# <a name="parameter-binding-offsets"></a>매개 변수 바인딩 오프셋
응용 프로그램에서 오프셋은 바인딩된 매개 변수 버퍼 주소 및 해당 길이/표시기를 추가 지정할 수 있습니다 때 버퍼 주소 **SQLExecDirect** 또는 **SQLExecute** 라고 합니다. 이러한 추가 하면 이러한 작업에 사용 되는 주소를 결정 합니다.  
  
 호출 하지 않고 바인딩을 변경 하려면 응용 프로그램을 허용 하는 바인딩 오프셋 **SQLBindParameter** 이전에 바인딩된 매개 변수입니다. 에 대 한 호출 **SQLBindParameter** 매개 변수를 바인딩할 버퍼 주소 및 길이/표시기 포인터를 변경 합니다. 기존 바인딩된 매개 변수 버퍼 주소 및 길이/표시기 버퍼 주소 오프셋을 간단히 추가 다른 한편으로 오프셋을 사용 하 여 다시 바인딩. 오프셋을 사용 하는 경우 바인딩에 응용 프로그램 버퍼를 레이아웃 하는 방법의 "템플릿" 하 고 응용 프로그램 메모리의 다른 영역에 오프셋을 변경 하 여에 "템플릿"이를 이동할 수 있습니다. 새 오프셋을 언제 든 지 지정할 수 있으며은 항상 원래 바인딩된 값에 추가 합니다.  
  
 바인딩 오프셋을 지정 하려면 응용 프로그램을 SQLINTEGER 버퍼의 주소에 SQL_ATTR_PARAM_BIND_OFFSET_PTR 문 특성을 설정 합니다. 응용 프로그램 바인딩을 사용 하는 함수를 호출 하기 전에 배치 오프셋이이 버퍼의 바이트에서 매개 변수 버퍼 주소 아니고 길이/표시기 버퍼 주소는 0 이며 SQL 문에 바인딩된 매개 변수는 하기만 합니다. 주소와 오프셋의 합계에는 유효한 주소 여야 합니다. (즉, 중 하나 또는 모두 오프셋 및 오프셋 추가 되는 주소 수 있는 유효한 합계는 유효한 주소입니다.)  
  
> [!NOTE]  
>  바인딩 오프셋 ODBC 2에서 지원 되지 않습니다. *x* 드라이버입니다.
