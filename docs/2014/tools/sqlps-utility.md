---
title: sqlps 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqlps utility
- PowerShell [SQL Server], sqlps utility
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b25921a7b48ecd818527dd95ebc2d8714cb6871d
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241513"
---
# <a name="sqlps-utility"></a>sqlps 유틸리티
  `sqlps` 유틸리티는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 공급자와 cmdlet이 로드 및 등록된 Windows PowerShell 2.0 세션을 시작합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 구성 요소를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 및 해당 개체와 함께 작동하는 PowerShell 명령 또는 스크립트를 입력할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] 대신 `sqlps` PowerShell 모듈을 사용하십시오. 에 대 한 자세한 내용은 합니다 `sqlps` 모듈을 참조 하세요 [SQLPS 모듈 가져오기](../database-engine/import-the-sqlps-module.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
      sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -argsargument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## <a name="arguments"></a>인수  
 **-NoLogo**  
 `sqlps` 유틸리티가 시작될 때 저작권 배너를 표시하지 않도록 지정합니다.  
  
 **-NoExit**  
 시작 명령이 완료된 후에도 `sqlps` 유틸리티가 계속 실행되도록 지정합니다.  
  
 **-NoProfile**  
 `sqlps` 유틸리티가 사용자 프로필을 로드하지 않도록 지정합니다. 사용자 프로필은 PowerShell 세션에서 사용하도록 공통적으로 사용되는 별칭, 함수 및 변수를 기록합니다.  
  
 **-OutPutFormat** { **Text** | **XML** }  
 지정 된 `sqlps` 유틸리티 출력 형식이 텍스트 문자열 수 (**텍스트**) 또는 직렬화 된 CLIXML 형식에서 (**XML**).  
  
 **-InPutFormat** { **Text** | **XML** }  
 입력을 지정 합니다 `sqlps` 유틸리티는 형식이 텍스트 문자열 (**텍스트**) 또는 직렬화 된 CLIXML 형식에서 (**XML**).  
  
 **-Command**  
 `sqlps` 유틸리티에 대한 명령이 실행되도록 지정합니다. 합니다 `sqlps` 유틸리티가 명령을 실행 한 다음 종료 하지 않는 한 **-NoExit** 도 지정 합니다. **-Command**뒤에는 다른 스위치를 지정하지 마세요. 이 경우 스위치가 명령 매개 변수로 읽힙니다.  
  
 **-**  
 **-Command-** 지정 된 `sqlps` 유틸리티가 표준 입력 으로부터 입력을 읽어서 합니다.  
  
 *script_block* [ **-args**_argument_array_ ]  
 실행할 PowerShell 명령 블록을 지정합니다. 명령 블록은 중괄호 {}로 묶어야 합니다. *Script_block* 때만 지정할 수는 `sqlps` 유틸리티에서 호출 된 **PowerShell** 또는 다른 `sqlps` 유틸리티 세션입니다. *argument_array* 는 *script_block*의 PowerShell 명령에 대한 인수를 포함하는 PowerShell 변수 배열입니다.  
  
 *string* [ *command_parameters* ]  
 실행할 PowerShell 명령을 포함하는 문자열을 지정합니다. 형식을 사용 하 여 **"& {*`command`*}"** 합니다. 큰따옴표는 문자열 및 호출 연산자 (&) 원인 나타내며는 `sqlps` 명령을 실행 하는 유틸리티입니다.  
  
 [ **-?** | **-Help** ]  
 `sqlps` 유틸리티 옵션의 구문 요약 정보를 표시합니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 `sqlps` 유틸리티는 PowerShell 환경 (PowerShell.exe) 시작 하 고 로드를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 모듈. 모듈을 라고도 `sqlps`, 로드 하 고 이러한 등록 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 스냅인:  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 공급자 및 **Encode-SqlName** , **Decode-SqlName**과 같은 관련 cmdlet을 구현합니다.  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     **Invoke-Sqlcmd** 및 **Invoke-PolicyEvaluation** cmdlet을 구현합니다.  
  
 다음과 같은 작업에 `sqlps` 유틸리티를 사용할 수 있습니다.  
  
-   대화형으로 PowerShell 명령을 실행합니다.  
  
-   PowerShell 스크립트 파일을 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet을 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자 경로를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체의 계층 구조를 탐색합니다.  
  
 기본적으로 `sqlps` 로 설정 된 스크립팅 실행 정책과 함께 실행 되는 유틸리티 **Restricted**합니다. 이는 모든 PowerShell 스크립트의 실행을 차단합니다. **Set-ExecutionPolicy** cmdlet을 사용하면 서명된 스크립트나 모든 스크립트를 실행하도록 설정할 수 있습니다. 신뢰할 수 있는 출처에서 제공하는 스크립트만 실행하고 적절한 NTFS 권한을 사용하여 모든 입력 및 출력 파일을 보호하십시오. PowerShell 스크립트를 설정하는 방법은 [Windows PowerShell 스크립트 실행](https://www.tech-recipes.com/rx/2513/powershell_enable_script_support/)을 참조하십시오.  
  
 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]의 `sqlps` 유틸리티 버전은 Windows PowerShell 1.0 미니 셸로 구현되었습니다. 미니 셸에는 사용자가 미니 셸에서 로드하는 스냅인 이외의 스냅인을 로드할 수 없는 것과 같은 몇 가지 제한 사항이 있습니다. 이러한 제한 사항은 `sqlps` 모듈을 사용하도록 변경된 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 이상 버전의 유틸리티에는 적용되지 않습니다.  
  
## <a name="examples"></a>예  
 **A. 저작권 배너를 표시하지 않고 sqlps 유틸리티를 기본 대화형 모드로 실행합니다.**  
  
```  
sqlps -NoLogo  
```  
  
 **B. 명령 프롬프트에서 SQL Server PowerShell 스크립트를 실행합니다.**  
  
```  
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
 **C. 명령 프롬프트에서 SQL Server PowerShell 스크립트를 실행하고 스크립트가 완료된 후에도 계속 실행되도록 합니다.**  
  
```  
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 설정 또는 해제](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
