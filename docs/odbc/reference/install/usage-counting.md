---
title: "사용 현황 계산 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f9db5a35b8b0bb3dc437dd203267c6f53825e22
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="usage-counting"></a>사용 현황 계산
> [!NOTE]  
>  Windows XP 및 Windows Server 2003부터 ODBC Windows 운영 체제에 포함 됩니다. 이전 버전의 Windows에서 ODBC만 명시적으로 설치 해야 합니다.  
  
 두 가지 유형의 사용 횟수는 각 구성 요소에 대 한 레지스트리에 유지 됩니다: 구성 요소는 사용 카운트 및 하나 이상의 선택적 파일 사용 횟수입니다. 구성 요소 사용 횟수 설치 관리자를 사용 하면 DLL 레지스트리 항목을 유지 합니다. ODBC 핵심, 드라이버 및 변환기 하위 키 아래에 있는 UsageCount 값에 저장 됩니다. UsageCount 값 및 이러한 하위 키에 대 한 자세한 내용은 형식에 대 한 참조 [ODBC 구성 요소에 대 한 레지스트리 항목](../../../odbc/reference/install/registry-entries-for-odbc-components.md)합니다.  
  
 구성 요소를 처음 설치할 때 설치 관리자 DLL에 대 한 하위 키를 만든 및 해당 하위 키를 1에서 UsageCount 값에 대 한 데이터를 설정 합니다. 요소를 다시 설치, 설치 관리자 DLL 사용 횟수를 증가 시킵니다. 구성 요소가 제거 되는 설치 관리자 DLL 사용 횟수를 줄입니다. 사용 횟수를 0으로 뒤쳐지면 DLL 설치 관리자 구성 요소에 대 한 하위 키를 제거 합니다.  
  
> [!CAUTION]  
>  구성 요소 사용 수 및 파일 사용 횟수가 0에 도달 하면 응용 프로그램 파일 드라이버 관리자를 물리적으로 제거 하지 않아야 합니다.  
  
 파일 사용량 개수 결정할 때 파일을 실제로 복사 하거나 삭제 해야으로 반대로 증가 시키거나 감소 시키는 사용 횟수입니다. ODBC 구성 요소 및 ODBC 구성 요소에 있는 파일 공유 및 설치 하거나 제거할 수는 다양 한 응용 프로그램에서 때문에 유용 합니다. 응용 프로그램 구성 요소 사용 수 및 파일 사용 횟수가 0에 도달 하는 경우 드라이버 및 변환기 파일을 삭제할 수 있습니다. 그러나 드라이버 관리자 파일 되어서는 안, 이러한 파일을 파일 사용 횟수를 증가 있어야 하는 다른 응용 프로그램에서 사용할 수 있으므로 구성 요소 사용 수 및 파일 사용 횟수가 모두 0에 도달한 경우 삭제할 수 있습니다.  
  
> [!NOTE]  
>  파일 사용 횟수는 Microsoft® WindowsNT®/Windows2000 옵션입니다.  
  
 호출 후 파일 사용 횟수 설치 프로그램에서 유지 관리 **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**, 또는 **SQLRemoveTranslator**합니다.  
  
 구성 요소를 처음 설치할 때 설치 프로그램 또는 설치 관리자 DLL 수행 하면 각 파일에 대 한 다음 키 아래 시스템에 설치 되지 않은 해당 구성:  
  
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
>  하기 위해 SharedDlls  
  
 데이터에 해당 값을 1로 설정 하 고 시스템에는 파일을 복사 합니다. 구성 요소가 다시 설치 되 면 설치 프로그램 또는 DLL installer 사용 횟수를 증가 시킵니다. 구성 요소가 제거 되 면 설치 프로그램 또는 설치 관리자 DLL 감소의 사용량 계산 합니다. 사용 카운트를 0으로 뒤쳐지면 설치 프로그램 또는 설치 관리자 DLL 파일에 대 한 값을 제거 및, 경우에 드라이버 또는 변환기는 파일을 삭제 합니다. 드라이버 관리자 파일은 삭제 되지 않습니다.  
  
 파일 사용 count 값의 형식은 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|data|  
|----------|---------------|----------|  
|*전체 경로*|REG_DWORD|*count*|  
  
 이 드라이버가 두 번 설치 가정 고 Infrmx32.dll 및 Infrmx32.hlp 파일을 사용 하 여 Informix에 대 한 드라이버 가정 합니다. 예를 들어 합니다. Informix 드라이버에 대 한 하기 위해 SharedDlls 하위 키 아래에 값은 다음과 같이 합니다.  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```

