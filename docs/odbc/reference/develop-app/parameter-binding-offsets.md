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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de67b230883f3cf8a582e73ce82e8c4bd7d21ad0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282498"
---
# <a name="parameter-binding-offsets"></a>매개 변수 바인딩 오프셋
응용 프로그램에서는 **Sqlexecdirect** 또는 **sqlexecute** 를 호출할 때 바인딩된 매개 변수 버퍼 주소와 해당 길이/표시기 버퍼 주소에 오프셋을 추가 하도록 지정할 수 있습니다. 이러한 추가의 결과로 이러한 작업에 사용 되는 주소가 결정 됩니다.  
  
 바인딩 오프셋을 사용 하면 이전에 바인딩된 매개 변수에 대해 **SQLBindParameter** 를 호출 하지 않고 응용 프로그램에서 바인딩을 변경할 수 있습니다. **SQLBindParameter** 를 호출 하 여 매개 변수를 다시 바인딩하는 경우 버퍼 주소와 길이/표시기 포인터가 변경 됩니다. 반면에 오프셋을 사용한 리바인딩은 기존 바인딩된 매개 변수 버퍼 주소 및 길이/표시기 버퍼 주소에 오프셋을 추가 합니다. 오프셋을 사용 하는 경우 바인딩은 응용 프로그램 버퍼가 배치 되는 방법의 "템플릿" 이며, 응용 프로그램은 오프셋을 변경 하 여이 "템플릿"을 다른 메모리 영역으로 이동할 수 있습니다. 언제 든 지 새 오프셋을 지정할 수 있으며, 항상 원래 바인딩된 값에 추가 됩니다.  
  
 바인딩 오프셋을 지정 하기 위해 응용 프로그램은 SQL_ATTR_PARAM_BIND_OFFSET_PTR statement 특성을 SQLINTEGER 버퍼의 주소로 설정 합니다. 응용 프로그램은 바인딩을 사용 하는 함수를 호출 하기 전에 매개 변수 버퍼 주소와 길이/표시 버퍼 주소가 모두 0이 아니고 바인딩된 매개 변수가 SQL 문에 있는 한이 버퍼에 오프셋 (바이트)을 배치 합니다. 주소와 오프셋의 합은 올바른 주소 여야 합니다. 즉, 오프셋이 추가 된 오프셋 및 주소 중 하나 또는 둘 모두가 유효 하지 않을 수 있습니다 (합계가 유효한 주소인 경우).  
  
> [!NOTE]  
>  바인딩 오프셋은 ODBC 2에서 지원 되지 않습니다. *x* 드라이버.
