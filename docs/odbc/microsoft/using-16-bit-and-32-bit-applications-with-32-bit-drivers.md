---
title: 32비트 드라이버가 있는 16비트 및 32비트 애플리케이션 사용 | 마이크로 소프트 문서
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
ms.openlocfilehash: 7ce996a7c4816d4d14491e226f891904b6cf8c02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307614"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>32비트 드라이버와 16비트 및 32비트 애플리케이션 사용
> [!IMPORTANT]  
>  16비트 응용 프로그램 지원은 향후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 32비트 또는 64비트 응용 프로그램을 개발합니다.  
  
 ODBC 데이터 액세스 구성 요소를 사용하면 32비트 드라이버가 있는 16비트 및 32비트 응용 프로그램을 사용할 수 있습니다. 마이크로소프트® 윈도우® 95/98 및 마이크로소프트 윈도 NT®/윈도우 2000 운영 체제 는 응용 프로그램 및 드라이버의 다음과 같은 조합을 지원:  
  
-   32비트 드라이버가 있는 16비트 애플리케이션  
  
-   32비트 드라이버가 있는 32비트 애플리케이션  
  
 16비트 드라이버가 있는 32비트 응용 프로그램을 사용하는 것은 지원되지 않습니다.  
  
> [!NOTE]  
>  ODBC 버전 3.0의 릴리스를 시작으로 Windows NT 4.0이 지원되었습니다.  
  
 ODBC에는 16비트 주소를 32비트 주소로 변환하는 "DDL"(DLL)을 "툰킹"하여 위의 구성을 지원하는 데 필요한 ODBC 구성 요소가 포함되어 있습니다. 설치 프로그램은 사용 중인 운영 체제를 결정하고 해당 시스템에 필요한 ODBC 구성 요소를 설치합니다. 모든 시스템에서 사용되는 ODBC 구성 요소를 설치하도록 선택할 수도 있습니다.  
  
 대부분의 경우 응용 프로그램 또는 드라이버를 16비트에서 32비트로 포팅하려면 다음 5가지 유형의 변경이 필요합니다.  
  
-   메시지 처리 코드 변경 사항  
  
-   정수 와 핸들이 32 비트이기 때문에 변경  
  
-   Windows 응용 프로그램 프로그래밍 인터페이스(API)에 대한 호출 변경 사항  
  
-   드라이버를 스레드안전으로 만들기 위한 변경 사항  
  
-   ODBC 구성 요소 변경  
  
 응용 프로그램 또는 드라이버 프로그래밍 관점에서 16비트 및 32비트 ODBC 구성 요소의 주요 차이점은 파일 이름이 다르다는 것입니다. 시스템 관점에서 볼 때 각 응용 프로그램 또는 드라이버 연결의 아키텍처는 다르며 데이터 원본을 관리하는 데 사용되는 도구는 다릅니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [32비트 드라이버와 16비트 애플리케이션 사용](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [32비트 드라이버와 32비트 애플리케이션 사용](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
