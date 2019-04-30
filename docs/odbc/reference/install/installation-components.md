---
title: 설치 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a883377a17aa9e0c3426b4805263616375ea6215
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198396"
---
# <a name="installation-components"></a>설치 구성 요소
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC를 명시적으로 설치 해야 합니다.  
  
 설치 프로세스에는 사용자는 설치 프로그램을 실행할 때 시작 됩니다. 설치 프로그램을 함께 작동 합니다 *설치 관리자 DLL* 및 *드라이버 설치 DLL* 각 드라이버에 대 한 합니다. 인수를 사용 하 여 설치 프로그램 및 설치 관리자 DLL **SQLInstallDriverEx** 하 고 **SQLInstallTranslatorEx** 파일을 복사 하거나 각 구성 요소에 대 한 삭제를 확인 하는 함수입니다. 다음 그림에서는 이러한 설치 구성 요소 간의 관계를 보여 줍니다.  
  
 ![설치 구성 요소 간의 관계](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  ODBC 2에 사용 된 Odbc.inf 파일입니다. *x* 각 ODBC에서 필요한 파일을 설명 하기 위해 구성 요소 ODBC 3에서 사용 되지 않습니다 *.x*합니다. ODBC 3 제공 되는 드라이버 *.x* 구성 요소를 Odbc.inf 파일을 만들 필요가 없습니다. 제거 **SQLInstallDriver** 및 **SQLInstallODBC**, 및의 사용 중단 **SQLInstallTranslator**, Odbc.inf 불필요 한 렌더링 해야 합니다. Odbc.inf Driver 키워드 섹션에서 사용 되는 드라이버 정보에서 제공 됩니다는 *lpszDriver* 에서 인수 **SQLInstallDriverEx**합니다. [ODBC 변환기]에 사용 하는 변환기 정보 및 Odbc.inf의 변환기 사양 섹션에서 제공 됩니다는 *lpszTranslator* 인수의 **SQLInstallTranslatorEx**합니다. 이러한 변경 내용은 플랫폼 간에 이식 가능 하도록 ODBC 설치 관리자를 허용 합니다.  
  
 이러한 구성 요소에 대 한 자세한 내용은이 섹션의 끝에 다음 항목을 참조 하세요.  
  
-   [설치 프로그램](../../../odbc/reference/install/setup-program.md)  
  
-   [설치 관리자 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [드라이버 설치 DLL](../../../odbc/reference/install/driver-setup-dll.md)
