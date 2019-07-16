---
title: 추적 옵션 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13e8caf9f3a9643f8063d6227258245a603f1665
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901631"
---
# <a name="setting-tracing-options"></a>추적 옵션 설정
합니다 **추적** 탭의 **ODBC 데이터 원본 관리자** 대화 상자를 사용 하면 odbc 함수를 추적 하는 방법을 구성할 수 있습니다.  
  
## <a name="how-tracing-works"></a>추적의 작동 원리  
 추적을 시작 하는 경우는 **추적** 드라이버 관리자 탭 이후에 응용 프로그램을 실행 모두에 대 한 모든 ODBC 함수 호출을 기록 합니다. 추적 시작 되기 전에 실행 중인 응용 프로그램에서 ODBC 함수 호출 기록 되지 않습니다. ODBC 함수 호출 수를 지정 하는 로그 파일에 기록 됩니다.  
  
 클릭 한 후에 추적이 중지 되 **추적 중지**합니다. 추적에 있는 동안 로그 파일을 계속 증가 하 고이 영향을 준다는 모든 ODBC 응용 프로그램의 성능을 해야 합니다.  
  
 추적에 대 한 자세한 내용은 참조 하세요. [추적](../../odbc/reference/develop-app/tracing.md)합니다.  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 추적에서 변경 내용  
 MDAC 2.7 SP2 이전 버전 추적 캡처 id에서 실행 되는 모든 ODBC 응용 프로그램에 대 한 노출 된 정보는 전체 컴퓨터 별로 되려면 ODBC 추적만 허용 되었습니다. 이 프로세스를 만들거나 다른 로컬 사용자 계정 및 Local Service 및 Network Service와 같은 기본 제공 보안 주체를 대신 하 여 실행에 대 한 발생할 수 있는 ODBC 관련 활동에 대 한 추적을 포함 합니다.  
  
 기본적으로 ODBC 이제 사용자별 모드 사용을 추적 합니다. 그러나 로컬 관리자 인 경우 여전히 추적을 설정할 수 있습니다 시스템 수준의 ODBC 데이터 원본 관리자를 사용 하 여 합니다.  
  
 ODBC 추적 모드를 구성 합니다.  
  
1.  필요한 경우 로컬 관리자 ' 그룹의 멤버 자격 증명이 있는 계정을 사용 하 여 로그온 합니다.  
  
2.  관리 도구에서 ODBC 데이터 원본 관리자를 엽니다.  
  
3.  클릭 합니다 **추적** 탭 합니다.  
  
4.  사용 하 여 추적 모드를 구성 합니다 **모든 사용자 id에 대 한 시스템 수준의 추적** 확인란:  
  
5.  시스템 수준의 추적을 사용 하려면 확인란을 선택 합니다.  
  
6.  사용자별 추적으로 돌아가려면 확인란의 선택을 취소 합니다.  
  
7.  **적용**을 클릭합니다.  
  
> [!NOTE]  
>  이미 추적 모드에서를 시작한 경우 추적을 중지 하 고 성공적으로 변경 하는 모드에 대 한 다른 모드로 전환 해야 합니다.  
  
> [!IMPORTANT]  
>  시스템 수준의 추적; 필요한 경우에 활성화 해야 왼쪽이 고, 그렇지 해제 합니다.  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio 분석기 추적  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer에 대 한 지원 (Visual Studio Analyzer 이전 버전의 Visual Studio에만 포함 되었습니다.) Windows 8부터 제거 되었습니다. 문제 해결 메커니즘 대신 BID 추적을 사용 합니다.  
  
 Visual Studio® 분석기 추적 성능과 ODBC 계층에 대 한 디버깅 정보를 제공합니다. ODBC 구성 요소에 소요 된 시간에 관한 최대한 그림을 정확한 것으로 표시 하는 최상위 인터페이스에서 나가는 모든 이벤트 발생 합니다. Visual Studio 분석기 추적 모든 이벤트 소스를 원본으로 설정 하면 등록 해야 합니다. 이러한 종류의 추적에 대 한 자세한 내용은 Visual Studio 설명서를 참조 하세요.
