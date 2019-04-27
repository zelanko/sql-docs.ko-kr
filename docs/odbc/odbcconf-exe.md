---
title: ODBCCONF 합니다. EXE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33688a46be5e5e33aa940f3553c98db5091b159d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62677378"
---
# <a name="odbcconfexe"></a>ODBCCONF 합니다. EXE
ODBCCONF.exe는 ODBC 드라이버 및 데이터 원본 이름을 구성할 수 있는 명령줄 도구입니다.  
  
> [!NOTE]  
>  ODBCCONF.exe는 Windows Data Access Components의 이후 버전에서 제거 됩니다. 이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버 및 데이터 원본을 관리할 PowerShell 명령을 사용할 수 있습니다. 다음 PowerShell 명령에 대 한 자세한 내용은 참조 하세요. [Windows Data Access Components cmdlet](https://technet.microsoft.com/library/hh771019.aspx)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>인수  
 *switches*  
 0 개 이상의 스위치 옵션입니다. 사용할 수 있는 스위치의 목록에 대 한이 항목의 뒷부분에 나오는 주의 섹션을 참조 하세요.  
  
 *action*  
 하나의 수행할 작업입니다. 사용 가능한 옵션 목록에 대 한 설명 섹션을 참조 합니다.  
  
## <a name="remarks"></a>Remarks  
 다음 스위치를 사용할 수 있습니다.  
  
|스위치|Description|  
|------------|-----------------|  
|/A {*action*}|작업을 지정 합니다.<br /><br /> / A만 하나의 동작을 지정 하는 경우 선택 사항입니다.|  
|/?|ODBCCONF에 대 한 사용량을 표시 합니다. EXE 수 있습니다.|  
|/C|처리는 작업이 실패 하는 경우 계속 합니다.|  
|/E|처리가 완료 되 면 /F를 사용 하 여 지정 된 응답 파일을 지웁니다.|  
|/F|와 같은 응답 파일을 사용 하 여 `odbcconf /F my.rsp`입니다.<br /><br /> my.rsp이 같습니다. `REGSVR c:\my.dll`<br /><br /> / A 지시 파일에서 사용 되지 않습니다.|  
|/H|사용량 (도움말)를 표시 합니다. 이 스위치는 동일 /?|  
|/L[*mode*] *filename*|프로그램 출력 파일에 세 가지 모드 중 하나을 보낼: 보통 (n), 자세한 정보 (v) 및 디버그 (d). 모드 레코드 odbcconf.exe에서 로드 되는 Dll을 디버그 합니다.<br /><br /> /L 없이 모드를 지정 하는 경우 로그 파일이 비어 있게 됩니다.<br /><br /> 예를 들어 **/Lv log.txt**합니다.|  
|/R|작업을 다시 부팅 한 후 수행 됩니다.|  
|/S|자동 모드입니다. 오류 메시지를 표시 하지 않습니다.|  
  
 다음 작업을 사용할 수 있습니다.  
  
|작업|Description|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name * * 드라이버 관련 구성 매개 변수*|적절 한 드라이버 설치 DLL 및 호출을 로드 합니다 **ConfigDriver** 함수입니다.<br /><br /> 에 해당 하는 [SQLConfigDriver 함수](../odbc/reference/syntax/sqlconfigdriver-function.md)합니다.<br /><br /> 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.<br /><br /> / A {CONFIGDRIVER "드라이버 이름" "CPTimeout 60 ="}<br /><br /> /A {CONFIGDRIVER " Driver Name" "DriverODBCVer=03.80"}|  
|CONFIGDSN *driver_name* DSN =*이름* &#124; *특성*|추가 하거나 시스템 데이터 원본을 수정 합니다.<br /><br /> 에 해당 하는 [SQLConfigDataSource 함수](../odbc/reference/syntax/sqlconfigdatasource-function.md)합니다.<br /><br /> 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.<br /><br /> /A {CONFIGDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|CONFIGSYSDSN *driver_name* DSN =*이름* &#124; *특성*|추가 하거나 시스템 데이터 원본을 수정 합니다.<br /><br /> 에 해당 하는 [SQLConfigDataSource 함수](../odbc/reference/syntax/sqlconfigdatasource-function.md)합니다.<br /><br /> 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|INSTALLDRIVER|같음 [SQLInstallDriverEx 함수](../odbc/reference/syntax/sqlinstalldriverex-function.md)합니다.<br /><br /> INSTALLDRIVER에 전달 된 키워드-값 쌍 구문에 대 한 자세한 내용은 [드라이버 사양 하위 키](../odbc/reference/install/driver-specification-subkeys.md)합니다.<br /><br /> 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.<br /><br /> /A {INSTALLDRIVER  "Your Driver &#124; Driver=c:\your.dll &#124; Setup=c:\your.dll &#124; APILevel=2 &#124; ConnectFunctions=YYY &#124; DriverODBCVer=03.50 &#124; FileUsage=0 &#124; SQLLevel=1"}|  
|INSTALLTRANSLATOR *translator 구성 * * 드라이버 경로*|변환기에 대 한 정보 추가 **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST 합니다. INI\ODBC 변환기** 레지스트리 키입니다.<br /><br /> 같음 [SQLInstallTranslatorEx 함수](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)합니다.<br /><br /> INSTALLDRIVER에 전달 된 키워드-값 쌍 구문에 대 한 자세한 내용은 [변환기 사양 서브 키](../odbc/reference/install/translator-specification-subkeys.md)합니다.<br /><br /> 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.<br /><br /> /A {INSTALLTRANSLATOR  "My Translator &#124; Translator=c:\my.dll &#124; Setup=c:\my.dll"}|  
|REGSVR *dll*|DLL을 등록합니다.<br /><br /> Regsvr32.exe에 해당 합니다.<br /><br /> 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|때 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC 합니다. INI\ODBC 파일 DSN\DefaultDSNDir 존재 하지 않는, SETFILEDSNDIR 작업을 만들 되며 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir, \ODBC\Data 원본과 추가 값을 할당 합니다.<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC 값입니다. INI\ODBC 파일 DSN\DefaultDSNDir ODBC 데이터 원본 관리자에서 파일 기반 데이터 원본을 만들 때 사용할 기본 위치를 지정 합니다.<br /><br /> 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.<br /><br /> {SETFILEDSNDIR} / A|  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft ODBC(Open Database Connectivity)](../odbc/microsoft-open-database-connectivity-odbc.md)
