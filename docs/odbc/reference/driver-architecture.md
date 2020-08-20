---
description: 드라이버 아키텍처
title: 드라이버 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 530940cef233b8a6b6a3f5c0575dd154998126cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494616"
---
# <a name="driver-architecture"></a>드라이버 아키텍처
드라이버 아키텍처는 SQL 문을 처리 하는 소프트웨어에 따라 다음과 같은 두 가지 범주로 나뉩니다.  
  
-   **파일 기반 드라이버** 드라이버는 물리적 데이터에 직접 액세스 합니다. 이 경우 드라이버는 드라이버 및 데이터 원본 역할을 합니다. 즉, ODBC 호출 및 SQL 문을 처리 합니다. 예를 들어 dbase 드라이버는 드라이버에서 사용할 수 있는 독립 실행형 데이터베이스 엔진을 제공 하지 않으므로 파일 기반 드라이버입니다. 파일 기반 드라이버의 개발자는 자신의 데이터베이스 엔진을 작성 해야 합니다.  
  
-   **DBMS 기반 드라이버** 드라이버는 별도의 데이터베이스 엔진을 통해 실제 데이터에 액세스 합니다. 이 경우 드라이버는 ODBC 호출만 처리 합니다. 처리를 위해 SQL 문을 데이터베이스 엔진에 전달 합니다. 예를 들어 oracle 드라이버는 드라이버에서 사용 하는 독립 실행형 데이터베이스 엔진을 포함 하므로 DBMS 기반 드라이버입니다. 데이터베이스 엔진이 있는 위치는 어떤 않으므로입니다. 드라이버 또는 네트워크 상의 다른 컴퓨터와 동일한 컴퓨터에 있을 수 있습니다. 게이트웨이를 통해 액세스할 수도 있습니다.  
  
 드라이버 아키텍처는 일반적으로 드라이버 작성자 에게만 흥미롭습니다. 즉, 드라이버 아키텍처는 일반적으로 응용 프로그램에 차이가 없습니다. 그러나 아키텍처는 응용 프로그램에서 DBMS 관련 SQL을 사용할 수 있는지 여부에 영향을 줄 수 있습니다. 예를 들어 Microsoft Access는 독립 실행형 데이터베이스 엔진을 제공 합니다. Microsoft 액세스 드라이버가 DBMS 기반 인 경우이 엔진을 통해 데이터에 액세스 합니다. 응용 프로그램은 처리를 위해 Microsoft Access SQL 문을 엔진에 전달할 수 있습니다.  
  
 그러나 드라이버가 파일을 기반으로 하는 경우 (즉, Microsoft® Access .mdb 파일에 직접 액세스 하는 소유 엔진을 포함 하는 경우) Microsoft Access 특정 SQL 문을 엔진에 전달 하려고 하면 구문 오류가 발생할 수 있습니다. 그 이유는 소유 엔진이 ODBC SQL만 구현할 가능성이 있기 때문입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [파일 기반 드라이버](../../odbc/reference/file-based-drivers.md)  
  
-   [DBMS 기반 드라이버](../../odbc/reference/dbms-based-drivers.md)  
  
-   [네트워크 예제](../../odbc/reference/network-example.md)  
  
-   [기타 드라이버 아키텍처](../../odbc/reference/other-driver-architectures.md)
