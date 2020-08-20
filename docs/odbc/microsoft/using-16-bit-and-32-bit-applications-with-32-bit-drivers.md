---
description: 32비트 드라이버와 16비트 및 32비트 애플리케이션 사용
title: 32 비트 드라이버에서 16 비트 및 32 비트 응용 프로그램 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3985fa6fa4fd24ad9638e418915542b48abc26f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471378"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>32비트 드라이버와 16비트 및 32비트 애플리케이션 사용
> [!IMPORTANT]  
>  16 비트 응용 프로그램 지원은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 32 비트 또는 64 비트 응용 프로그램을 개발 하세요.  
  
 ODBC 데이터 액세스 구성 요소를 사용 하면 32 비트 드라이버에서 16 비트 및 32 비트 응용 프로그램을 사용할 수 있습니다. Microsoft® Windows® 95/98 및 Microsoft Windows NT®/Windows 2000 운영 체제는 다음과 같은 응용 프로그램 및 드라이버 조합을 지원 합니다.  
  
-   32 비트 드라이버를 사용 하는 16 비트 응용 프로그램  
  
-   32 비트 드라이버를 사용 하는 32 비트 응용 프로그램  
  
 16 비트 드라이버에서 32 비트 응용 프로그램을 사용 하는 것은 지원 되지 않습니다.  
  
> [!NOTE]  
>  ODBC 버전 3.0 릴리스 부터는 Windows NT 4.0이 지원 됩니다.  
  
 ODBC에는 "썽킹" Dll (동적 연결 라이브러리)에서 16 비트 주소를 32 비트 주소로 변환 하 고 그 반대로 변환 하는 데 필요한 ODBC 구성 요소가 포함 되어 있습니다. 설치 프로그램은 사용 중인 운영 체제를 결정 하 고 해당 시스템에 필요한 ODBC 구성 요소를 설치 합니다. 모든 시스템에서 사용 하는 ODBC 구성 요소를 설치 하도록 선택할 수도 있습니다.  
  
 대부분의 경우 응용 프로그램 또는 드라이버를 16 비트에서 32 비트로 포팅 하는 데는 5 가지 변경 사항이 포함 됩니다.  
  
-   메시지 처리 코드 변경  
  
-   정수 및 핸들이 32 비트 이기 때문에 변경  
  
-   Windows Api (응용 프로그래밍 인터페이스)에 대 한 호출의 변경 내용  
  
-   드라이버를 스레드로부터 안전 하 게 만들기 위한 변경 내용  
  
-   ODBC 구성 요소에 대 한 변경 내용  
  
 응용 프로그램 또는 드라이버 프로그래밍 측면에서 16 비트와 32 비트 ODBC 구성 요소의 주요 차이점은 파일 이름이 다르다는 것입니다. 시스템 관점에서 각 응용 프로그램 또는 드라이버 연결의 아키텍처가 다르며 데이터 소스를 관리 하는 데 사용 되는 도구는 다릅니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [32비트 드라이버와 16비트 애플리케이션 사용](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [32비트 드라이버와 32비트 애플리케이션 사용](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
