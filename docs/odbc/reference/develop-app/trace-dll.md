---
title: 트레이스 DLL | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298073"
---
# <a name="trace-dll"></a>추적 DLL
추적을 수행하는 DLL은 ODBC 핵심 구성 요소 중 하나입니다. 추적 DLL은 현재 Windows SDK의 ODBC 구성 요소에서 샘플 DLL로 제공되며 이전에는 Microsoft 데이터 액세스 구성 요소(MDAC) SDK가 포함되었습니다. 따라서 추적 DLL에 대 한 레지스트리 입력, 인터페이스 및 샘플 코드를 사용할 수 있습니다. 이 DLL은 ODBC 사용자 또는 타사 공급업체에서 생성한 추적 DLL로 대체할 수 있습니다. 사용자 지정 추적 DLL은 원래 샘플 추적 DLL과 다른 이름을 지정해야 합니다. 추적 DLL은 시스템 디렉터리에 설치해야 하거나 로드에 실패합니다. 연결 문자열은 드라이버 관리자가 추적 DLL로 전달되지 않습니다.  
  
 추적 DLL은 입력 인수, 출력 인수, 지연된 인수, 반환 코드 및 SQLSTATEs를 추적합니다. 추적을 사용하도록 설정하면 드라이버 관리자는 함수 입력 시(인수 유효성 검사 전)와 함수가 반환되기 직전에 다시 두 지점에서 추적 DLL을 호출합니다.  
  
 응용 프로그램이 함수를 호출할 때 드라이버 관리자는 드라이버의 함수를 호출하거나 호출 자체를 처리하기 전에 추적 DLL에서 추적 함수를 호출합니다. 각 ODBC 함수에는 이름을 제외한 ODBC 함수와 동일한 해당 추적 *함수(Trace*접두사)가 있습니다. 추적 함수가 호출되면 trace DLL은 입력 인수를 캡처하고 반환 코드를 반환합니다. 드라이버 관리자가 인수를 유효성검사하기 전에 추적 DLL이 호출되므로 잘못된 함수 호출이 추적되므로 상태 전환 오류와 잘못된 인수가 기록됩니다.  
  
 추적 DLL에서 추적 함수를 호출한 후 드라이버 관리자는 드라이버에서 ODBC 함수를 호출합니다. 그런 다음 추적 DLL에서 **TraceReturn을** 호출합니다. 이 함수는 추적 함수에 대한 추적 DLL에서 반환되는 값과 ODBC 함수에 대해 드라이버 관리자에 반환된 반환 코드(또는 함수를 처리한 경우 드라이버 관리자 자체에서 반환된 값)의 두 가지 인수를 사용합니다. 함수는 추적 함수에 대해 반환된 값을 사용하여 캡처된 입력 인수 값을 조작합니다. ODBC 함수에 대해 반환된 코드를 로그 파일에 기록합니다(또는 활성화된 경우 동적으로 표시). 출력 인수 포인터를 참조하고 출력 인수 값을 기록합니다.
