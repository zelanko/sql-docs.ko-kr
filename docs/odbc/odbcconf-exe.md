---
title: ODBCCONF. EXE | 마이크로 소프트 문서
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
ms.openlocfilehash: d771f01d292312f8a0f0060c16e3c348bf2e009e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307534"
---
# <a name="odbcconfexe"></a>ODBCCONF. Exe
ODBCCONF.exe는 ODBC 드라이버 및 데이터 원본 이름을 구성할 수 있는 명령줄 도구입니다.  
  
> [!NOTE]  
>  ODBCCONF.exe는 이후 버전의 Windows 데이터 액세스 구성 요소에서 제거됩니다. 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. PowerShell 명령을 사용하여 드라이버 및 데이터 원본을 관리할 수 있습니다. 이러한 PowerShell 명령에 대한 자세한 내용은 [Windows 데이터 액세스 구성 요소 cmdlet](/powershell/module/wdac)을 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>인수  
 *스위치*  
 0 개 이상의 스위치 옵션. 사용 가능한 스위치 목록은 이 항목의 후반부에서 비고 섹션을 참조하십시오.  
  
 *작업*  
 수행할 작업 중 하나. 사용 가능한 옵션 목록은 비고 섹션을 참조하십시오.  
  
## <a name="remarks"></a>설명  
 다음 스위치를 사용할 수 있습니다.  
  
|스위치|설명|  
|------------|-----------------|  
|/A {*액션*}|작업을 지정합니다.<br /><br /> /A는 하나의 작업만 지정하면 선택 사항입니다.|  
|/?|ODBCCONF에 대한 디스플레이 사용량. Exe.|  
|/C|작업이 실패하면 처리가 계속됩니다.|  
|/E|처리가 완료되면 /F로 지정된 응답 파일을 지웁습니다.|  
|/F|와 같은 `odbcconf /F my.rsp`응답 파일을 사용합니다.<br /><br /> my.rsp는 다음과 같이 보일 수 있습니다.`REGSVR c:\my.dll`<br /><br /> /A는 응답 파일에 사용되지 않습니다.|  
|/H|사용(도움말)을 표시합니다. 이 스위치는 /?와 동일합니다.|  
|/L[*모드]* *파일 이름*|프로그램 출력을 일반(n), 자세한 내용(v) 및 디버그(d) 중 하나의 세 가지 모드 중 하나로 파일에 보냅니다. 디버그 모드는 odbcconf.exe에 의해 로드된 DLL을 기록합니다.<br /><br /> 모드 없이 /L을 지정하면 로그 파일이 비어 있습니다.<br /><br /> 예를 **들어/Lv log.txt**.|  
|/R|작업은 재부팅 후 수행됩니다.|  
|/S|자동 모드. 오류 메시지를 표시하지 마십시오.|  
  
 사용할 수 있는 작업은 다음과 같습니다.  
  
|작업|설명|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name**드라이버별 구성 매개 변수*|적절한 드라이버 설정 DLL을 로드하고 **ConfigDriver** 함수를 호출합니다.<br /><br /> [SQLConfigDriver 함수와](../odbc/reference/syntax/sqlconfigdriver-function.md)동일합니다.<br /><br /> 다음은 그 예입니다.<br /><br /> /A {CONFIGDRIVER "드라이버 이름" "CPTimeout=60"}<br /><br /> /A {CONFIGDRIVER "드라이버 이름" "DriverODBCVer=03.80"}|  
|CONFIGDSN *driver_name* DSN=*이름* &#124; *특성*|시스템 데이터 원본을 추가하거나 수정합니다.<br /><br /> [SQLConfigDataSource 함수와](../odbc/reference/syntax/sqlconfigdatasource-function.md)동일합니다.<br /><br /> 다음은 그 예입니다.<br /><br /> /{CONFIGDSN "SQL 서버" "DSN=이름 &#124; 서버=srv"}|  
|CONFIGSYSDSN *driver_name* DSN=*이름* &#124; *특성*|시스템 데이터 원본을 추가하거나 수정합니다.<br /><br /> [SQLConfigDataSource 함수와](../odbc/reference/syntax/sqlconfigdatasource-function.md)동일합니다.<br /><br /> 다음은 그 예입니다.<br /><br /> /a {CONFIGSYSDSN "SQL 서버" "DSN=이름 &#124; 서버=srv"}|  
|설치 드라이버|[SQLInstallDriverEx 함수와](../odbc/reference/syntax/sqlinstalldriverex-function.md)동일합니다.<br /><br /> INSTALLDRIVER에 전달된 키워드-값 쌍 구문에 대한 자세한 내용은 [드라이버 사양 하위 키를](../odbc/reference/install/driver-specification-subkeys.md)참조하십시오.<br /><br /> 다음은 그 예입니다.<br /><br /> /A {INSTALLDRIVER "드라이버 &#124; 드라이버=c:\your.dll &#124; 설치=c:\your.dll &#124; APILevel=2 &#124; ConnectFunctions=YYY &#124; DriverODBCVer=03.50 &#124; 파일 사용=0 &#124; SQLLevel=1"}|  
|설치 번역기 *번역기 구성**드라이버 경로*|**HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST에 번역기에 대한 정보를 추가합니다. INI\ODBC 번역기** 레지스트리 키입니다.<br /><br /> [SQLInstallTranslatorEx 함수에](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)해당합니다.<br /><br /> INSTALLDRIVER에 전달된 키워드-값 쌍 구문에 대한 자세한 내용은 [번역기 사양 하위 키를](../odbc/reference/install/translator-specification-subkeys.md)참조하십시오.<br /><br /> 다음은 그 예입니다.<br /><br /> /A {INSTALLTRANSLATOR "내 번역기 &#124; 번역기 =c:\my.dll &#124; 설치=c:\my.dll"}|  
|REGSVR *dll*|DLL을 등록합니다.<br /><br /> regsvr32.exe에 해당합니다.<br /><br /> 다음은 그 예입니다.<br /><br /> /A {REGSVR c:\my.dll}|  
|셋파일드스디르|HKEY_LOCAL_MACHINE 때\소프트웨어\ODBC\ODBC. INI\ODBC 파일 DSN\DefaultDSNDir이 존재하지 않는 경우, SETFILEDSNDIR 작업이 생성되어 \SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir에서 HKEY_LOCAL_MACHINE 값을 할당하고 \ODBC\데이터 소스와 함께 추가됩니다.<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC의 값입니다. INI\ODBC 파일 DSN\DefaultDSNDir은 파일 기반 데이터 원본을 만들 때 ODBC 데이터 원본 관리자가 사용하는 기본 위치를 지정합니다.<br /><br /> 다음은 그 예입니다.<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft ODBC(Open Database Connectivity)](../odbc/microsoft-open-database-connectivity-odbc.md)
