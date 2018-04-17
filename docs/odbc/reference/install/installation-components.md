---
title: 설치 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1e8d3c6f5362cef672c5aa02b7547fa86040b4aa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="installation-components"></a>설치 구성 요소
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC만 명시적으로 설치 해야 합니다.  
  
 설치 프로세스가 시작 된 사용자가 설치 프로그램을 실행 합니다. 와 함께에서 작동 하는 설치 프로그램은 *installer DLL* 및 *드라이버 설치 DLL* 각 드라이버에 대 한 합니다. 인수를 사용 하 여 설치 프로그램과 DLL 설치 관리자는 **SQLInstallDriverEx** 및 **SQLInstallTranslatorEx** 함수를 복사 하거나 각 구성 요소에 대 한 삭제 된 파일을 확인 합니다. 다음 그림은 이러한 설치 구성 요소 간의 관계를 보여줍니다.  
  
 ![설치 구성 요소 간의 관계](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]  
>  ODBC 2에서 사용 된 Odbc.inf 파일입니다. *x* ODBC 3 사용 되지 않는 구성 요소의 각 ODBC에 필요한 파일을 설명 하기 위해*.x*합니다. ODBC 3 제공 드라이버를*.x* 구성 요소를 Odbc.inf 파일을 만들 필요가 없습니다. 제거 하 고 **SQLInstallDriver** 및 **SQLInstallODBC**, 및의 사용 중단 **SQLInstallTranslator**, 불필요 한 Odbc.inf을 렌더링 해야 합니다. Odbc.inf의 드라이버 키워드 섹션에서 사용 되는 드라이버 정보에서 제공 됩니다는 *lpszDriver* 인수 **SQLInstallDriverEx**합니다. [ODBC 변환기]에 포함 되도록 사용 하는 변환기 정보 및 Odbc.inf의 변환기 사양 섹션에서 제공 됩니다는 *lpszTranslator* 의 인수 **SQLInstallTranslatorEx**합니다. 이러한 변경 내용을 통해 플랫폼 간에 이식 가능 하도록 ODBC 설치 합니다.  
  
 이러한 구성 요소에 대 한 자세한 내용은이 섹션의 끝에 다음 항목을 참조 합니다.  
  
-   [설치 프로그램](../../../odbc/reference/install/setup-program.md)  
  
-   [설치 관리자 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [드라이버 설치 DLL](../../../odbc/reference/install/driver-setup-dll.md)
