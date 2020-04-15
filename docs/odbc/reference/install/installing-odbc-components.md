---
title: ODBC 부품 설치 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd0a6aeba8073ce14b08b8635396b1f231895fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298983"
---
# <a name="installing-odbc-components"></a>ODBC 구성 요소 설치
> [!NOTE]  
>  Windows XP 및 Windows 서버 2003을 시작으로 ODBC는 Windows 운영 체제에 포함되어 있습니다. 이전 버전의 Windows에서는 ODBC만 명시적으로 설치해야 합니다.  
  
 이 섹션에서는 ODBC 구성 요소를 설치하고 제거하는 방법에 대해 설명합니다. 드라이버 개발자는 항상 ODBC 구성 요소(드라이버)를 설치하기 때문에 이 섹션을 읽어야 합니다. 응용 프로그램 개발자는 ODBC 구성 요소를 응용 프로그램과 함께 제공할 경우에만 이 섹션을 읽어야 합니다. ODBC 구성 요소에는 드라이버 관리자, 드라이버, 번역기, 설치 관리자 DLL, 커서 라이브러리 및 관련 파일이 포함됩니다. 이 섹션의 목적상 ODBC 응용 프로그램은 ODBC 구성 요소로 간주되지 않습니다.  
  
> [!NOTE]  
>  이 섹션은 Microsoft Windows 플랫폼에만 해당됩니다. ODBC 구성 요소가 다른 플랫폼에 설치되는 방식은 플랫폼에 따라 다릅니다.  
  
 ODBC 구성 요소는 파일별로 설치되지 않고 구성 요소별로 설치및 제거됩니다. 예를 들어, 번역기가 번역기 자체와 여러 데이터 파일로 구성된 경우 이러한 파일은 그룹으로 설치되고 제거됩니다. 파일단위로 설치및 제거해서는 안 됩니다. 그 이유는 시스템에 완전한 구성 요소만 있는지 확인하기 위해서입니다.  
  
 구성 요소를 설치하고 제거하기 위해 다음을 ODBC 구성 요소로 정의합니다.  
  
-   **핵심 구성 요소입니다.** 드라이버 관리자, 커서 라이브러리, 설치 관리자 DLL 및 기타 관련 파일은 핵심 구성 요소를 구성하므로 그룹으로 설치 및 제거해야 합니다.  
  
-   **드라이버.** 각 드라이버는 별도의 구성 요소입니다.  
  
-   **번역.** 각 번역기는 별도의 구성 요소입니다.  
  
 ODBC 3.5 이상에서 유니코드를 지원하므로 ODBC가 있는 OLE DB 구성 요소를 사용하는 데 몇 가지 고려 사항이 주어져야 합니다. ODBC용 OLE DB 공급자의 1.1 버전은 ODBC 3.0 내의 특정 유니코드 사양으로 작성되었습니다. 이러한 사양은 ODBC 3.5에서 변경되므로 ODBC 3.5 이상을 사용할 때 공급자의 버전 1.5 이상이 필요합니다. 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [설치 구성 요소](../../../odbc/reference/install/installation-components.md)  
  
-   [사용량 계산](../../../odbc/reference/install/usage-counting.md)
