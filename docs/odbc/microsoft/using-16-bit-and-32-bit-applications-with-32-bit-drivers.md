---
title: "16 비트 및 32 비트 응용 프로그램을 사용 하 여 32 비트 드라이버와 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 802b09dd83ce3671edbff33ff2be447c6279621f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>32 비트 드라이버와 16 비트 및 32 비트 응용 프로그램을 사용 하 여
> [!IMPORTANT]  
>  16 비트 응용 프로그램 지원은 이후 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. 대신 32 비트 또는 64 비트 응용 프로그램을 개발 합니다.  
  
 ODBC 데이터 액세스 구성 요소와 32 비트 드라이버와 16 비트 및 32 비트 응용 프로그램을 사용할 수 있습니다. Microsoft® Windows® 95/98 및 Microsoft Windows/Windows 2000 운영 체제는 응용 프로그램 및 드라이버의 다음과 같은 조합을 지원합니다.  
  
-   32 비트 드라이버와 16 비트 응용 프로그램  
  
-   32 비트 드라이버와 32 비트 응용 프로그램  
  
 32 비트 응용 프로그램을 사용 하 여 16 비트 드라이버와 함께 지원 되지 않습니다.  
  
> [!NOTE]  
>  ODBC 버전 3.0의 릴리스를 시작 하 고, Windows NT 4.0 지원 했습니다.  
  
 ODBC 위 구성을 "썽킹" 동적 연결 라이브러리 (Dll) 32 비트 주소를 16 비트 주소를 변환 하 여 그 반대의 지원 하기 위해 필요한 ODBC 구성 요소를 포함 합니다. 설치 프로그램을 사용 하 고 해당 시스템에 필요한 ODBC 구성 요소를 설치 하는 운영 체제를 결정 합니다. 또한 모든 시스템에서 사용 하는 ODBC 구성 요소를 설치할 수 있습니다.  
  
 대부분의 경우에서 응용 프로그램 또는 드라이버에서 16 비트 이식 32 비트를 5 가지 유형의 변경 내용이 포함 됩니다.  
  
-   메시지 처리 코드를 변경  
  
-   32 비트 정수 및 핸들 수 있으므로 변경  
  
-   Windows 응용 프로그램 프로그래밍 인터페이스 (Api)에 대 한 호출에서 변경 내용  
  
-   스레드로부터 안전한 드라이버 확인에 대 한 변경  
  
-   ODBC 구성 요소에 대 한 변경  
  
 응용 프로그램 또는 드라이버 프로그래밍 관점에서 16 비트 및 32 비트 ODBC 구성 요소 간의 주요한 차이점은 파일 이름을 다르게 수 있는 것입니다. 시스템의 관점에서 각 응용 프로그램 또는 드라이버 연결의 아키텍처는 서로 다른 되며 데이터 원본을 관리 하는 데 사용 되는 도구 서로 다릅니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [32비트 드라이버와 16비트 응용 프로그램 사용](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [32비트 드라이버와 32비트 응용 프로그램 사용](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)

