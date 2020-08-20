---
description: ODBC가 응답입니까?
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a51c4248a041d65f00ec1846f60788cded68f7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476605"
---
# <a name="is-odbc-the-answer"></a>ODBC가 응답입니까?
상호 운용성에 대 한 질문을 살펴보기 전에 다음 질문을 고려해 야 합니다. 응용 프로그램에서 ODBC를 사용 해야 하나요? 이는 ODBC에 대 한 가이드를 요청 하는 이상한 질문 일 수 있지만 실제로 합법적인 것입니다. ODBC는 네이티브 데이터베이스 Api를 완전히 대체 하도록 설계 되지 않았고 모든 상황에서 데이터베이스 액세스를 제공 하도록 설계 되었습니다. 이는 데이터베이스에 대 한 공통 인터페이스를 제공 하도록 설계 되었으며 응용 프로그램 프로그래머가 여러 데이터베이스에 대 한 링크를 학습 하 고 유지 관리할 필요가 없습니다.  
  
 사용자 지정 응용 프로그램은 네이티브 데이터베이스 Api에 대 한 주요 후보입니다. 주로 사용자 지정 응용 프로그램은 단일 DBMS에서 작동 하 고 상호 운용할 필요가 없기 때문입니다. 네이티브 데이터베이스 Api는 특정 DBMS의 기능을 노출 하는 ODBC 보다 더 나은 작업을 수행할 수 있으며 ODBC에서 노출 하지 않는 기능을 노출할 수 있습니다. 또한 사용자 지정 응용 프로그램 개발자는 일반적으로 DBMS에 대 한 네이티브 데이터베이스 API에 익숙합니다. ODBC를 학습 하는 이유는 거의 없습니다. 그러나 일부 Dbms의 경우 ODBC는 네이티브 데이터베이스 API입니다.  
  
 그렇다면 어떤 응용 프로그램이 ODBC에 대 한 후보 인가요? 두 개 이상의 DBMS에서 작동 하는 응용 프로그램을 사용 하는 것이 가장 좋습니다. 여기에는 거의 모든 일반 및 수직 응용 프로그램이 포함 됩니다. 또한 다양 한 사용자 지정 응용 프로그램을 포함 합니다. 예를 들어 여러 가지 Dbms를 사용 하는 사용자 지정 응용 프로그램은 여러 네이티브 Api 보다 ODBC를 사용 하 여 훨씬 쉽고 깔끔하고 간단 하 게 작성할 수 있습니다. 회사에서 다른 DBMS로 이동 하거나 다른 dbms에 대해 동일한 응용 프로그램을 배포 하는 경우에는 ODBC로 작성 된 사용자 지정 응용 프로그램을 보다 쉽게 마이그레이션할 수 있습니다.
