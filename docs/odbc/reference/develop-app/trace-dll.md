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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e1f9dc57415ad9865ca1b2ad02487b62a93f18f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "81298073"
---
# <a name="trace-dll"></a>추적 DLL
추적을 수행 하는 DLL은 ODBC 핵심 구성 요소 중 하나입니다. 추적 DLL은 현재 Windows SDK의 ODBC 구성 요소에서 샘플 DLL로 제공 되며 이전에는 MDAC (Microsoft Data Access Components) SDK를 포함 했습니다. 따라서 추적 DLL에 대 한 레지스트리 항목, 인터페이스 및 샘플 코드를 사용할 수 있습니다. 이 DLL은 ODBC 사용자 또는 타사 공급 업체에 의해 생성 된 추적 DLL로 대체 될 수 있습니다. 사용자 지정 추적 DLL은 원래 예제 추적 DLL과 다른 이름을 지정 해야 합니다. 추적 Dll은 system 디렉터리에 설치 해야 합니다. 그렇지 않으면 로드 되지 않습니다. 연결 문자열은 드라이버 관리자에 의해 추적 DLL에 전달 되지 않습니다.  
  
 추적 DLL은 입력 인수, 출력 인수, 지연 된 인수, 반환 코드 및 SQLSTATEs를 추적 합니다. 추적을 사용 하는 경우 드라이버 관리자는 함수 입력 (인수 유효성 검사 전) 및 함수가 반환 되기 바로 전에 다시 두 개의 지점에서 추적 DLL을 호출 합니다.  
  
 응용 프로그램에서 함수를 호출 하는 경우 드라이버 관리자는 드라이버에서 함수를 호출 하거나 호출 자체를 처리 하기 전에 추적 DLL에서 추적 함수를 호출 합니다. 각 ODBC 함수에는 이름이 제외 된 ODBC 함수와 동일한 해당 추적 함수 ( *trace*접두사가 있음)가 있습니다. 추적 함수가 호출 되 면 추적 DLL은 입력 인수를 캡처하여 반환 코드를 반환 합니다. 드라이버 관리자가 인수의 유효성을 검사 하기 전에 추적 DLL이 호출 되기 때문에 잘못 된 함수 호출을 추적 하므로 상태 전환 오류가 발생 하 고 잘못 된 인수가 기록 됩니다.  
  
 추적 DLL에서 추적 함수를 호출한 후 드라이버 관리자는 드라이버에서 ODBC 함수를 호출 합니다. 그런 다음 추적 DLL에서 **TraceReturn** 을 호출 합니다. 이 함수는 두 개의 인수, 즉 추적 DLL에서 추적 함수에 대해 반환 되는 값, ODBC 함수 (또는 함수를 처리 한 경우 드라이버 관리자 자체에서 반환 되는 값)에 대 한 드라이버 관리자에 의해 반환 되는 반환 코드를 사용 합니다. 함수는 추적 함수에 대해 반환 된 값을 사용 하 여 캡처된 입력 인수 값을 조작 합니다. ODBC 함수에 대해 반환 된 코드를 로그 파일에 기록 하거나, 사용 하도록 설정 된 경우 동적으로 표시 합니다. 출력 인수 포인터를 역참조 하 고 출력 인수 값을 기록 합니다.
