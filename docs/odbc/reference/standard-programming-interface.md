---
title: 표준 프로그래밍 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c91448833c6dacecaadfa4b0c11892e1a0c5e439
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="standard-programming-interface"></a>표준 프로그래밍 인터페이스
가장 확실 한 후보 표준화에 대 한 프로그래밍 인터페이스가입니다. 사실, ODBC 개발 시 ANSI 및 ISO 이미 제공 된 표준 포함 된 SQL 및 SQL에 대 한 모듈입니다. CLI의 SQL 액세스 그룹 데이터베이스에 대 한 없는 표준 있었지만-데이터베이스 공급 업체는 업계 컨소시엄-; 만들 것인지를 고려할 되었습니다 ODBC의 일부를 나중에 작업에 대 한 기본 업체가 되었습니다.  
  
 ODBC에 대 한 요구 사항 중은 단일 응용 프로그램 이진 여러 Dbms 작업할 수 있습니다. ODBC 포함 된 SQL 또는 모듈 언어를 사용 하지 않는 이러한 이유 때문입니다. 포함 된 SQL 및 모듈 언어의 언어 표준화 되어 있지만 각 DBMS 전용 precompilers 연결 됩니다. 따라서 각 DBMS에 대 한 응용 프로그램을 컴파일해야 하 고 결과 바이너리 단일 DBMS에만 작동 합니다. 미니 컴퓨터 및 메인프레임 세계에는 저용량 응용 프로그램에 대해 허용 가능한 상태인 동안 허용 가능한에 없는 개인용 컴퓨터 세계 합니다. 첫째, 것은 고객;에 여러 버전의 대량, 축소 래핑된 소프트웨어를 제공 하도록 물류 밋 둘째, 개인용 컴퓨터 응용 프로그램 여러 Dbms를 동시에 액세스 해야 하는 경우가 많습니다.  
  
 반면에 라이브러리 또는 각 로컬 시스템에 상주 하는 데이터베이스 드라이버를 통해 호출 수준 인터페이스를 구현할 수 있습니다. 다른 드라이버는 각 DBMS 필요 합니다. 최신 운영 체제 실행 시 (예: Microsoft® Windows® 운영 체제에서 동적 연결 라이브러리) 이러한 라이브러리를 로드할 수 있습니다., 때문에 단일 응용 프로그램 데이터의 다시 컴파일하지 않고 다른 Dbms 및에서 데이터에 액세스할 수도 있습니다. 여러 동시에 데이터베이스. 사용할 수 있는 새 데이터베이스 드라이버 해지면 사용자가 설치할 수도 자신의 컴퓨터에 이러한 수정 컴파일하거나 데이터베이스 응용 프로그램을 다시 연결 하지 않고도 합니다. 또한 호출 수준 인터페이스에서 적합 한 ODBC 했으므로 Windows-ODBC 개발 원래 된 플랫폼-이미 만들어져 있으므로 이러한 라이브러리를 많이 사용 합니다.
