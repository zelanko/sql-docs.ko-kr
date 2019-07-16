---
title: 드라이버 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC]
- ODBC architecture [ODBC], driver manager
- driver manager [ODBC], about driver manager
- ODBC driver manager [ODBC]
ms.assetid: 559e4de1-16c9-4998-94f5-6431122040cd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 659678451c368df0b6a213e54cf7edaedfc29bd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039331"
---
# <a name="the-driver-manager"></a>드라이버 관리자
합니다 *드라이버 관리자* 응용 프로그램 및 드라이버 간의 통신을 관리 하는 라이브러리입니다. 예를 들어, Microsoft® Windows® 플랫폼에서 드라이버 관리자는 동적 연결 라이브러리 (DLL)는 Microsoft에서 기록 되 고 사용자의 재배포 가능 패키지 MDAC 2.8 SP1 SDK가 재배포할 수 있습니다.  
  
 드라이버 관리자는 응용 프로그램 작성기에 주로 편의상 있고 다양 한 모든 응용 프로그램에 공통적으로 적용 되는 문제가 해결 되었습니다. 여기에 드라이버 로드를 데이터 원본 이름에 따라 결정, 로드 및 언로드 드라이버 및 드라이버에서 함수 호출 포함 됩니다.  
  
 이유는 후자는 문제를 확인 하려면 어떻게 될 것이 좋습니다. 응용 프로그램이 드라이버에서 직접 함수를 호출 합니다. 응용 프로그램 특정 드라이버에 직접 연결 된 경우가 아니면 해당 드라이버의 함수에 대 한 포인터의 테이블을 작성 하 여 포인터에서 이러한 함수를 호출 해야 합니다. 한 번에 둘 이상의 드라이버에 대 한 동일한 코드를 사용 하 여 다른 수준의 복잡성 추가할 수 있습니다. 응용 프로그램은 먼저 올바른 드라이버에서 올바른 함수가를 가리키도록 함수 포인터를 설정 해야를 다음 포인터를 통해 함수를 호출 합니다.  
  
 드라이버 관리자는 각 함수를 호출 하는 단일 위치를 제공 하 여이 문제를 해결 합니다. 응용 프로그램은 드라이버가 아니라 드라이버 관리자에서 드라이버 관리자 및 호출 ODBC 함수에 연결 됩니다. 사용 하 여 대상 드라이버 및 데이터 소스를 식별 하는 응용 프로그램을 *연결 핸들*합니다. 드라이버를 로드할 때 드라이버 관리자는 해당 드라이버의 함수에 대 한 포인터의 테이블을 작성 합니다. 대상 드라이버에서 함수의 주소를 찾으려면 응용 프로그램으로 전달 하 여 연결 핸들을 사용 하 고 주소로 해당 함수를 호출 합니다.  
  
 대부분의 경우 드라이버 관리자는 방금 올바른 드라이버 응용 프로그램에서 함수 호출을 전달합니다. 하지만 또한 일부 함수 구현 (**SQLDataSources**를 **SQLDrivers**, 및 **SQLGetFunctions**) 하 고 기본 오류 검사를 수행 합니다. 예를 들어 드라이버 관리자 처리 되지 않는다는 사실을 null 포인터는 함수가 올바른 순서 대로 호출 하 고 특정 함수 인수가 올바른지 확인 합니다. 드라이버 관리자에 의해 확인 오류 설명은 각 함수에 대 한 참조 섹션을 참조 하 고 [부록 b: ODBC 상태 전환 테이블](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.  
  
 드라이버 관리자의 마지막 주요 역할 로드 하 고 드라이버를 언로드하는 합니다. 응용 프로그램 로드 하 고 드라이버 관리자만을 언로드합니다. 연결 함수를 호출, 특정 드라이버를 사용 하려는 경우 (**SQLConnect**를 **SQLDriverConnect**, 또는 **SQLBrowseConnect**) 드라이버 관리자를 지정 하 고 특정 데이터 원본 또는 드라이버에서 "계정" 또는 "SQL Server."와 같은 이름 이 이름을 사용 하 여, 드라이버 관리자 Sqlsrvr.dll 같은 드라이버의 파일 이름에 대 한 데이터 원본 정보를 검색 합니다. 그런 다음 (아직 로드 되지 않은 것으로 가정) 드라이버를 로드, 드라이버에서 각 함수의 주소를 저장 하 고 그런 다음 자체적으로 초기화 하 고 데이터 원본에 연결 하는 드라이버에서 연결 함수를 호출 합니다.  
  
 응용 프로그램이 완료 되 면 호출 드라이버를 사용 하 여 **SQLDisconnect** 드라이버 관리자의 합니다. 드라이버 관리자는 데이터 원본에서 연결을 끊습니다는 드라이버에서이 함수를 호출 합니다. 그러나 드라이버 관리자 응용 프로그램에 다시 연결 하는 경우에 드라이버 메모리에 유지 합니다. 응용 프로그램 드라이버에서 사용 하는 연결을 해제 하거나 다른 드라이버의 경우 연결을 사용 하 고 드라이버를 사용 하 여 다른 연결이 없는 경우에 드라이버를 언로드합니다. 에 대 한 전체 설명은 로드 및 언로드 드라이버에서 드라이버 관리자의 역할, 참조 [연결 프로세스에서 드라이버 관리자의 역할](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)입니다.
