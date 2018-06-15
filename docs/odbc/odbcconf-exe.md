---
title: ODBCCONF 합니다. EXE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f7a6e48f6a7a17c8ea3decd79d765fb176080e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914308"
---
# <a name="odbcconfexe"></a>ODBCCONF 합니다. EXE
ODBCCONF.exe는 ODBC 드라이버 및 데이터 원본 이름을 구성할 수 있는 명령줄 도구입니다.  
  
> [!NOTE]  
>  ODBCCONF.exe는 Windows Data Access Components의 이후 버전에서 제거 됩니다. 이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버 및 데이터 원본을 관리 하는 PowerShell 명령을 사용할 수 있습니다. 이러한 PowerShell 명령에 대 한 자세한 내용은 참조 [Windows Data Access Components cmdlet](https://technet.microsoft.com/library/hh771019.aspx)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>인수  
 *스위치*  
 0 개 이상의 스위치 옵션입니다. 사용할 수 있는 스위치의 목록을 보려면이 항목의 뒷부분에 나오는 주의 섹션을 참조 합니다.  
  
 *action*  
 하나의 수행할 동작입니다. 사용 가능한 옵션 목록에 대 한 설명 섹션을 참조 합니다.  
  
## <a name="remarks"></a>주의  
 다음 스위치를 사용할 수 있습니다.  
  
|스위치|Description|  
|------------|-----------------|  
|/A {*동작*}|작업을 지정 합니다.<br /><br /> /A 하나만 하나의 동작을 지정 하는 경우 선택 사항입니다.|  
|/?|ODBCCONF 사용 현황이 표시 됩니다. EXE 합니다.|  
|/C|작업이 실패 하는 경우 수행 됩니다.|  
|/E|처리가 완료 될 때 /F로 지정 된 지시 파일을 지웁니다.|  
|/F|와 같은 응답 파일을 사용 하 여 `odbcconf /F my.rsp`합니다.<br /><br /> my.rsp 다음과 같이 표시 될 수 있습니다. `REGSVR c:\my.dll`<br /><br /> /A 지시 파일에서 사용 되지 않습니다.|  
|/H|사용 현황 (도움말)을 표시 합니다. 이 스위치는 동일 /?.|  
|/ L [*모드*] *파일 이름*|프로그램 출력 세 가지 모드 중 하나에 있는 파일을 보낼: 보통 (n), 자세한 정보 (v) 및 디버그 (d). 모드 레코드 odbcconf.exe에서 로드 되는 Dll을 디버깅 합니다.<br /><br /> 모드를 하지 않고 /L을 지정 하면 로그 파일이 비어 있게 됩니다.<br /><br /> 예를 들어 **/Lv log.txt**합니다.|  
|/R|다시 부팅 한 후 작업을 수행 됩니다.|  
|/S|자동 모드입니다. 오류 메시지를 표시 하지 않습니다.|  
  
 다음 작업을 사용할 수 있습니다.  
  
|동작|Description|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name * * 드라이버 관련 구성 매개 변수*|적절 한 드라이버 설치 DLL 및 호출 로드는 **ConfigDriver** 함수입니다.<br /><br /> 에 해당 하는 [SQLConfigDriver 함수](../odbc/reference/syntax/sqlconfigdriver-function.md)합니다.<br /><br /> 예를 들어:<br /><br /> /A {CONFIGDRIVER "드라이버 이름" "CPTimeout = 60"을 (를)<br /><br /> /A {"드라이버 이름" CONFIGDRIVER "DriverODBCVer 03.80 ="을 (를)|  
|CONFIGDSN *driver_name* DSN =*이름* &#124; *특성*|추가 하거나 시스템 데이터 원본을 수정 합니다.<br /><br /> 에 해당 하는 [SQLConfigDataSource 함수](../odbc/reference/syntax/sqlconfigdatasource-function.md)합니다.<br /><br /> 예를 들어:<br /><br /> /A {"SQL Server" CONFIGDSN "DSN = 이름 &#124; 서버 srv ="을 (를)|  
|CONFIGSYSDSN *driver_name* DSN =*이름* &#124; *특성*|추가 하거나 시스템 데이터 원본을 수정 합니다.<br /><br /> 에 해당 하는 [SQLConfigDataSource 함수](../odbc/reference/syntax/sqlconfigdatasource-function.md)합니다.<br /><br /> 예를 들어:<br /><br /> /A {"SQL Server" CONFIGSYSDSN "DSN = 이름 &#124; 서버 srv ="을 (를)|  
|INSTALLDRIVER|에 해당 [SQLInstallDriverEx 함수](../odbc/reference/syntax/sqlinstalldriverex-function.md)합니다.<br /><br /> INSTALLDRIVER에 전달 된 키워드-값 쌍 구문에 대 한 정보를 참조 하십시오. [드라이버 사양 하위 키](../odbc/reference/install/driver-specification-subkeys.md)합니다.<br /><br /> 예를 들어:<br /><br /> /A {INSTALLDRIVER "드라이버 &#124; Driver=c:\your.dll &#124; Setup=c:\your.dll &#124; APILevel = 2 &#124; ConnectFunctions YYY = &#124; DriverODBCVer 03.50 = &#124; FileUsage = 0 &#124; SQLLevel = 1"을 (를)|  
|INSTALLTRANSLATOR *변환기 구성 * * 드라이버 경로*|추가 하는 변환기에 대 한 정보는 **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST 합니다. INI\ODBC 변환기** 레지스트리 키입니다.<br /><br /> 에 해당 [SQLInstallTranslatorEx 함수](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)합니다.<br /><br /> INSTALLDRIVER에 전달 된 키워드-값 쌍 구문에 대 한 정보를 참조 하십시오. [변환기 사양 하위 키](../odbc/reference/install/translator-specification-subkeys.md)합니다.<br /><br /> 예를 들어:<br /><br /> /A {INSTALLTRANSLATOR "내 변환기 &#124; Translator=c:\my.dll &#124; Setup=c:\my.dll"을 (를)|  
|REGSVR *dll*|DLL을 등록합니다.<br /><br /> Regsvr32.exe와 동일 합니다.<br /><br /> 예를 들어:<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|때 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC 합니다. INI\ODBC 파일 DSN\DefaultDSNDir 존재 하지 않는, SETFILEDSNDIR 작업은 만들고 \ODBC\Data 원본과 추가 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir에 값을 할당 합니다.<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC 값입니다. INI\ODBC 파일 DSN\DefaultDSNDir 파일 기반 데이터 원본을 만들 때는 ODBC 데이터 원본 관리자에서 사용 되는 기본 위치를 지정 합니다.<br /><br /> 예를 들어:<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft ODBC(Open Database Connectivity)](../odbc/microsoft-open-database-connectivity-odbc.md)
