---
title: "추적 옵션 설정 | Microsoft Docs"
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
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b11d6337c2e0ca2853838d964842be536454c5f4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setting-tracing-options"></a>추적 옵션 설정
**추적** 탭은 **ODBC 데이터 원본 관리자** 대화 상자를 사용 하는 ODBC 함수 호출을 추적 하는 방법을 구성할 수 있습니다.  
  
## <a name="how-tracing-works"></a>추적의 작동 원리  
 추적을 시작 하는 경우는 **추적** 드라이버 관리자 탭 이후에 응용 프로그램을 실행 모두에 대 한 모든 ODBC 호출을 기록 합니다. 추적을 시작 하기 전에 실행 중인 응용 프로그램에서 ODBC 함수 호출 기록 되지 않습니다. ODBC 함수 호출이 지정 하는 로그 파일에 기록 됩니다.  
  
 추적은 중지를 클릭 한 후에 **추적 중지**합니다. 추적 하는 반면, 로그 파일 계속 증가 하 고 모든 ODBC 응용 프로그램의 성능을 미치면 기억 합니다.  
  
 추적에 대 한 자세한 내용은 참조 [추적](../../odbc/reference/develop-app/tracing.md)합니다.  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 추적의 변경 내용  
 MDAC 2.7 SP2 이전 버전 ODBC 추적이 되었습니다 추적은 캡처합니다 모든 id에서 실행 중인 모든 ODBC 응용 프로그램에 대 한 노출 된 세부 정보는 시스템 수준의 별로 적용 되려면만 허용 됩니다. 이 프로세스를 만들거나 다른 로컬 사용자 계정 및 로컬 서비스 및 네트워크 서비스와 같은 기본 제공 보안 주체를 대신 하 여 실행에 대 한 발생할 수 있는 ODBC 관련 활동에 대 한 추적을 포함 합니다.  
  
 기본적으로 ODBC 이제 사용자 단위 모드 사용을 추적 합니다. 그러나 로컬 관리자 인 경우 여전히 추적을 설정할 수 있습니다 시스템 수준의 ODBC 데이터 원본 관리자를 사용 하 여 합니다.  
  
 구성 하려면 ODBC 추적 모드:  
  
1.  필요한 경우 로컬 관리자 그룹의 구성원 인 계정을 사용 하 여 로그온 합니다.  
  
2.  관리 도구에서 ODBC 데이터 원본 관리자를 엽니다.  
  
3.  클릭는 **추적** 탭 합니다.  
  
4.  사용 하 여 추적 모드 구성의 **모든 사용자 id에 대 한 시스템 수준의 추적** 확인란:  
  
5.  시스템 수준의 추적을 사용 하려면 확인란을 선택 합니다.  
  
6.  사용자 추적 돌아가려면 확인란의 선택을 취소 합니다.  
  
7.  **적용**을 클릭합니다.  
  
> [!NOTE]  
>  하나의 모드로 이미 추적을 시작 하는 경우 추적을 중지 하 고 모드를 성공적으로 변경할 수에 대 한 다른 모드로 전환 해야 합니다.  
  
> [!IMPORTANT]  
>  시스템 수준의 추적; 필요한 경우에 설정 해야 왼쪽 그렇지 않은 경우 해제 합니다.  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio Analyzer 추적  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer에 대 한 지원 (Visual Studio Analyzer 이전 버전의 Visual Studio에만 포함 되었습니다.) Windows 8 부터는 제거 되었습니다. 다른 방법은 문제 해결 메커니즘 BID 추적을 사용 합니다.  
  
 Visual Studio® 분석기 추적 성능 및 ODBC 계층에 대 한 디버깅 정보를 제공합니다. ODBC 구성 요소에 소요 된 시간에 대 한 가능한 그림을 정확한 것으로 표시 하려면 최상위 인터페이스에서 나가는 모든 이벤트 발생 합니다. Visual Studio Analyzer 추적 소스를 설정할 때 등록 하는 이벤트 소스가 필요 합니다. 이러한 종류의 추적에 대 한 자세한 내용은 Visual Studio 설명서를 참조 합니다.

