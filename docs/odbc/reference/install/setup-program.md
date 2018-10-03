---
title: 설치 프로그램 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f64eda5ad640e50afd25db111de74141e41e652d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722151"
---
# <a name="setup-program"></a>설치 프로그램
> **참고:** Windows XP 및 Windows Server 2003 부터는 **ODBC Windows 운영 체제에 포함 되어**입니다. 이전 버전의 Windows에서 ODBC를 명시적으로 설치 해야 합니다.  
  
 사용자는 설치 프로세스를 시작 하려면 설치 프로그램을 실행 합니다. 설치 프로그램은 응용 프로그램 또는 드라이버 개발자가 기록 됩니다. ODBC 구성 요소를 설치 하는 것 외에도 다른 소프트웨어를 설치할 수 있습니다. 예를 들어, 응용 프로그램 개발자가 ODBC 구성 요소를 설치 하 고 응용 프로그램을 설치 하려면 동일한 설치 프로그램을 사용할 수 있습니다.  
  
 개발자는 Microsoft® Windows® SDK 설치 유틸리티 또는 다른 공급 업체의 설치 소프트웨어를 사용 하 여 설치 프로그램을 처음부터 작성할 수 있습니다. 이 통해 이러한 개발자는 설치 프로그램의 모양과 느낌을 완전히 제어 합니다. ODBC 응용 프로그램 등의 추가 소프트웨어를 설치 하려면 설치 프로그램을 작성할 수 있습니다. Windows SDK 설치 유틸리티에 대 한 자세한 내용은 Windows SDK 설명서를 참조 하세요.  
  
 설치의 실제 수행 되는 설치 프로그램에서 설치 관리자 DLL에서에서 호출 함수에 따라 달라 집니다. 설치 관리자 DLL에는 개별 ODBC 구성 요소를 설치 하는 함수가 포함 됩니다. 설치 프로그램 호출 **SQLInstallDriverManager**를 **SQLInstallDriverEx**, 또는 **SQLInstallTranslatorEx** 설치 관리자의 경로 검색 하는 DLL에는 구성 요소는 설치 되 고 레지스트리에 구성 요소에 대 한 정보를 추가 하는 디렉터리입니다. 이러한 함수 파일을 실제로 복사 하지 않으려면 설치 프로그램 정보를 사용 하 여 이러한 함수의 인수에이 수행 합니다.  
  
 또한 설치 관리자 DLL에는 ODBC 구성 요소를 제거 하는 함수가 포함 됩니다. 설치 프로그램 호출 **SQLRemoveDriverManager**를 **SQLRemoveDriver**, 또는 **SQLRemoveTranslator** 설치 관리자에서 구성 요소의 사용량 감소 하는 DLL의 수를 레지스트리 및 해당 구성 요소의 새 사용 횟수가 0으로 떨어지면 레지스트리에서 구성 요소에 대 한 모든 정보를 제거 합니다. 이러한 함수는 구성 파일을 완전히 제거 하지 마십시오 설치 프로그램을이 새 사용 횟수를 0으로 떨어지면 수행 합니다.
