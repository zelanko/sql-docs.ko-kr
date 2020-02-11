---
title: 사용량 계산 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: edf9976dd3e5d890b46919808e896a8e81a0cd93
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093787"
---
# <a name="usage-counting"></a>사용량 계산
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC는 Windows 운영 체제에 포함 되어 있습니다. ODBC는 이전 버전의 Windows에만 명시적으로 설치 해야 합니다.  
  
 구성 요소 사용 횟수 및 하나 이상의 선택적 파일 사용 횟수와 같은 두 가지 유형의 사용 개수가 레지스트리에서 각 구성 요소에 대해 유지 관리 됩니다. 구성 요소 사용 횟수는 설치 관리자 DLL에서 레지스트리 항목을 유지 관리 하는 데 도움이 됩니다. 이 값은 ODBC Core, 드라이버 및 변환기 하위 키 아래에 있는 UsageCount 값에 저장 됩니다. UsageCount 값의 형식과 이러한 하위 키에 대 한 자세한 내용은 [ODBC 구성 요소에 대 한 레지스트리 항목](../../../odbc/reference/install/registry-entries-for-odbc-components.md)을 참조 하세요.  
  
 구성 요소가 처음 설치 될 때 설치 관리자 DLL은이에 대 한 하위 키를 만들고 해당 하위 키에 UsageCount 값에 대 한 데이터를 1로 설정 합니다. 구성 요소가 다시 설치 되 면 설치 관리자 DLL이 사용 횟수를 늘립니다. 구성 요소가 제거 되 면 설치 관리자 DLL이 사용 횟수를 감소 시킵니다. 사용 횟수가 0이 되 면 설치 관리자 DLL에서 구성 요소에 대 한 하위 키를 제거 합니다.  
  
> [!CAUTION]  
>  구성 요소 사용 횟수와 파일 사용 횟수가 0에 도달 하면 응용 프로그램에서 드라이버 관리자 파일을 물리적으로 제거 하면 안 됩니다.  
  
 파일 사용 횟수는 사용 횟수를 증가 또는 감소 시키는 것과는 반대로 파일을 실제로 복사 하거나 삭제 해야 하는 경우를 결정 하는 데 도움이 됩니다. Odbc 구성 요소와 ODBC 구성 요소의 파일은 공유 되므로 다양 한 응용 프로그램에서 설치 하거나 제거할 수 있기 때문에이는 중요 합니다. 구성 요소 사용 횟수와 파일 사용 횟수가 0에 도달 하면 응용 프로그램에서 드라이버 및 번역기 파일을 삭제할 수 있습니다. 그러나 파일 사용 횟수를 증가 하지 않은 다른 응용 프로그램에서 이러한 파일을 사용할 수 있기 때문에 구성 요소 사용 횟수와 파일 사용 횟수가 모두 0에 도달 하는 경우에는 드라이버 관리자 파일을 삭제 하면 안 됩니다.  
  
> [!NOTE]  
>  파일 사용 횟수는 Microsoft® Windows nt®/Windows2000.에서 선택 사항입니다.  
  
 파일 사용 횟수는 **Sqlinstalldrivermanager**, **sqlinstalldrivermanager**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**또는 **SQLRemoveTranslator**를 호출한 후 설치 프로그램에 의해 유지 관리 됩니다.  
  
 구성 요소를 처음 설치 하는 경우 설치 프로그램 또는 설치 관리자 DLL은 시스템에 아직 없는 해당 구성 요소의 각 파일에 대해 다음 키 아래에 값을 만듭니다.  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  소프트웨어만  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 이러한 값에 대 한 데이터를 1로 설정 하 고 파일을 시스템에 복사 합니다. 구성 요소가 다시 설치 되 면 설치 프로그램 또는 설치 관리자 DLL이 사용 횟수를 증가 시킵니다. 구성 요소가 제거 되 면 설치 프로그램 또는 설치 관리자 DLL이 사용 횟수를 감소 시킵니다. 사용 횟수가 0이 되 면 설치 프로그램 또는 설치 관리자 DLL이 파일에 대 한 값을 제거 하 고, 구성 요소가 드라이버 또는 변환기 인 경우 파일을 삭제 합니다. 드라이버 관리자 파일을 삭제 하면 안 됩니다.  
  
 파일 사용 횟수 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|data|  
|----------|---------------|----------|  
|*전체 경로*|REG_DWORD|*count*|  
  
 예를 들어 Informix에 대 한 드라이버에서 Infrmx32 및 Infrmx32 파일을 사용 하 고이 드라이버가 두 번 설치 되었다고 가정 합니다. Informix 드라이버의 SharedDlls 하위 키 아래에 있는 값은 다음과 같습니다.  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
