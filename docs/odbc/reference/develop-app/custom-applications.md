---
title: 사용자 지정 응용 프로그램 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df00a748ee4d5e3a63b32c95449417a1057b58e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305284"
---
# <a name="custom-applications"></a>사용자 지정 애플리케이션
사용자 지정 응용 프로그램은 일반적으로 몇 가지 DBMS에 대해 특정 작업을 수행합니다. 예를 들어 응용 프로그램은 단일 DBMS에서 데이터를 검색하고 보고서를 생성하거나 여러 DBMS 간에 데이터를 전송할 수 있습니다. 이러한 응용 프로그램의 공통점은 이러한 DBMS가 응용 프로그램을 작성하기 전에 알려져 있으며 응용 프로그램의 수명 동안 변경될 가능성이 낮다는 것입니다.  
  
 따라서 사용자 지정 응용 프로그램에는 상호 운용성이 거의 또는 전혀 필요하지 않습니다. 응용 프로그램 개발자는 각 DBMS에 대해 단일 드라이버를 선택하고 해당 드라이버에 직접 코드를 만들 수 있습니다. 응용 프로그램은 해당 드라이버의 기능을 악용하기 위해 드라이버 관련 코드를 안전하게 포함할 수 있으며 ODBC에서 지원하지 않는 기능을 사용하기 위해 네이티브 데이터베이스 API를 호출할 수도 있습니다.  
  
 대부분의 사용자 지정 응용 프로그램의 주요 상호 운용성 문제는 나중에 대상 DBMS가 변경될지 여부입니다. 그렇다면 먼저 상호 운용 가능한 코드를 작성하여 이 프로세스를 단순화할 수 있습니다. 그러나 DBMS의 이러한 변경은 드물며 일반적으로 많은 양의 작업이 수반됩니다. 따라서 사용자 지정 응용 프로그램 개발자는 기능을 희생하면서 상호 운용성을 높이는 것을 거의 선택하지 않습니다. 일반적으로 DBMS를 변경할 때 해당 기능을 다시 코딩하도록 선택합니다.
