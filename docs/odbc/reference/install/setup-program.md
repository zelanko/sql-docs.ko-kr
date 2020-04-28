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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b89cae70db65bd2aa54b8e9789a5c2b35696923e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296153"
---
# <a name="setup-program"></a>설치 프로그램
> **참고:** Windows XP 및 Windows Server 2003부터 **ODBC는 windows 운영 체제에 포함 되어**있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 사용자가 설치 프로그램을 실행 하 여 설치 프로세스를 시작 합니다. 응용 프로그램 또는 드라이버 개발자가 설치 프로그램을 작성 합니다. ODBC 구성 요소를 설치 하는 것 외에 다른 소프트웨어를 설치할 수도 있습니다. 예를 들어 응용 프로그램 개발자는 동일한 설치 프로그램을 사용 하 여 ODBC 구성 요소를 설치 하 고 해당 응용 프로그램을 설치할 수 있습니다.  
  
 개발자는 Microsoft® Windows® SDK 설치 유틸리티 또는 다른 공급 업체의 설치 소프트웨어를 사용 하 여 처음부터 설치 프로그램을 작성할 수 있습니다. 이렇게 하면 이러한 개발자가 설치 프로그램의 모양과 느낌을 완벽 하 게 제어할 수 있습니다. ODBC 응용 프로그램과 같은 추가 소프트웨어를 설치 하도록 설치 프로그램을 작성할 수 있습니다. Windows SDK 설치 유틸리티에 대 한 자세한 내용은 Windows SDK 설명서를 참조 하십시오.  
  
 설치 프로그램에서 실제로 수행 하는 설치의 양은 설치 관리자 DLL에서 호출 하는 함수에 따라 달라 집니다. 설치 관리자 DLL에는 개별 ODBC 구성 요소를 설치 하는 함수가 포함 되어 있습니다. 설치 프로그램은 설치 관리자 DLL에서 **Sqlinstalldrivermanager**, **sqlinstalldrivermanager**또는 **SQLInstallTranslatorEx** 를 호출 하 여 구성 요소를 설치할 디렉터리의 경로를 검색 하 고 구성 요소에 대 한 정보를 레지스트리에 추가 합니다. 이러한 함수는 실제로 파일을 복사 하지 않습니다. 설치 프로그램은 이러한 함수의 인수에 있는 정보를 사용 하 여이를 수행 합니다.  
  
 설치 관리자 DLL에는 ODBC 구성 요소를 제거 하는 함수도 포함 되어 있습니다. 설치 프로그램은 설치 관리자 DLL에서 **SQLRemoveDriverManager**, **SQLRemoveDriver**또는 **SQLRemoveTranslator** 를 호출 하 여 레지스트리의 구성 요소 사용 횟수를 감소 시킵니다. 구성 요소의 새로운 사용 횟수가 0이 되 면 레지스트리에서 구성 요소에 대 한 모든 정보를 제거 합니다. 이러한 함수는 구성 요소에 대 한 파일을 실제로 제거 하지 않습니다. 새 사용 횟수가 0이 되 면 설치 프로그램에서이를 수행 합니다.
