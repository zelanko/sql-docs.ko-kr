---
title: 추적 DLL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7a99f6c2960600d62a789471f68c1f5da89ae8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63148862"
---
# <a name="trace-dll"></a>추적 DLL
추적을 수행 하는 DLL ODBC 핵심 구성 요소 중 하나입니다. DLL은 현재 Windows SDK의 ODBC 구성 요소에 있는 샘플 DLL로 제공 되 고 추적에는 Microsoft Data Access Components (MDAC) SDK 이전 포함 되어 있습니다. 따라서 레지스트리 항목, 인터페이스 및 추적 DLL에 대 한 샘플 코드는 사용할 수 있습니다. 이 DLL은 DLL ODBC 사용자 또는 제 3 자 공급 업체에서 생성 된 추적으로 바꿀 수 있습니다. 사용자 지정 추적 DLL에는 원래 샘플 추적 DLL 다른 이름이 지정 되어야 합니다. 추적 Dll은 시스템 디렉터리에 설치 해야 하거나 로드 되지 것입니다. 연결 문자열을 전달 되지 않습니다 추적 DLL에 드라이버 관리자가 있습니다.  
  
 추적 DLL 입력된 인수, 출력 인수, 지연 된 인수, 반환 코드 및 Sqlstate를 추적합니다. 드라이버 관리자 추적 DLL 두 지점에서 호출 추적을 사용 하는 경우: 인수 유효성 검사) (이전 함수 시작 시 한 번 그리고 다시 함수가 반환 되기 전에 합니다.  
  
 응용 프로그램 함수를 호출할 때 드라이버 관리자 추적 드라이버에서 함수를 호출 하거나 호출 자체를 처리 하기 전에 DLL에에서는 추적 함수를 호출 합니다. 에 해당 추적 함수는 각 ODBC 함수 (접두사로 *추적*) 이름 제외 하 고 ODBC 함수는 동일 합니다. 추적 함수를 호출 하면 추적 DLL 입력된 인수를 캡처하고 반환 코드를 반환 합니다. 추적 DLL 드라이버 관리자는 인수의 유효성을 검사 하기 전에 호출 하기 때문에 상태 전환 오류와 잘못 된 인수가 기록 되므로 잘못 된 함수 호출 추적 됩니다.  
  
 드라이버 관리자 추적 DLL에서에서 추적 함수를 호출한 후 드라이버에서 ODBC 함수를 호출 합니다. 그런 다음 호출 **TraceReturn** DLL 추적에서 합니다. 이 함수는 두 개의 인수: 추적 함수에 대 한 추적 DLL에 의해 반환 되는 값 및 ODBC 함수에 대 한 드라이버 관리자를 드라이버에 의해 반환 되는 반환 코드 (또는 함수를 처리 하는 경우 자체 드라이버 관리자에 의해 반환 된 값). 함수는 캡처된 입력된 인수 값을 조작 추적 함수에 대해 반환 되는 값을 사용 합니다. 로그 파일에 ODBC 함수에 대 한 반환 코드를 작성 (또는 사용 되 면이 동적으로 표시). 출력 인수 포인터를 역참조 하 고 출력 인수 값을 기록 합니다.
