---
description: 사용자 지정 애플리케이션
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56829c72264ba128554af0534e8a6bfa16254142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429395"
---
# <a name="custom-applications"></a>사용자 지정 애플리케이션
사용자 지정 응용 프로그램은 일반적으로 몇 가지 Dbms에 대해 특정 작업을 수행 합니다. 예를 들어 응용 프로그램은 단일 DBMS에서 데이터를 검색 하 고 보고서를 생성 하거나 여러 Dbms 간에 데이터를 전송할 수 있습니다. 이러한 응용 프로그램이 일반적으로 적용 되는 것은 응용 프로그램을 작성 하기 전에 이러한 Dbms를 알 수 있으며 응용 프로그램의 수명 동안 변경 될 가능성은 거의 없습니다.  
  
 따라서 사용자 지정 응용 프로그램에는 상호 운용성이 거의 필요 하지 않습니다. 응용 프로그램 개발자는 각 DBMS에 대 한 단일 드라이버 및 해당 드라이버에 직접 코드를 선택할 수 있습니다. 응용 프로그램은 드라이버 관련 코드를 안전 하 게 포함 하 여 이러한 드라이버의 기능을 활용할 수 있으며, ODBC에서 지원 하지 않는 기능을 사용 하기 위해 네이티브 데이터베이스 API를 호출할 수도 있습니다.  
  
 대부분의 사용자 지정 응용 프로그램의 주요 상호 운용성 문제는 나중에 대상 Dbms가 변경 되는지 여부입니다. 그렇다면에서 시작 하는 상호 운용 가능한 코드를 작성 하 여이 프로세스를 간소화할 수 있습니다. 그러나 이러한 Dbms 변경은 드물게 발생 하며 일반적으로 많은 양의 작업이 수반 됩니다. 이로 인해 사용자 지정 응용 프로그램 개발자는 기능을 활용 하 여 상호 운용성을 높일 수 있습니다. 일반적으로 Dbms를 변경 하는 경우 해당 기능을 recode 선택 합니다.
