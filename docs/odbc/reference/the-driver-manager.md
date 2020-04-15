---
title: 운전자 매니저 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 686a2b9673fb392f969a42f4cc86dd95a95668a6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286797"
---
# <a name="the-driver-manager"></a>드라이버 관리자
*드라이버 관리자는* 응용 프로그램과 드라이버 간의 통신을 관리하는 라이브러리입니다. 예를 들어 Microsoft® Windows® 플랫폼에서 드라이버 관리자는 Microsoft에서 작성한 동적 링크 라이브러리(DLL)이며 재배포 가능한 MDAC 2.8 SP1 SDK의 사용자가 재배포할 수 있습니다.  
  
 드라이버 관리자는 주로 응용 프로그램 작성기의 편의를 위해 존재하며 모든 응용 프로그램에 공통되는 여러 가지 문제를 해결합니다. 여기에는 데이터 원본 이름에 따라 로드할 드라이버를 결정하고, 드라이버를 로드 및 언로드하고, 드라이버의 함수를 호출하는 것이 포함됩니다.  
  
 후자의 문제가 왜 있는지 확인하려면 응용 프로그램이 드라이버의 함수를 직접 호출하는 경우 어떤 일이 발생하는지 고려하십시오. 응용 프로그램이 특정 드라이버에 직접 연결되지 않는 한 해당 드라이버의 함수에 대한 포인터 테이블을 빌드하고 포인터로 해당 함수를 호출해야 합니다. 한 번에 두 개 이상의 드라이버에 대해 동일한 코드를 사용하면 또 다른 수준의 복잡성이 추가됩니다. 응용 프로그램은 먼저 올바른 드라이버에서 올바른 함수를 가리키는 함수 포인터를 설정한 다음 해당 포인터를 통해 함수를 호출해야 합니다.  
  
 드라이버 관리자는 각 함수를 호출할 수 있는 단일 위치를 제공하여 이 문제를 해결합니다. 응용 프로그램은 드라이버 관리자에 연결되고 드라이버가 아닌 드라이버 관리자에서 ODBC 함수를 호출합니다. 응용 프로그램은 *연결 핸들을*사용하여 대상 드라이버 및 데이터 원본을 식별합니다. 드라이버를 로드하면 드라이버 관리자는 해당 드라이버의 함수에 대한 포인터 테이블을 작성합니다. 응용 프로그램에서 전달되는 연결 핸들을 사용하여 대상 드라이버에서 함수의 주소를 찾고 해당 함수를 주소별로 호출합니다.  
  
 대부분의 경우 드라이버 관리자는 응용 프로그램에서 올바른 드라이버로 함수 호출을 전달합니다. 그러나 일부**함수(SQLDataSource,** **SQL드라이버**및 **SQLGetFunctions)도**구현하고 기본 오류 검사를 수행합니다. 예를 들어 Driver Manager는 핸들이 null 포인터가 아니고 함수가 올바른 순서로 호출되고 특정 함수 인수가 유효한지 확인합니다. 드라이버 관리자에서 확인한 오류에 대한 전체 설명은 각 함수 및 [부록 B: ODBC 상태 전환 테이블의](../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조 섹션을 참조하십시오.  
  
 드라이버 관리자의 마지막 주요 역할은 드라이버를 로드하고 언로드하는 것입니다. 응용 프로그램은 드라이버 관리자만 로드하고 언로드합니다. 특정 드라이버를 사용하려는 경우 드라이버 관리자에서 연결**함수(SQLConnect,** **SQLDriverConnect**또는 **SQLBrowseConnect)를**호출하고 "회계" 또는 "SQL Server"와 같은 특정 데이터 원본 또는 드라이버의 이름을 지정합니다. 드라이버 관리자는 이 이름을 사용하여 Sqlsrvr.dll과 같은 드라이버의 파일 이름에 대한 데이터 원본 정보를 검색합니다. 그런 다음 드라이버를 로드하고(아직 로드되지 않은 경우) 드라이버에 각 함수의 주소를 저장하고 드라이버에 연결 함수를 호출한 다음 자체를 초기화하고 데이터 원본에 연결합니다.  
  
 응용 프로그램이 드라이버를 사용하여 완료되면 드라이버 관리자에서 **SQLDisconnect를** 호출합니다. 드라이버 관리자는 데이터 원본에서 연결이 끊어지는 드라이버에서 이 함수를 호출합니다. 그러나 드라이버 관리자는 응용 프로그램이 다시 연결되는 경우에 대비하여 드라이버를 메모리에 유지합니다. 응용 프로그램이 드라이버에서 사용하는 연결을 해제하거나 다른 드라이버에 대한 연결을 사용하는 경우에만 드라이버를 언로드하고 다른 연결은 드라이버를 사용하지 않습니다. 드라이버 로드 및 언로드에서 드라이버 관리자의 역할에 대한 전체 설명은 [연결 프로세스에서 드라이버 관리자의 역할을](../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)참조하십시오.
