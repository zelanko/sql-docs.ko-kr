---
title: "ODBC 구성 요소 설치 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 383a3a17abb969a57eb2de68b304da4b1bde9a6b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="installing-odbc-components"></a>ODBC 구성 요소 설치
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC만 명시적으로 설치 해야 합니다.  
  
 이 섹션에서는 ODBC 구성 요소는 설치 및 제거 하는 방법을 설명 합니다. 드라이버 개발자는 항상 ODBC 구성 요소 (해당 드라이버)를 설치 하기 때문에이 섹션을 읽어 필요 합니다. 응용 프로그램 개발자가 응용 프로그램과 함께 ODBC 구성 요소는 제공 하는 경우에이 섹션을 읽고 있어야 합니다. ODBC 구성 요소 드라이버 관리자, 드라이버, 변환기, DLL 설치 관리자, 커서 라이브러리 및 모든 관련된 파일을 포함 합니다. 이 섹션에서는 ODBC 응용 프로그램 ODBC 구성 요소로 간주 되지 않습니다.  
  
> [!NOTE]  
>  이 섹션은 Microsoft Windows 플랫폼에 특정 합니다. 다른 플랫폼에서 ODBC 구성 요소가 설치 되는 방식과 플랫폼 마다 다릅니다.  
  
 ODBC 구성 요소 설치 되 고 없습니다-파일 기반은 구성 요소 별로 제거 합니다. 예를 들어는 변환기 구성 된 경우 변환기 자체와 데이터 파일 수, 이러한 파일 설치 되 고 그룹 만들기 때문에 제거 하지 설치 하 고 해야 파일 별로 별로 제거 합니다. 이 대 한 이유 전체가 구성 요소는 시스템에 존재 하는지 확인 하기 위해서입니다.  
  
 설치 및 구성 요소 제거를 위해 다음은 ODBC 구성 요소를 것으로 정의 됩니다.  
  
-   **핵심 구성 요소입니다.** 드라이버 관리자, 커서 라이브러리, DLL, 설치 관리자 및 다른 관련 파일의 핵심 구성 요소를 구성 하 고 설치 하 고 해야 그룹으로 제거 합니다.  
  
-   **드라이버입니다.** 각 드라이버는 별도 구성 요소입니다.  
  
-   **변환기입니다.** 각 변환기는 별도 구성 요소입니다.  
  
 및 이후 버전 ODBC 3.5에 유니코드를 지 원하는 몇 가지 고려해 야 ODBC와 OLE DB 구성 요소를 사용 하 여 합니다. OLE DB Provider for ODBC의 1.1 버전 ODBC 3.0 내 특정 유니코드 사양에 기록 되었습니다. 되기 때문에 이러한 사양은 ODBC 3.5에 변경 되 면 ODBC 3.5를 사용 하는 경우에 버전 1.5 이상의 공급자를 설정할 필요가 이상. 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [설치 구성 요소](../../../odbc/reference/install/installation-components.md)  
  
-   [사용량 계산](../../../odbc/reference/install/usage-counting.md)
