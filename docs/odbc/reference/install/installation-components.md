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
ms.openlocfilehash: 34d1b6d143f6f40d73e2feeb0b718f3c3b3248fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094132"
---
# <a name="installation-components"></a>설치 구성 요소
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC는 Windows 운영 체제에 포함 되어 있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 설치 프로세스는 사용자가 설치 프로그램을 실행할 때 시작 됩니다. 설치 프로그램은 각 드라이버에 대 한 설치 *관리자 dll* 및 *드라이버 설치 dll* 과 함께 작동 합니다. 설치 프로그램과 설치 관리자 DLL은 모두 **Sqlinstalldriverex** 및 **SQLInstallTranslatorEx** 함수에서 인수를 사용 하 여 각 구성 요소에 대해 복사 하거나 삭제할 파일을 결정 합니다. 다음 그림에서는 이러한 설치 구성 요소 간의 관계를 보여 줍니다.  
  
 ![설치 구성 요소 간의 관계](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  Odbc 2.x에서 각 ODBC 구성 요소에 필요한 파일을 *설명 하는* 데 사용 된 odbc .inf 파일 *은 odbc 3.x*에서 사용 되지 않습니다. ODBC *3.x 구성 요소* 를 제공 하는 드라이버는 odbc .inf 파일을 만들 필요가 없습니다. **Sqlinstalldriver** 및 **SQLInstallODBC**를 제거 하 고 **sqlinstalldriver**의 사용 중단을 제거 하는 경우에는 Odbc를 렌더링 하지 않아도 됩니다. 이제 Odbc .inf의 Driver 키워드 섹션에 사용 되는 드라이버 정보가 **Sqlinstalldriverex**의 *lpszDriver* 인수에 제공 됩니다. 이제 Odbc .inf의 [ODBC 변환기] 및 번역기 사양 섹션에 사용 되는 변환기 정보가 **SQLInstallTranslatorEx**의 *lpszTranslator* 인수에 제공 됩니다. 이러한 변경으로 ODBC 설치 관리자를 플랫폼 간에 더 이식할 수 있습니다.  
  
 이러한 구성 요소에 대 한 자세한 내용은이 섹션의 끝에 있는 다음 항목을 참조 하십시오.  
  
-   [설치 프로그램](../../../odbc/reference/install/setup-program.md)  
  
-   [설치 관리자 DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [드라이버 설정 DLL](../../../odbc/reference/install/driver-setup-dll.md)
