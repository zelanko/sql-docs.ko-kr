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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21bee5d903459423a134389e62db844f5f63c9c1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307202"
---
# <a name="setting-tracing-options"></a>추적 옵션 설정
**Odbc 데이터 원본 관리자** 대화 상자의 **추적** 탭에서는 odbc 함수 호출을 추적 하는 방법을 구성할 수 있습니다.  
  
## <a name="how-tracing-works"></a>추적 작동 방법  
 **추적** 탭에서 추적을 시작 하면 드라이버 관리자는 모든 후속 실행 응용 프로그램에 대 한 모든 ODBC 함수 호출을 기록 합니다. 추적을 시작 하기 전에 실행 중인 응용 프로그램의 ODBC 함수 호출은 로깅되지 않습니다. ODBC 함수 호출은 사용자가 지정 하는 로그 파일에 기록 됩니다.  
  
 추적 **중지**를 클릭 한 후에만 추적을 중지 합니다. 추적이 설정 되어 있는 동안 로그 파일은 계속 증가 하며,이는 모든 ODBC 응용 프로그램의 성능에 영향을 줍니다.  
  
 추적에 대 한 자세한 내용은 [추적](../../odbc/reference/develop-app/tracing.md)을 참조 하세요.  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 추적의 변경 내용  
 MDAC 2.7 SP2 이전 버전에서는 추적을 통해 모든 id에서 실행 되는 모든 ODBC 응용 프로그램에 대 한 세부 정보를 표시 하는 컴퓨터 전체에만 ODBC 추적이 발생 했습니다. 여기에는 다른 로컬 사용자 계정을 대신 하 여 만들어지거나 실행 되는 프로세스에 대해 발생할 수 있는 ODBC 관련 작업 및 로컬 서비스 및 네트워크 서비스와 같은 기본 제공 보안 주체에 대 한 추적이 포함 되어 있습니다.  
  
 기본적으로 ODBC 추적은 이제 사용자별 모드를 사용 합니다. 그러나 로컬 관리자 인 경우에도 ODBC 데이터 원본 관리자를 사용 하 여 컴퓨터 전체 추적을 사용 하도록 설정할 수 있습니다.  
  
 ODBC 추적 모드를 구성 하려면:  
  
1.  필요한 경우 로컬 관리자 그룹의 구성원 인 계정을 사용 하 여 로그온 합니다.  
  
2.  관리 도구에서 ODBC 데이터 원본 관리자를 엽니다.  
  
3.  **추적** 탭을 클릭 합니다.  
  
4.  **모든 사용자 id에 대 한 시스템 수준 추적** 을 사용 하 여 추적 모드 구성 확인란:  
  
5.  컴퓨터 전체 추적을 사용 하도록 설정 하려면 확인란을 선택 합니다.  
  
6.  사용자별 추적으로 돌아가려면 확인란의 선택을 취소 합니다.  
  
7.  **적용**을 클릭합니다.  
  
> [!NOTE]  
>  한 모드에서 추적을 이미 시작한 경우에는 추적을 중지 하 고 모드를 변경 하기 위해 다른 모드로 전환 해야 합니다.  
  
> [!IMPORTANT]  
>  필요한 경우에만 컴퓨터 전체 추적을 사용 하도록 설정 해야 합니다. 그렇지 않은 경우에는 해제 해야 합니다.  
  
## <a name="visual-studio-analyzer-tracing"></a>Visual Studio 분석기 추적  
  
> [!IMPORTANT]  
>  Visual Studio 분석기에 대 한 지원은 Windows 8부터 제거 되었습니다 (Visual Studio 분석기 이전 버전의 Visual Studio에만 포함 됨). 다른 문제 해결 메커니즘을 사용 하려면 입찰 추적을 사용 합니다.  
  
 Visual Studio® Analyzer 추적은 ODBC 계층에 대 한 성능 및 디버깅 정보를 제공 합니다. 모든 나가는 이벤트는 최상위 인터페이스에서 발생 하므로 ODBC 구성 요소에 소요 된 시간과 관련 하 여 가능한 한 그림을 정확 하 게 제공 합니다. Visual Studio 분석기 추적에는 원본이 설정 될 때 등록할 이벤트 원본이 필요 합니다. 이러한 종류의 추적에 대 한 자세한 내용은 Visual Studio 설명서를 참조 하세요.
