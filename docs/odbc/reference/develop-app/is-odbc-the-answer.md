---
title: ODBC가 응답입니까? | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3716acbcc1b8ea648b5edc03e277983936da557
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288094"
---
# <a name="is-odbc-the-answer"></a>ODBC가 응답입니까?
상호 운용성의 문제를 자세히 살펴보기 전에 응용 프로그램이 ODBC를 전혀 사용해야 합니까? 이것은 ODBC에 대한 가이드에서 묻는 이상한 질문처럼 보일 수 있지만 실제로는 합법적 인 질문입니다. ODBC는 네이티브 데이터베이스 API를 완전히 대체하도록 설계되지 않았으며 모든 상황에서 데이터베이스 액세스를 제공하도록 설계되지 않았습니다. 데이터베이스에 대한 공통 인터페이스를 제공하도록 설계되었으며 응용 프로그램 프로그래머가 여러 데이터베이스에 대한 링크를 배우고 유지 관리할 필요가 없도록 하기 위한 것입니다.  
  
 사용자 지정 응용 프로그램은 네이티브 데이터베이스 API의 주요 후보입니다. 주된 이유는 사용자 지정 응용 프로그램이 단일 DBMS로 작동하는 경우가 많으며 상호 운용이 가능하지 않다는 것입니다. 네이티브 데이터베이스 API는 특정 DBMS의 기능을 노출하는 ODBC보다 더 나은 작업을 수행할 수 있으며 ODBC에 의해 노출되지 않는 기능을 노출할 수 있습니다. 또한 사용자 지정 응용 프로그램의 개발자는 일반적으로 DBMS에 대한 기본 데이터베이스 API에 익숙하기 때문에 ODBC를 배울 이유가 거의 없습니다. 그러나 일부 DBMS의 경우 ODBC가 기본 데이터베이스 API라는 점에 유의해야 합니다.  
  
 그렇다면 ODBC의 후보자는 무엇입니까? 가장 적합한 후보는 둘 이상의 DBMS에서 작동하는 응용 프로그램입니다. 여기에는 거의 모든 일반 및 수직 응용 프로그램이 포함됩니다. 또한 여러 사용자 지정 응용 프로그램이 포함되어 있습니다. 예를 들어 여러 개의 다른 DBMS를 사용하는 사용자 지정 응용 프로그램은 여러 네이티브 API를 사용하는 것보다 ODBC로 작성하는 것이 훨씬 쉽고 깔끔합니다. ODBC로 작성된 사용자 지정 응용 프로그램은 회사가 한 DBMS에서 다른 DBMS로 이동하거나 다른 DBMS에 대해 동일한 응용 프로그램을 배포할 때 마이그레이션하기가 훨씬 쉽습니다.
