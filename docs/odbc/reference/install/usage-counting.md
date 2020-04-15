---
title: 사용량 계산 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d516a591bfde47522c0ccfe08bd2bd706218e07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296023"
---
# <a name="usage-counting"></a>사용량 계산
> [!NOTE]  
>  Windows XP 및 Windows 서버 2003을 시작으로 ODBC는 Windows 운영 체제에 포함되어 있습니다. 이전 버전의 Windows에서는 ODBC만 명시적으로 설치해야 합니다.  
  
 각 구성 요소에 대한 레지스트리에는 구성 요소 사용 횟수와 하나 이상의 선택적 파일 사용 수의 두 가지 유형의 사용 수가 유지됩니다. 구성 요소 사용 수는 설치 관리자 DLL이 레지스트리 항목을 유지하는 데 도움이 됩니다. ODBC 코어, 드라이버 및 번역기 하위 키 아래의 UsageCount 값에 저장됩니다. UsageCount 값의 형식과 이러한 하위 키에 대한 자세한 내용은 [ODBC 구성 요소에 대한 레지스트리 항목을](../../../odbc/reference/install/registry-entries-for-odbc-components.md)참조하십시오.  
  
 구성 요소를 처음 설치하면 설치 관리자 DLL은 해당 하위 키에 대한 하위 키를 만들고 해당 하위 키의 UsageCount 값에 대한 데이터를 1로 설정합니다. 구성 요소를 다시 설치하면 설치 관리자 DLL이 사용량 수를 증가시입니다. 구성 요소를 제거하면 설치 관리자 DLL이 사용 횟수를 줄입니다. 사용 수가 0으로 떨어지면 설치 관리자 DLL은 구성 요소의 하위 키를 제거합니다.  
  
> [!CAUTION]  
>  구성 요소 사용량 이 수와 파일 사용 수가 0에 도달하면 응용 프로그램이 Driver Manager 파일을 물리적으로 제거해서는 안 됩니다.  
  
 파일 사용 수는 사용 횟수를 증가하거나 감소시키는 것이 아니라 파일을 실제로 복사하거나 삭제해야 하는 시기를 결정하는 데 도움이 됩니다. ODBC 구성 요소와 ODBC 구성 요소의 파일이 공유되고 다양한 응용 프로그램에서 설치하거나 제거할 수 있기 때문에 이는 중요합니다. 구성 요소 사용량 이 수와 파일 사용량 수가 0에 도달하면 응용 프로그램은 드라이버 및 번역기 파일을 삭제할 수 있습니다. 그러나 이러한 파일은 파일 사용 수를 증가시키지 않은 다른 응용 프로그램에서 사용할 수 있으므로 구성 요소 사용 수와 파일 사용 수가 모두 0에 도달하면 드라이버 관리자 파일을 삭제하면 안 됩니다.  
  
> [!NOTE]  
>  파일 사용 수는 마이크로소프트® WindowsNT®/Windows2000에서 선택 사항입니다.  
  
 파일 사용 수는 **SQLInstallDriverManager,** **SQLInstallDriverEx,** **SQLInstallTranslatorEx,** **SQLRemoveDriverManager,** **SQLRemoveDriverDriver, SQLRemoveDriver**또는 **SQLRemoveTranslator**를 호출 한 후 설치 프로그램에서 유지 관리됩니다.  
  
 구성 요소를 처음 설치하면 설치 프로그램 또는 설치 관리자 DLL은 시스템에 아직 없는 해당 구성 요소의 각 파일에 대해 다음 키 아래에 값을 만듭니다.  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  소프트웨어  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  공유 Dlls  
  
 해당 값에 대한 데이터를 1로 설정하고 파일을 시스템에 복사합니다. 구성 요소를 다시 설치하면 설치 프로그램 또는 설치 프로그램 DLL이 사용량을 증가시게 됩니다. 구성 요소를 제거하면 설치 프로그램 또는 설치 프로그램 DLL이 사용량 수를 줄입니다. 사용량 수가 0으로 떨어지면 설치 프로그램 또는 설치 관리자 DLL은 파일값을 제거하고 구성 요소가 드라이버 또는 번역자인 경우 파일을 삭제합니다. 드라이버 관리자 파일을 삭제하면 안 됩니다.  
  
 파일 사용 수 개 수 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|*전체 경로*|REG_DWORD|*count*|  
  
 예를 들어 Informix의 드라이버가 Infrmx32.dll 및 Infrmx32.hlp 파일을 사용하고 이 드라이버가 두 번 설치되었다고 가정합니다. Informix 드라이버의 SharedDlls 하위 키 아래의 값은 다음과 같습니다.  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
