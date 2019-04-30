---
title: ODBC 구성 요소를 설치 합니다. | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5f033ac12569c7de61af071930d6c8d58d8b611
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198232"
---
# <a name="installing-odbc-components"></a>ODBC 구성 요소 설치
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC를 명시적으로 설치 해야 합니다.  
  
 이 섹션에서는 ODBC 구성 요소 설치 및 제거 되는 방법을 설명 합니다. 항상 드라이버 개발자는 ODBC 구성 요소 (해당 드라이버)를 설치 하기 때문에이 섹션을 참조 해야 합니다. 응용 프로그램 개발자가 응용 프로그램을 사용 하 여 ODBC 구성 요소는 전송 하는 경우에이 섹션을 참조 해야 합니다. ODBC 구성 요소는 드라이버 관리자, 드라이버, 변환기, 설치 관리자 DLL, 커서 라이브러리를 및 모든 관련된 파일을 포함 합니다. 이 섹션에서는 ODBC 응용 프로그램은 ODBC 구성 요소로 간주 되지 않습니다.  
  
> [!NOTE]  
>  이 섹션에서는 Microsoft Windows 플랫폼에 따라 다릅니다. ODBC 구성 요소를 다른 플랫폼에서 설치 되는 방식과 플랫폼 마다 다릅니다.  
  
 ODBC 구성 요소가 설치 되 고 제거는 구성 요소 별로 파일 별로 별로 없습니다. 예를 들어, 변환기로 구성 된 경우 변환기의 자체 및 수의 데이터 파일을 이러한 파일 설치 및 제거 되는 그룹으로 이러한 하지 설치 하 고 해야 파일 별로 별로 제거 합니다. 이러한 이유로 전체 구성 요소를 시스템에 존재 하는지 확인 하는 것입니다.  
  
 설치 및 구성 요소 제거를 위해 다음은 ODBC 구성 요소를 정의 됩니다.  
  
-   **핵심 구성 요소입니다.** 드라이버 관리자, 커서 라이브러리, 설치 관리자 DLL 및 다른 관련 파일 핵심 구성 요소를 구성 하 고 설치 하 고 해야 그룹을 제거 합니다.  
  
-   **드라이버입니다.** 각 드라이버는 별도 구성 요소입니다.  
  
-   **변환기입니다.** 각 변환기는 별도 구성 요소입니다.  
  
 유니코드 ODBC 3.5 이상 버전의 지원, 몇 가지 고려 사항 OLE DB 구성 요소를 사용 하 여 ODBC를 사용 하 여 지정 되어야 합니다. OLE DB Provider for ODBC의 1.1 버전은 ODBC 3.0 내 특정 유니코드 사양에 작성 되었습니다. ODBC 3.5에서 이러한 사양은 변경 되므로 ODBC 3.5를 사용 하는 경우 버전 1.5 이상의 공급자가 필요할 이상. 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [설치 구성 요소](../../../odbc/reference/install/installation-components.md)  
  
-   [사용량 계산](../../../odbc/reference/install/usage-counting.md)
