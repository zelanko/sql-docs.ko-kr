---
title: 설치 구성 요소 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a196e9b935229fa03c6dd0eda92b8e99e69f0ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285253"
---
# <a name="installation-components"></a>설치 구성 요소
> [!NOTE]  
>  Windows XP 및 Windows 서버 2003을 시작으로 ODBC는 Windows 운영 체제에 포함되어 있습니다. 이전 버전의 Windows에서는 ODBC만 명시적으로 설치해야 합니다.  
  
 설치 프로세스는 사용자가 설치 프로그램을 실행하면 시작됩니다. 설치 프로그램은 *설치 프로그램 DLL* 및 각 드라이버에 대한 *드라이버 설정 DLL과* 함께 작동합니다. 설치 프로그램과 설치 관리자 DLL은 **SQLInstallDriverEx** 및 **SQLInstallTranslatorEx** 함수의 인수를 사용하여 각 구성 요소에 대해 복사하거나 삭제할 파일을 결정합니다. 다음 그림에서는 이러한 설치 구성 요소 간의 관계를 보여 주시고 있습니다.  
  
 ![설치 구성 요소 간의 관계](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  ODBC *2.x에서* 각 ODBC 구성 요소에 필요한 파일을 설명하는 데 사용된 Odbc.inf 파일은 ODBC *3.x에서*사용되지 않습니다. ODBC *3.x* 구성 요소를 제공하는 드라이버는 Odbc.inf 파일을 만들 필요가 없습니다. **SQLInstallDriver** 및 **SQLInstallODBC의**제거 및 **SQLInstallTranslator의**사용 중단은 Odbc.inf를 불필요하게 렌더링했습니다. Odbc.inf의 드라이버 키워드 섹션에 사용 되 었던 드라이버 정보는 이제 **SQLInstallDriverEx의** *lpszDriver* 인수에 제공 됩니다. Odbc.inf의 [ODBC 번역기] 및 번역기 사양 섹션에 사용 되 었던 번역기 정보는 이제 **SQLInstallTranslatorEx의** *lpszTranslator* 인수에 제공 됩니다. 이러한 변경 사항을 통해 ODBC 설치 프로그램을 플랫폼 전체에서 보다 이식가능하게 사용할 수 있습니다.  
  
 이러한 구성 요소에 대한 자세한 내용은 이 섹션의 끝에 있는 다음 항목을 참조하십시오.  
  
-   [설치 프로그램](../../../odbc/reference/install/setup-program.md)  
  
-   [설치 관리자 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [드라이버 설치 DLL](../../../odbc/reference/install/driver-setup-dll.md)
