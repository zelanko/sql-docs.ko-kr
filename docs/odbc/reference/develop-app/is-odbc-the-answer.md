---
title: "ODBC 대답 인지 확인 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ada446a96ecb6fd81d05380c8a29707eb41f8ee
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="is-odbc-the-answer"></a>ODBC 대답 인지 확인 합니다.
상호 운용성에 대 한 문제를 살펴보기 전에 먼저 다음과 같은 질문을 고려해: 응용 프로그램은 ODBC 전혀 사용? ODBC에 대 한 지침을 이상한 질문 것 처럼 보일 수 있지만, 실제로 합법적인 쿼리에. ODBC Api, 네이티브 데이터베이스를 완전히 바꾸기 하도록 설계 되지 않았습니다도 모든 상황에서 데이터베이스 액세스를 제공 하도록 설계 되었습니다. 데이터베이스에 공통 인터페이스를 제공 하도록 디자인 된 하 고를 확인 하 고 여러 데이터베이스에 대 한 링크를 유지 관리 하지 않아도 응용 프로그램 프로그래머를 해제 합니다.  
  
 사용자 지정 응용 프로그램은 기본 데이터베이스 Api에 가장 적합 합니다. 주요 이유는 사용자 지정 응용 프로그램 종종 단일 DBMS와 작동 상호 운용 되도록 해야 합니다. 네이티브 데이터베이스 Api의 특정 DBMS의 기능을 노출 하는 ODBC 보다 더 효율적으로 수행할 수 및 ODBC에 의해 노출 되지 않는 기능을 노출 될 수 있습니다. 또한 없기 때문에 사용자 지정 응용 프로그램 개발자가 일반적으로 DBMS에 대 한 기본 데이터베이스 API ODBC에 알아보려면이 좋습니다. 그러나 일부 Dbms ODBC는 네이티브 데이터베이스 API는 흥미로운 부분입니다.  
  
 따라서 응용 프로그램을 ODBC에 대 한 후보는? 가장 좋은 후보는 둘 이상의 DBMS와 작동 하는 응용 프로그램. 제네릭 및 세로 거의 모든 응용 프로그램이 포함 됩니다. 사용자 지정 응용 프로그램 수가 포함 됩니다. 예를 들어 여러 다른 Dbms를 사용 하는 사용자 지정 응용 프로그램은 훨씬 쉽고 여러 네이티브 Api 사용 하 여 보다 ODBC를 사용 하 여 작성 정확 합니다. 및 ODBC로 작성 된 사용자 지정 응용 프로그램은 훨씬 쉽게 회사 하나의 DBMS에서 다른 위치로 이동 또는 여러 Dbms에 대해 동일한 응용 프로그램 배포를 마이그레이션할 수 있습니다.

