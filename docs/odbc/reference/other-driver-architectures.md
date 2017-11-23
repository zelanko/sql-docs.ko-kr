---
title: "다른 드라이버 아키텍처 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f3fc19dd4b6553362705b7cc57c9431a29aa91ca
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="other-driver-architectures"></a>다른 드라이버 아키텍처
일부 ODBC 드라이버에는 앞에서 설명한 아키텍처 엄격 하 게 준수 하지 않는 합니다. 드라이버는 기존의 ODBC 드라이버의 이외의 상의 임무를 수행할 또는 일반적인 의미에서 드라이버가 아닌 때문일 수 있습니다.  
  
## <a name="driver-as-a-middle-component"></a>중간 구성 요소로 드라이버  
 ODBC 드라이버는 드라이버 관리자와 하나 이상의 다른 ODBC 드라이버 사이의 있을 수 있습니다. 중간에 드라이버는 여러 데이터 원본 작업의 수, ODBC 호출 (또는 적절 하 게 번역 된 호출)에 실제로 데이터 원본에 액세스 하는 다른 모듈에는 발송자 작동 합니다. 이 아키텍처에서 중간에 드라이버를 드라이버 관리자의 역할의 일부에 걸리고 있습니다.  
  
 드라이버의 이러한 종류의 또 다른 예로 차단 하 고 드라이버 관리자와 드라이버 간에 전송 되는 ODBC 함수를 복사 하는 ODBC에 대 한 spy 프로그램입니다. 이 계층 응용 프로그램 또는 드라이버를 에뮬레이트하는 데 사용할 수 있습니다. 드라이버 관리자를 레이어 것 같습니다. 드라이버; 드라이버에 레이어 드라이버 관리자 것 같습니다.  
  
## <a name="heterogeneous-join-engines"></a>형식이 다른 조인 엔진  
 일부 ODBC 드라이버는 다른 유형의 조인을 수행 하는 쿼리 엔진을 기반으로 합니다. 형식이 다른 조인 엔진의 한 아키텍처에서 (다음 그림 참조), 드라이버 응용 프로그램으로 다른 디렉터리로 드라이버 관리자의 인스턴스를 표시 하지만 드라이버는 응용 프로그램에 표시 합니다. 이 드라이버는 드라이버의 각 조인 된 데이터베이스에 대해 별도 SQL 문을 호출 하 여 응용 프로그램에서 다른 유형의 조인을 처리 합니다.  
  
 ![형식이 다른 조인 엔진의 아키텍처](../../odbc/reference/media/fig3-4.gif "fig3 4")  
  
 이 아키텍처는 다양 한 데이터베이스의 데이터에 액세스 하도록 응용 프로그램에 대 한 공용 인터페이스를 제공 합니다. 특수 열 (행 식별자)에 대 한 정보 등의 메타 데이터를 검색 하는 일반적인 방법은 사용할 수 있습니다 및 데이터 사전 정보를 검색 하는 일반 카탈로그 함수를 호출할 수 있습니다. ODBC 함수를 호출 하 여 **SQLStatistics**, 예를 들어, 통해 응용 프로그램이 두 개의 서로 다른 데이터베이스 테이블은 경우에 테이블을 조인할 수에 인덱스에 대 한 정보를 검색할 수 있습니다. 쿼리 프로세서는 데이터베이스 메타 데이터를 저장 하는 방법에 대해 걱정할 필요가 없습니다.  
  
 또한 데이터 형식에 대 한 표준 액세스를 포함 합니다. ODBC는 DBMS 관련 데이터 형식에 매핑되는 일반 SQL 데이터 형식을 정의 합니다. 응용 프로그램에서 호출할 수 **SQLGetTypeInfo** 서로 다른 데이터베이스에 데이터 형식에 대 한 정보를 검색 합니다.  
  
 다른 유형의 조인 문을 생성 하는 응용 프로그램,이 아키텍처의 쿼리 프로세서는 SQL 문을 구문 분석 하 고 조인할 각 데이터베이스에 대 한 별도 SQL 문을 생성 합니다. 각 드라이버에 대 한 메타 데이터를 사용 하 여 쿼리 프로세서가 가장 효율적인, 지능형 조인 결정할 수 있습니다. 예를 들어 문이 하나의 데이터베이스와 다른 데이터베이스에 한 테이블에 두 개의 테이블을 조인, 쿼리 프로세서 조인할 수는 두 테이블 하나의 데이터베이스에 결과를 다른 데이터베이스에서 테이블에 연결 하기 전에.  
  
## <a name="odbc-on-the-server"></a>서버에서 ODBC  
 ODBC 드라이버는 모든 클라이언트 컴퓨터에서 응용 프로그램에서 사용할 수 있도록 서버에 설치할 수 있습니다. 이 아키텍처에서 (다음 그림 참조), 각 클라이언트에 설치 된 드라이버 관리자와 단일 ODBC 드라이버 및 드라이버는 다른 관리자와 일련의 ODBC 드라이버는 서버에 설치 됩니다. 따라서 각 클라이언트 액세스를를 사용 하 고 서버에서 유지 관리 하는 드라이버의 다양 한 수 있습니다.  
  
 ![서버에서 ODBC 드라이버의 아키텍처](../../odbc/reference/media/fig3-5.gif "FIG3 5")  
  
 이 아키텍처의 장점 중 하나는 효율적으로 소프트웨어 유지 관리 및 구성 됩니다. 드라이버는 한 곳에서 업데이트 필요: 서버에 있습니다. 시스템 데이터 소스를 사용 하 여 모든 클라이언트에서 데이터 원본은 사용 하기 위해 서버에서 정의할 수 있습니다. 클라이언트에서 데이터 원본은 정의할 필요가 있습니다. 연결 풀링을 사용할 수 있는 클라이언트 데이터 원본에 연결 하는 프로세스를 간소화 하 합니다.  
  
 클라이언트에서 드라이버는 일반적으로 서버에 대 한 드라이버 관리자 호출을 전송 하는 매우 작은 드라이버. 공간이 서버에서 모든 기능을 갖춘 ODBC 드라이버 보다 훨씬 적을 수 있습니다. 이 아키텍처에서 서버에 있는 경우 추가 컴퓨팅 기능이 클라이언트 리소스를 해제할 수 있습니다. 또한 백업 서버를 설치 하 고 서버 사용을 최적화 하기 위해 부하 분산을 수행 하 여 효율성 및 전체 시스템의 보안을 향상 시킬 수 있습니다.
