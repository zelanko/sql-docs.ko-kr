---
description: 일반 애플리케이션
title: 일반 응용 프로그램 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9980edcaf34182b4c7f43aa8e935d095f2345138
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476685"
---
# <a name="generic-applications"></a>일반 애플리케이션
일반 응용 프로그램에서는 때때로 데이터베이스에서 데이터를 검색 하는 스프레드시트와 같은 하드 코딩 된 작업을 수행 합니다. 사용자가 SQL 문을 입력 하 고 실행할 수 있도록 하는 일반 쿼리 응용 프로그램과 같은 다양 한 사용자 정의 태스크를 수행할 수도 있습니다. 일반적으로 사용 되는 일반적인 응용 프로그램은 다양 한 Dbms를 사용 해야 하며 개발자가 이러한 Dbms를 미리 알지 못하는 것입니다.  
  
 따라서 제네릭 응용 프로그램은 상호 운용성이 매우 중요 해야 합니다. 개발자는 다양 한 옵션을 설정 하 여 기능에 대 한 상호 운용성을 확보 하 고, 다양 한 기능을 지 원하는 드라이버를 필요로 하는 코드를 작성 해야 합니다. 일반 응용 프로그램은 인기 있는 Dbms에서 작동 하도록 조정 될 수 있지만 드라이버 특정 또는 DBMS 관련 코드는 거의 포함 하지 않습니다.
