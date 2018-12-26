---
title: 사용자 지정 응용 프로그램 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ab470951162b5e4035c1253ed4ce425356ad8ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799861"
---
# <a name="custom-applications"></a>사용자 지정 애플리케이션
사용자 지정 응용 프로그램은 일반적으로 몇 가지 Dbms에 대 한 특정 작업을 수행 합니다. 예를 들어, 응용 프로그램 수는 단일 DBMS에서 데이터를 검색 하 고 보고서를 생성 하거나 여러 Dbms 간에 데이터를 전송할 수 있습니다. 이러한 응용 프로그램의 공통점은 이러한 Dbms 응용 프로그램 기록 되기 전에 알려진 응용 프로그램의 수명 동안 변경 될 가능성이 없는입니다.  
  
 따라서 사용자 지정 응용 프로그램에 거의 또는 전혀 상호 운용성에 필요합니다. 응용 프로그램 개발자는 각 DBMS 및 드라이버에 직접 코드에 대 한 단일 드라이버를 선택할 수 있습니다. 응용 프로그램이 드라이버의 기능을 이용 하려면 드라이버 관련 코드를 안전 하 게 포함 될 수 있습니다 및도 ODBC에서 지원 되지 않습니다 하는 기능을 사용 하려면 네이티브 데이터베이스 API 호출 해야 합니다.  
  
 대부분의 사용자 지정 응용 프로그램의 주요 상호 운용성 문제를 대상 Dbms 나중에 변경 될 여부입니다. 그렇다면 시작 상호 운용성이 우수한 코드를 작성 하 여이 프로세스를 단순화할 수 있습니다. 그러나 이러한 변경의 Dbms 드물게 발생 하며 일반적으로 많은 양의 작업을 수반 합니다. 이 인해 사용자 지정 응용 프로그램 개발자는 거의 선택 기능 저하 상호 운용성을 높이기 위해 일반적으로 Dbms 변경 될 때 해당 기능을 다시 코딩을 선택 합니다.
