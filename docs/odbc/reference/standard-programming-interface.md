---
title: 표준 프로그래밍 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e0e10a6b8c15b6522e6b34ab008295fc411fcd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232058"
---
# <a name="standard-programming-interface"></a>표준 프로그래밍 인터페이스
프로그래밍 인터페이스는 아마도 표준화에 대 한 가장 확실 한 후보입니다. 사실, ODBC 개발 중인 경우 ANSI 및 ISO 이미 제공 표준을 포함 된 SQL 및 SQL 모듈입니다. SQL 액세스 그룹-데이터베이스 공급 업체의 업계 컨소시엄-; 만들 것인지 고려 된 없는 표준 CLI 데이터베이스에 대 한 존재 하지만 ODBC의 일부를 나중에 회사의 기반이 되었습니다.  
  
 ODBC에 대 한 요구 사항 중 하나는 단일 응용 프로그램 이진 여러 Dbms를 사용 하 여 작업 해야 했습니다. ODBC 포함 된 SQL 또는 모듈 언어를 사용 하지 않는 이러한 이유 때문입니다. 포함 된 SQL 및 모듈 언어의 언어는 표준화 되지만 각 DBMS 관련 precompilers 연결 됩니다. 따라서 각 DBMS에 대 한 응용 프로그램을 컴파일해야 하 고 결과 이진 파일을 단일 DBMS 에서만 작동 합니다. 이 미니 컴퓨터 및 메인프레임 환경에 있는 볼륨이 적은 응용 프로그램에 대 한 허용 되는 동안이 허용 되지 개인용 컴퓨터 환경에서. 첫째, 여러 버전의 대규모, 압축 포장 소프트웨어; 고객에 게 전달할 공포 것은 둘째, 개인용 컴퓨터 응용 프로그램 여러 Dbms를 동시에 액세스 해야 하는 경우가 많습니다.  
  
 반면에 라이브러리 또는 각 로컬 컴퓨터에 상주 하는 데이터베이스 드라이버를 통해 호출 수준 인터페이스를 구현할 수 있습니다. 다른 드라이버는 각 DBMS 필요 합니다. 단일 응용 프로그램을 다시 컴파일하지 않고도 다양 한 Dbms의 데이터에 액세스할 수 및에서 데이터에 액세스할 수도 최신 운영 체제는 런타임 시 이러한 라이브러리 (예: Microsoft® Windows® 운영 체제에서 동적 연결 라이브러리)을 로드할 수, 때문에 여러 동시에 데이터베이스. 새 데이터베이스 드라이버를 사용할 수 있을 경우 사용자만 설치할 수 해당 컴퓨터에서 이러한 수정 컴파일하거나 데이터베이스 응용 프로그램을 다시 연결 하지 않고도. 또한 호출 수준 인터페이스를 이어서 ODBC에 대 한 좋은 후보 Windows-는 ODBC 처음 개발한-이미 만들어져 있으므로 이러한 라이브러리의 광범위 하 게 사용 되는 플랫폼입니다.
