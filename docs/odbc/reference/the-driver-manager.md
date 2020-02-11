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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039331"
---
# <a name="the-driver-manager"></a>드라이버 관리자
*드라이버 관리자* 는 응용 프로그램과 드라이버 간의 통신을 관리 하는 라이브러리입니다. 예를 들어 Microsoft® Windows® 플랫폼에서 드라이버 관리자는 Microsoft에서 작성 한 DLL (동적 연결 라이브러리) 이며 재배포 가능 MDAC 2.8 SP1 SDK의 사용자가 재배포할 수 있습니다.  
  
 드라이버 관리자는 주로 응용 프로그램 작성자에 게 편리한 기능으로 서 모든 응용 프로그램에 공통적인 여러 문제를 해결 합니다. 여기에는 데이터 원본 이름을 기반으로 로드할 드라이버를 결정 하 고, 드라이버를 로드 및 언로드하고, 드라이버에서 함수를 호출 하는 작업이 포함 됩니다.  
  
 후자가 문제가 되는 이유를 확인 하려면 응용 프로그램이 드라이버에서 직접 함수를 호출 하는 경우 어떤 일이 발생 하는지 살펴봅니다. 응용 프로그램을 특정 드라이버에 직접 연결 하지 않은 경우 해당 드라이버의 함수에 대 한 포인터 테이블을 빌드하여 포인터로 해당 함수를 호출 해야 합니다. 한 번에 두 개 이상의 드라이버에 동일한 코드를 사용 하는 경우 다른 복잡성 수준이 추가 됩니다. 응용 프로그램은 먼저 올바른 드라이버의 올바른 함수를 가리키도록 함수 포인터를 설정한 다음 해당 포인터를 통해 함수를 호출 해야 합니다.  
  
 드라이버 관리자는 각 함수를 호출 하는 단일 장소를 제공 하 여이 문제를 해결 합니다. 응용 프로그램은 드라이버 관리자에 연결 되며 드라이버가 아니라 드라이버 관리자에서 ODBC 함수를 호출 합니다. 응용 프로그램은 *연결 핸들*을 사용 하 여 대상 드라이버 및 데이터 원본을 식별 합니다. 드라이버가 로드 되 면 드라이버 관리자는 해당 드라이버의 함수에 대 한 포인터 테이블을 작성 합니다. 응용 프로그램에 의해 전달 된 연결 핸들을 사용 하 여 대상 드라이버에서 함수의 주소를 찾고 해당 함수를 주소로 호출 합니다.  
  
 대부분의 경우 드라이버 관리자는 응용 프로그램의 함수 호출을 올바른 드라이버로 전달 하기만 합니다. 그러나 일부 함수 (**Sqldatasources**, **Sqldatasources**및 **SQLGetFunctions**)도 구현 하 고 기본적인 오류 검사를 수행 합니다. 예를 들어 드라이버 관리자는 핸들이 not null 포인터이 고 해당 함수가 올바른 순서로 호출 되며 특정 함수 인수가 유효한 지를 확인 합니다. 드라이버 관리자에서 확인 한 오류에 대 한 자세한 내용은 각 함수에 대 한 참조 섹션과 [부록 B: ODBC 상태 전환 테이블](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)을 참조 하십시오.  
  
 드라이버 관리자의 최종 주 역할은 드라이버를 로드 하 고 언로드하는 것입니다. 응용 프로그램은 드라이버 관리자만 로드 하 고 언로드합니다. 특정 드라이버를 사용 하려는 경우 드라이버 관리자에서 연결 함수 (**SQLConnect**, **SQLDriverConnect**또는 **SQLBrowseConnect**)를 호출 하 고 특정 데이터 원본 또는 드라이버 (예: "Accounting" 또는 "SQL Server")의 이름을 지정 합니다. 드라이버 관리자는이 이름을 사용 하 여 드라이버의 파일 이름 (예: Sqlsrvr)에 대 한 데이터 원본 정보를 검색 합니다. 그런 다음 드라이버를 로드 하 고 (아직 로드 되지 않은 경우) 드라이버에 각 함수의 주소를 저장 하 고 드라이버에서 연결 함수를 호출 합니다. 그러면이 드라이버에서 자동으로 초기화 되 고 데이터 소스에 연결 됩니다.  
  
 응용 프로그램이 드라이버를 사용 하 여 완료 되 면 드라이버 관리자에서 **Sqldisconnect** 를 호출 합니다. 드라이버 관리자는 드라이버에서이 함수를 호출 하 여 데이터 원본과의 연결을 끊습니다. 그러나 드라이버 관리자는 응용 프로그램이 다시 연결 하는 경우 드라이버를 메모리에 보관 합니다. 응용 프로그램이 드라이버에서 사용 하는 연결을 해제 하거나 다른 드라이버에 대 한 연결을 사용 하 고 다른 연결에서 드라이버를 사용 하지 않는 경우에만 드라이버를 언로드합니다. 드라이버를 로드 하 고 언로드하는 데 드라이버 관리자의 역할에 대 한 자세한 설명은 [연결 프로세스에서 드라이버 관리자의 역할](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)을 참조 하세요.
