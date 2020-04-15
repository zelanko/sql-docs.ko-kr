---
title: 설치 프로그램 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b89cae70db65bd2aa54b8e9789a5c2b35696923e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296153"
---
# <a name="setup-program"></a>설치 프로그램
> **참고:** Windows XP 및 Windows 서버 2003을 시작으로 **ODBC는 Windows 운영 체제에 포함되어 있습니다.** 이전 버전의 Windows에서는 ODBC만 명시적으로 설치해야 합니다.  
  
 사용자가 설치 프로그램을 실행하여 설치 프로세스를 시작합니다. 설치 프로그램은 응용 프로그램 또는 드라이버 개발자가 작성합니다. ODBC 구성 요소를 설치하는 것 외에도 다른 소프트웨어를 설치할 수 있습니다. 예를 들어 응용 프로그램 개발자는 ODBC 구성 요소를 설치하고 응용 프로그램을 설치하기 위해 동일한 설치 프로그램을 사용할 수 있습니다.  
  
 개발자는 Microsoft® Windows® SDK 설치 유틸리티 또는 다른 공급업체의 설치 소프트웨어를 사용하여 처음부터 설치 프로그램을 작성할 수 있습니다. 이를 통해 개발자는 설치 프로그램의 모양과 느낌을 완벽하게 제어할 수 있습니다. 설치 프로그램은 ODBC 응용 프로그램과 같은 추가 소프트웨어를 설치하도록 작성할 수 있습니다. Windows SDK 설치 유틸리티에 대한 자세한 내용은 Windows SDK 설명서를 참조하십시오.  
  
 설치 프로그램에서 실제로 수행되는 설치량은 설치 프로그램 DLL에서 호출하는 기능에 따라 다릅니다. 설치 관리자 DLL에는 개별 ODBC 구성 요소를 설치하는 기능이 포함되어 있습니다. 설치 프로그램은 단순히 **SQLInstallDriverManager,** **SQLInstallDriverEx**또는 **SQLInstallTranslatorEx를** 설치 프로그램 DLL에서 호출하여 구성 요소를 설치할 디렉터리 경로를 검색하고 구성 요소에 대한 정보를 레지스트리에 추가합니다. 이러한 함수는 실제로 파일을 복사하지 않습니다. 설치 프로그램은 이러한 함수의 인수에 있는 정보를 사용하여 이 작업을 수행합니다.  
  
 설치 관리자 DLL에는 ODBC 구성 요소를 제거하는 기능도 포함되어 있습니다. 설치 프로그램은 **SQLRemoveDriverManager,** **SQLRemoveDriver**또는 **SQLRemoveTranslator를** 호출하여 설치 관리자 DLL에서 구성 요소의 사용 수를 제거하고 구성 요소의 새 사용 수가 0으로 떨어지면 레지스트리에서 구성 요소에 대한 모든 정보를 제거합니다. 이러한 함수는 실제로 구성 요소의 파일을 제거하지 않습니다. 새 사용량 수가 0으로 떨어지면 설치 프로그램에서 이 작업을 수행합니다.
