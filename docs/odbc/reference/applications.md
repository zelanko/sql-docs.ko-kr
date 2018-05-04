---
title: 응용 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac9d98b3b7f6261333626d888c6a8b1d750f2d1b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="applications"></a>응용 프로그램
*응용 프로그램* 데이터에 액세스 하는 ODBC API를 호출 하는 프로그램입니다. 여러 유형의 응용 프로그램을 사용할 수 있지만 대부분이이 가이드 전체에서 예제로 사용 되는 세 범주로 분류 됩니다.  
  
-   **일반 응용 프로그램** 이 또한 라고 축소 래핑된 응용 프로그램이 나 기존의 많은 응용 프로그램이 있습니다. 일반 응용 프로그램은 다양 한 다른 Dbms와 작동 하도록 설계 되었습니다. 스프레드시트 또는 추가 분석을 위해 데이터를 가져오는 ODBC를 사용 하는 통계 패키지 및 데이터베이스에서 메일 그룹을 가져오기 위해 ODBC를 사용 하는 워드 프로세서를 예로 들 수 있습니다.  
  
     일반 응용 프로그램의 중요 한 하위 범주 PowerBuilder 또는 Microsoft® Visual Basic® 등의 응용 프로그램 개발 환경입니다. 아마도 이러한 환경을 사용 하 여 생성 하는 응용 프로그램은 단일 DBMS와만 작동, 하지만 환경 자체 여러 Dbms를 사용 해야 합니다.  
  
     어떤 일반 응용 프로그램을 모두 서로 공통 되는 Dbms 간에 매우 높습니다 상대적으로 일반적인 방식으로 ODBC를 사용 해야 할 때입니다. 상호 운용성에 대 한 자세한 내용은 참조 [운용성 수준을 선택](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)합니다.  
  
-   **수직 응용 프로그램** 세로 응용 프로그램이 단일 유형의 주문 입력 또는 제조 데이터를 추적 하는 등의 작업을 수행 하 고 응용 프로그램 개발자에 의해 제어 되는 데이터베이스 스키마와 함께 작동 합니다. 특정 고객에 대 한 응용 프로그램은 단일 DBMS와 작동합니다. 예를 들어 큰 비즈니스 Oracle과 사용할 수도 있고 소규모 기업 응용 프로그램을 사용 하 여 dBase, 사용 될 수 있습니다.  
  
     응용 프로그램이 제한 된 수의 유사한 기능을 제공 하는 Dbms에 연결 될 수 있지만 응용 프로그램이 모든 하나의 DBMS에 연결 되지 않은 방식으로 ODBC를 사용 합니다. 따라서 응용 프로그램 개발자는 DBMS에서 독립적으로 응용 프로그램을 판매할 수 있습니다. 수직 응용 프로그램은 이러한 인증서는 개발 하지만 고객이 DBMS 선택 noninteroperable 코드를 포함 하도록 수정 경우가 됩니다 때 상호 운용성입니다.  
  
-   **사용자 지정 응용 프로그램** 사용자 지정 응용 프로그램은 단일 회사에서 특정 작업을 수행 하는 데 사용 됩니다. 예를 들어 대기업에서 응용 프로그램 (각각 사용 하는 DBMS는) 여러 사업부에서 판매 데이터를 수집할 수도 있으며 단일 보고서를 만듭니다. ODBC는 일반 인터페이스가 고 프로그래머를 여러 인터페이스를 배울 필요에서 저장 있기 때문에 사용 됩니다. 이러한 응용 프로그램에서는 일반적으로 상호 운용 되지는 않습니다 하 고 특정 Dbms 및 드라이버에 기록 됩니다.  
  
 여러 가지 작업은 ODBC를 사용 하는 방법에 관계 없이 모든 응용 프로그램에 공통 됩니다. 전체적으로 볼 때, 주로 정의 ODBC 응용 프로그램의 흐름 합니다. 작업은 다음과 같습니다.  
  
-   데이터 소스를 선택 하 여에 연결 합니다.  
  
-   실행에 대 한 SQL 문을 제출합니다.  
  
-   결과 검색 합니다 (있는 경우).  
  
-   처리 오류가 발생 했습니다.  
  
-   커밋 또는 SQL 문을 포함 하는 트랜잭션을 롤백합니다.  
  
-   데이터 원본에서 연결을 끊는 중입니다.  
  
 대부분의 데이터 액세스 작업은을 완료 한 후 SQL 응용 프로그램을 ODBC를 사용 하는 주 작업 이므로 SQL 문을 제출 하 고 해당 문에 의해 생성 된 결과 (있는 경우)를 검색 합니다. 응용 프로그램을 ODBC를 사용 하는 다른 작업 및 드라이버 기능에 조정 하 고 데이터베이스 카탈로그를 찾아보는 등 합니다.
