---
description: ODBCCONF.EXE
title: ODBCCONF.EXE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4f4af809044a46fd6df8c45c77cf1d3a7929226
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471258"
---
# <a name="odbcconfexe"></a>ODBCCONF.EXE
ODBCCONF.exe는 ODBC 드라이버 및 데이터 원본 이름을 구성 하는 데 사용할 수 있는 명령줄 도구입니다.  
  
> [!NOTE]  
>  ODBCCONF.exe는 이후 버전의 Windows Data Access 구성 요소에서 제거 될 예정입니다. 이 기능을 사용 하지 말고, 현재이 기능을 사용 하는 응용 프로그램을 수정 하십시오. PowerShell 명령을 사용 하 여 드라이버 및 데이터 원본을 관리할 수 있습니다. 이러한 PowerShell 명령에 대 한 자세한 내용은 [Windows Data Access Components cmdlet](/powershell/module/wdac)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>인수  
 *스위치*  
 0 개 이상의 스위치 옵션입니다. 사용 가능한 스위치 목록은이 항목의 뒷부분에 나오는 주의 섹션을 참조 하십시오.  
  
 *action*  
 수행할 작업 하나입니다. 사용할 수 있는 옵션 목록은 설명 섹션을 참조 하세요.  
  
## <a name="remarks"></a>설명  
 다음 스위치를 사용할 수 있습니다.  
  
|스위치|Description|  
|------------|-----------------|  
|/A {*action*}|작업을 지정 합니다.<br /><br /> 하나의 동작만 지정 된 경우/a는 선택 사항입니다.|  
|/?|ODBCCONF.EXE에 대 한 사용법을 표시 합니다.|  
|/C|작업이 실패 하면 처리가 계속 됩니다.|  
|/E|처리가 완료 되 면/F로 지정 된 지시 파일을 지웁니다.|  
|/F|등의 지시 파일을 사용 `odbcconf /F my.rsp` 합니다.<br /><br /> my.user는 다음과 같습니다. `REGSVR c:\my.dll`<br /><br /> /A는 지시 파일에서 사용 되지 않습니다.|  
|/H|사용법 (도움말)을 표시 합니다. 이 스위치는/?와 동일 합니다.|  
|/L [*모드*] *파일 이름*|일반 (n), 자세한 정보 표시 (v) 및 디버그 (d)의 세 가지 모드 중 하나로 프로그램 출력을 파일로 보냅니다. 디버그 모드는 odbcconf.exe에서 로드 한 Dll을 기록 합니다.<br /><br /> 모드 없이/L을 지정 하면 로그 파일이 비어 있게 됩니다.<br /><br /> 예를 들어 **/Lv log.txt**합니다.|  
|/R|작업은 다시 부팅 한 후에 수행 됩니다.|  
|/S|자동 모드. 오류 메시지를 표시 하지 않습니다.|  
  
 사용할 수 있는 작업은 다음과 같습니다.  
  
|작업|설명|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name * * 드라이버별 구성 매개 변수*|적절 한 드라이버 설치 DLL을 로드 하 고 **Configdriver** 함수를 호출 합니다.<br /><br /> [SQLConfigDriver 함수와](../odbc/reference/syntax/sqlconfigdriver-function.md)동일 합니다.<br /><br /> 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> /A {CONFIGDRIVER "드라이버 이름" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "드라이버 이름" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *driver_name* DSN =*이름* &#124; *특성*|시스템 데이터 원본을 추가 하거나 수정 합니다.<br /><br /> [SQLConfigDataSource 함수와](../odbc/reference/syntax/sqlconfigdatasource-function.md)동일 합니다.<br /><br /> 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> /A {CONFIGDSN "SQL Server" "DSN = name &#124; Server = srv"}|  
|CONFIGSYSDSN *driver_name* dsn =*name* &#124; *특성*|시스템 데이터 원본을 추가 하거나 수정 합니다.<br /><br /> [SQLConfigDataSource 함수와](../odbc/reference/syntax/sqlconfigdatasource-function.md)동일 합니다.<br /><br /> 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN = name &#124; Server = srv"}|  
|INSTALLDRIVER|[Sqlinstalldriverex 함수와](../odbc/reference/syntax/sqlinstalldriverex-function.md)동일 합니다.<br /><br /> INSTALLDRIVER에 전달 된 키워드-값 쌍 구문에 대 한 자세한 내용은 [드라이버 사양 하위 키](../odbc/reference/install/driver-specification-subkeys.md)를 참조 하세요.<br /><br /> 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> /A {INSTALLDRIVER "드라이버 &#124; Driver =c:\your.dll &#124; Setup =c:\your.dll &#124; APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; FileUsage = 0 &#124; SQLLevel = 1"}|  
|INSTALLTRANSLATOR *변환기 구성 * * 드라이버 경로*|**HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI \ODBC 번역기** 레지스트리 키에 변환기에 대 한 정보를 추가 합니다.<br /><br /> [SQLInstallTranslatorEx 함수](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)에 해당 합니다.<br /><br /> INSTALLDRIVER에 전달 된 키워드-값 쌍 구문에 대 한 자세한 내용은 [Translator 사양 하위 키](../odbc/reference/install/translator-specification-subkeys.md)를 참조 하세요.<br /><br /> 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> /A {INSTALLTRANSLATOR "My Translator &#124; Translator =c:\my.dll &#124; Setup =c:\my.dll"}|  
|REGSVR *dll*|DLL을 등록 합니다.<br /><br /> regsvr32.exe와 동일 합니다.<br /><br /> 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> /A {REGSVR}|  
|SETFILEDSNDIR|HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI \ODBC 파일 DSN\DefaultDSNDir이 없으면 SETFILEDSNDIR 작업에서 \ODBC\Data 원본과 함께 추가 된 \SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir HKEY_LOCAL_MACHINE에 값을 할당 하 여 값을 할당 합니다.<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI \ODBC 파일 DSN\DefaultDSNDir의 값은 파일 기반 데이터 원본을 만들 때 ODBC 데이터 원본 관리자가 사용 하는 기본 위치를 지정 합니다.<br /><br /> 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft ODBC(Open Database Connectivity)](../odbc/microsoft-open-database-connectivity-odbc.md)
