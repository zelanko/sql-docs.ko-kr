---
title: ODBC가 응답입니까? | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e325793a7b703c445be836f6f427645acda3370
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138845"
---
# <a name="is-odbc-the-answer"></a>ODBC가 응답입니까?
상호 운용성에 대 한 문제를 살펴보기 전에 다음과 같은 질문을 고려 합니다. 응용 프로그램 사용 해야 ODBC 전혀? ODBC에 대 한 지침에는 이상한 질문 울 수 있지만 이지만, 사실 합법적인 합니다. ODBC Api를 기본 데이터베이스를 완전히 대체 하도록 설계 되지 않았습니다도 모든 상황에서 데이터베이스에 액세스할 수 있도록 설계 되었습니다. 데이터베이스에 공통 인터페이스를 제공 하도록 설계 되었습니다 하 고 응용 프로그램 프로그래머는 알아보기 및 여러 데이터베이스에 대 한 링크를 유지 관리할 필요가 없는 하려던 합니다.  
  
 사용자 지정 응용 프로그램은 네이티브 데이터베이스 Api의 주요 후보입니다. 주요 이유는 사용자 지정 응용 프로그램 종종 단일 DBMS를 사용 하 여 작동 및 상호 운용할 수를 지정할 필요가 없는 경우 네이티브 데이터베이스 Api는 특정 DBMS의 기능을 노출 하는 ODBC 보다 더 효율적으로 수행할 수 있습니다 및 ODBC에 의해 노출 되지 않는 기능을 노출할 수 있습니다. 또한 없기 때문에 사용자 지정 응용 프로그램의 개발자가 일반적으로 해당 DBMS에 대 한 네이티브 데이터베이스 API에 익숙한 거의 이유가 ODBC에 알아봅니다. 그러나 일부 Dbms에 대 한 ODBC는 네이티브 데이터베이스 API 흥미롭습니다.  
  
 따라서 응용 프로그램을 ODBC에 대 한 후보? 좋은 후보는 둘 이상의 DBMS를 사용 하는 응용 프로그램. 제네릭 및 세로 거의 모든 응용 프로그램이 포함 됩니다. 또한 여러 사용자 지정 응용 프로그램을 포함합니다. 예를 들어, 여러 다른 Dbms를 사용 하는 사용자 지정 응용 프로그램은 훨씬 더 쉽고 더 깔끔하게 보다 여러 네이티브 Api 사용 하 여 ODBC를 사용 하 여 작성 합니다. 및 ODBC를 사용 하 여 작성 하는 사용자 지정 응용 프로그램은 훨씬 쉽게 회사 하나 DBMS에서 다른 위치로 이동 하거나 다른 Dbms에 대해 동일한 응용 프로그램 배포를 마이그레이션할 수 있습니다.
