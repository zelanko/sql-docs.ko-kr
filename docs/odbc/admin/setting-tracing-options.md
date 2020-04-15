---
title: 추적 옵션 설정 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307202"
---
# <a name="setting-tracing-options"></a>추적 옵션 설정
**ODBC 데이터 원본 관리자** 대화 상자의 **추적** 탭을 사용하면 ODBC 함수 호출을 추적하는 방법을 구성할 수 있습니다.  
  
## <a name="how-tracing-works"></a>추적 작동 방식  
 **추적** 탭에서 추적을 시작하면 드라이버 관리자는 이후 실행되는 모든 응용 프로그램에 대한 모든 ODBC 함수 호출을 기록합니다. 추적이 시작되기 전에 실행 중인 응용 프로그램의 ODBC 함수 호출은 기록되지 않습니다. ODBC 함수 호출은 지정한 로그 파일에 기록됩니다.  
  
 추적은 지금 추적 중지를 클릭한 후에만 **중지됩니다.** 추적이 켜지는 동안 로그 파일이 계속 증가하고 모든 ODBC 응용 프로그램의 성능에 영향을 미칩니다.  
  
 추적에 대한 자세한 내용은 [추적](../../odbc/reference/develop-app/tracing.md)을 참조하십시오.  
  
### <a name="changes-in-odbc-tracing"></a>ODBC 추적의 변화  
 MDAC 2.7 SP2 이전에는 ODBC 추적이 시스템 전체에서만 수행되도록 허용되었으며, 이 경우 추적은 모든 ID에서 실행되는 모든 ODBC 응용 프로그램에 대한 노출된 세부 정보를 캡처합니다. 여기에는 다른 로컬 사용자 계정 및 로컬 서비스 및 네트워크 서비스와 같은 기본 제공 보안 주체를 대신하여 만들거나 실행하는 프로세스에 대해 발생할 수 있는 ODBC 관련 활동에 대한 추적이 포함됩니다.  
  
 기본적으로 ODBC 추적은 이제 사용자당 모드를 사용합니다. 그러나 로컬 관리자인 경우 ODBC 데이터 원본 관리자를 사용하여 컴퓨터 전체 추적을 활성화할 수 있습니다.  
  
 ODBC 추적 모드를 구성하려면 다음을 수행하십시오.  
  
1.  필요한 경우 로컬 관리자 그룹에 구성원이 있는 계정을 사용하여 로그온합니다.  
  
2.  관리 도구에서 ODBC 데이터 원본 관리자를 엽니다.  
  
3.  **추적** 탭을 클릭합니다.  
  
4.  모든 사용자 ID 확인란에 **대해 컴퓨터 전체 추적을** 사용하여 추적 모드를 구성합니다.  
  
5.  컴퓨터 전체 추적을 사용하려면 확인란을 선택합니다.  
  
6.  사용자별 추적으로 돌아가려면 확인란을 선택 취소합니다.  
  
7.  **적용**을 클릭합니다.  
  
> [!NOTE]  
>  한 모드에서 이미 추적을 시작한 경우 추적을 중지하고 모드를 성공적으로 변경하려면 다른 모드로 전환해야 합니다.  
  
> [!IMPORTANT]  
>  컴퓨터 전체 추적은 필요할 때만 활성화해야 합니다. 그렇지 않으면 꺼져 있어야 합니다.  
  
## <a name="visual-studio-analyzer-tracing"></a>비주얼 스튜디오 분석기 추적  
  
> [!IMPORTANT]  
>  비주얼 스튜디오 분석기지원은 Windows 8부터 제거되었습니다(Visual Studio 분석기는 이전 버전의 Visual Studio에만 포함되었습니다.) 대체 문제 해결 메커니즘을 보려면 BID 추적을 사용합니다.  
  
 Visual Studio® 분석기 추적은 ODBC 계층에 대한 성능 및 디버깅 정보를 제공합니다. 모든 나가는 이벤트는 ODBC 구성 요소에 소요된 시간에 대해 가능한 한 정확한 그림을 표시하기 위해 최상위 인터페이스에서 발생합니다. Visual Studio 분석기 추적에는 소스가 설정될 때 이벤트 소스를 등록해야 합니다. 이러한 종류의 추적에 대한 자세한 내용은 Visual Studio 설명서를 참조하십시오.
