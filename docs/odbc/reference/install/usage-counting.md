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
manager: craigg
ms.openlocfilehash: ca2a52eb08cdf1b1b9cb5a23805da34aab915b7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273386"
---
# <a name="usage-counting"></a>사용량 계산
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC를 명시적으로 설치 해야 합니다.  
  
 두 가지 유형의 사용 횟수는 각 구성 요소에 대 한 레지스트리에 유지 됩니다: 구성 요소 사용 횟수 및 하나 이상의 선택적 파일 사용 횟수입니다. 구성 요소 사용 횟수 설치 관리자를 사용 하면 DLL 레지스트리 항목을 유지 합니다. ODBC 핵심, 드라이버 및 변환기 하위 키 아래 UsageCount 값에 저장 됩니다. 형식 UsageCount 값 및 이러한 하위 키에 대 한 자세한 내용은 참조 하세요 [ODBC 구성 요소에 대 한 레지스트리 항목](../../../odbc/reference/install/registry-entries-for-odbc-components.md)합니다.  
  
 구성 요소를 처음 설치 하면 설치 관리자 DLL 하위 키를 만들고 설정 UsageCount 값의 데이터를 해당 하위 키를 1에서 합니다. 구성 요소를 다시 설치 하는 경우 설치 관리자 DLL 사용 횟수를 증가 시킵니다. 구성 요소가 제거 되는 설치 관리자 DLL 사용 횟수를 줄입니다. 사용 횟수를 0으로 떨어지면 설치 관리자 DLL 구성 요소에 대 한 하위 키를 제거 합니다.  
  
> [!CAUTION]  
>  구성 요소 사용 횟수 및 파일 사용 횟수가 0에 도달 하면 응용 프로그램 드라이버 관리자 파일을 물리적으로 제거 되지 해야 합니다.  
  
 개수 경우 파일을 실제로 복사 하거나 삭제 해야으로 확인 하는 데 도움이 되는 파일 사용과는 반대로 증가 시키거나 감소 시키는 사용 횟수입니다. 이 ODBC 구성 요소 및 ODBC 구성 요소에서 파일 공유 및 설치 하거나 제거할 수 다양 한 응용 프로그램에서 중요 합니다. 응용 프로그램 구성 요소 사용 횟수 및 파일 사용 횟수가 0에 도달 하는 경우 드라이버 및 translator 파일을 삭제할 수 있습니다. 하지만 드라이버 관리자 파일 안, 파일 사용 횟수를 증가 있어야 하는 다른 응용 프로그램에서 이러한 파일을 사용할 수 있으므로 구성 요소 사용 횟수 및 파일 사용 횟수가 0에 도달한 경우 삭제할 수 있습니다.  
  
> [!NOTE]  
>  파일 사용 횟수는 Microsoft® WindowsNT®/Windows2000 선택적입니다.  
  
 파일 사용 횟수 호출한 후 설치 프로그램에서 유지 됩니다 **SQLInstallDriverManager**를 **SQLInstallDriverEx**하십시오 **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**하십시오 **SQLRemoveDriver**, 또는 **SQLRemoveTranslator**합니다.  
  
 구성 요소를 처음 설치 하면 설치 프로그램 또는 설치 관리자를 DLL 수행 하면 각 파일에 대 한 다음 키 아래 시스템에 없는 구성 요소:  
  
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
>  SharedDlls  
  
 이러한 값에 대 한 데이터를 1로 설정 하 고 파일 시스템에 복사 합니다. 구성 요소를 다시 설치 하는 경우 설치 프로그램 또는 설치 관리자 DLL 사용 횟수를 증가 시킵니다. 구성 요소가 제거 되 면 설치 프로그램 또는 설치 관리자 DLL 감소 사용량을 계산 합니다. 모든 사용 횟수가 0으로 떨어지면 설치 프로그램 또는 설치 관리자 DLL 파일에 대 한 값을 제거 및, 드라이버 또는 변환기를 해당 구성 요소가 파일을 삭제 합니다. 드라이버 관리자 파일은 삭제 되지 않습니다.  
  
 파일 사용량 count 값의 형식은 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|data|  
|----------|---------------|----------|  
|*full-path*|REG_DWORD|*count*|  
  
 예를 들어, Informix 드라이버 Infrmx32.dll 및 Infrmx32.hlp 파일을 사용 한다고 가정 및이 드라이버 두 번 설치 되어 있는지 가정 합니다. Informix 드라이버용 하기 위해 SharedDlls 하위 키 아래의 값은 다음과 같을 수: 있습니다.  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
