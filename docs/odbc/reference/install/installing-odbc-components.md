---
title: ODBC 구성 요소 설치 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298983"
---
# <a name="installing-odbc-components"></a>ODBC 구성 요소 설치
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC는 Windows 운영 체제에 포함 되어 있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 이 섹션에서는 ODBC 구성 요소를 설치 및 제거 하는 방법을 설명 합니다. 드라이버 개발자는 항상 ODBC 구성 요소 (드라이버)를 설치 하므로이 섹션을 읽어야 합니다. 응용 프로그램 개발자는 ODBC 구성 요소가 응용 프로그램과 함께 제공 되는 경우에만이 섹션을 읽어야 합니다. ODBC 구성 요소에는 드라이버 관리자, 드라이버, 번역기, 설치 관리자 DLL, 커서 라이브러리 및 모든 관련 파일이 포함 됩니다. 이 섹션에서는 odbc 응용 프로그램을 ODBC 구성 요소로 간주 하지 않습니다.  
  
> [!NOTE]  
>  이 섹션은 Microsoft Windows 플랫폼에만 적용 됩니다. 다른 플랫폼에 ODBC 구성 요소를 설치 하는 방법은 플랫폼별로 지정 합니다.  
  
 ODBC 구성 요소는 파일을 기준으로 구성 요소 별로 설치 및 제거 됩니다. 예를 들어 변환기가 변환기 자체와 많은 데이터 파일로 구성 된 경우 이러한 파일은 그룹으로 설치 되 고 제거 됩니다. 이러한 파일은 파일을 기준으로 설치 및 제거 되지 않아야 합니다. 그 이유는 전체 구성 요소만 시스템에 존재 하도록 하는 것입니다.  
  
 구성 요소를 설치 및 제거 하기 위해 다음은 ODBC 구성 요소로 정의 됩니다.  
  
-   **핵심 구성 요소입니다.** 드라이버 관리자, 커서 라이브러리, 설치 관리자 DLL 및 기타 관련 파일은 핵심 구성 요소를 구성 하며 그룹으로 설치 하 고 제거 해야 합니다.  
  
-   **장치.** 각 드라이버는 개별 구성 요소입니다.  
  
-   **번역자.** 각 번역기는 개별 구성 요소입니다.  
  
 ODBC 3.5 이상에서 유니코드를 지원 하므로 ODBC와 함께 OLE DB 구성 요소를 사용 하려면 몇 가지 사항을 고려해 야 합니다. Odbc 용 OLE DB 공급자 1.1 버전은 ODBC 3.0 내의 특정 유니코드 사양에 기록 되었습니다. ODBC 3.5에서는 이러한 사양이 변경 되었으므로 ODBC 3.5 이상을 사용할 때 버전 1.5 이상의 공급자가 있어야 합니다. 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [설치 구성 요소](../../../odbc/reference/install/installation-components.md)  
  
-   [사용량 계산](../../../odbc/reference/install/usage-counting.md)
