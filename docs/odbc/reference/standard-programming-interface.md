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
ms.openlocfilehash: a241ea92af6c1273039cc45daab232a1fbe763a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081846"
---
# <a name="standard-programming-interface"></a>표준 프로그래밍 인터페이스
프로그래밍 인터페이스는 표준화를 위한 가장 명백한 후보가 될 수 있습니다. 실제로 ODBC를 개발 하는 경우 ANSI 및 ISO는 이미 포함 된 SQL 및 SQL 모듈에 대 한 표준을 제공 합니다. 데이터베이스 CLI에 대 한 표준이 없지만, SQL 액세스 그룹-데이터베이스 공급 업체의 업계 컨소시엄는 하나를 만들지 여부를 고려 하 고 있습니다. ODBC의 일부는 작업의 기반이 됩니다.  
  
 ODBC에 대 한 요구 사항 중 하나는 단일 응용 프로그램 이진이 여러 Dbms에서 작동 해야 하기 때문입니다. 이러한 이유로 ODBC는 포함 된 SQL 또는 모듈 언어를 사용 하지 않습니다. Embedded SQL 및 모듈 언어의 언어는 표준화 되지만 각각 DBMS 관련 precompilers에 연결 됩니다. 따라서 각 DBMS에 대해 응용 프로그램을 다시 컴파일해야 하며 결과 이진 파일은 단일 DBMS로만 작동 합니다. 이는 minicomputer 및 메인프레임 환경에서 발견 된 하위 볼륨 응용 프로그램에 허용 되지만 개인용 컴퓨터 환경에서는 허용 되지 않습니다. 첫째, 여러 버전의 대용량, 축소 된 소프트웨어를 고객에 게 제공 하는 것은 로지스틱입니다. 둘째, 개인용 컴퓨터 응용 프로그램은 종종 여러 Dbms에 동시에 액세스 해야 합니다.  
  
 반면, 각 로컬 컴퓨터에 상주 하는 라이브러리 또는 데이터베이스 드라이버를 통해 호출 수준 인터페이스를 구현할 수 있습니다. 각 DBMS에는 다른 드라이버가 필요 합니다. 최신 운영 체제는 런타임에 이러한 라이브러리 (예: Microsoft® Windows® 운영 체제의 동적 연결 라이브러리)를 로드할 수 있으므로 단일 응용 프로그램은 다시 컴파일하지 않고 다른 Dbms의 데이터에 액세스 하 여 데이터에 액세스할 수도 있습니다. 동시에 여러 데이터베이스 새 데이터베이스 드라이버를 사용할 수 있게 되 면 사용자는 데이터베이스 응용 프로그램을 수정, 다시 컴파일 또는 다시 링크 하지 않고도 컴퓨터에 설치할 수 있습니다. 또한, 호출 수준 인터페이스는 odbc를 사용 하는 것이 좋습니다. Windows-ODBC가 원래 개발 된 플랫폼이 이미 이러한 라이브러리를 광범위 하 게 사용 하 고 있습니다.
