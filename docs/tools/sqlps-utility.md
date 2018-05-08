---
title: sqlps 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: sqlps
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sqlps utility
- PowerShell [SQL Server], sqlps utility
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 75d8e510d2367fe56e392cff103ac4dfe0fbf82c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="sqlps-utility"></a>sqlps 유틸리티
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **sqlps** 유틸리티는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 공급자와 cmdlet이 로드 및 등록된 Windows PowerShell 세션을 시작합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 구성 요소를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스 및 해당 개체와 함께 작동하는 PowerShell 명령 또는 스크립트를 입력할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] 대신 **sqlps** PowerShell 모듈을 사용하세요. **sqlps** 모듈에 대한 자세한 내용은 [Import the SQLPS Module](../relational-databases/scripting/import-the-sqlps-module.md)를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -args argument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## <a name="arguments"></a>인수  
 **-NoLogo**  
 **sqlps** 유틸리티가 시작될 때 저작권 배너를 표시하지 않도록 지정합니다.  
  
 **-NoExit**  
 시작 명령이 완료된 후에도 **sqlps** 유틸리티가 계속 실행되도록 지정합니다.  
  
 **-NoProfile**  
 **sqlps** 유틸리티가 사용자 프로필을 로드하지 않도록 지정합니다. 사용자 프로필은 PowerShell 세션에서 사용하도록 공통적으로 사용되는 별칭, 함수 및 변수를 기록합니다.  
  
 **-OutPutFormat** { **Text** | **XML** }  
 **sqlps** 유틸리티 출력 형식이 텍스트 문자열(**Text**) 또는 직렬화된 CLIXML 형식(**XML**)이 되도록 지정합니다.  
  
 **-InPutFormat** { **Text** | **XML** }  
 **sqlps** 유틸리티에 대한 입력 형식이 텍스트 문자열(**Text**) 또는 직렬화된 CLIXML 형식(**XML**)이 되도록 지정합니다.  
  
 **-Command**  
 **sqlps** 유틸리티에 대한 명령이 실행되도록 지정합니다. **sqlps** 유틸리티는 **-NoExit** 가 지정되지 않은 경우 명령을 실행한 다음 종료됩니다. **-Command**뒤에는 다른 스위치를 지정하지 마세요. 이 경우 스위치가 명령 매개 변수로 읽힙니다.  
  
 **-**  
 **-Command-** 는 **sqlps** 유틸리티가 표준 입력으로부터 입력을 읽도록 지정합니다.  
  
 *script_block* [ **-args***argument_array* ]  
 실행할 PowerShell 명령 블록을 지정합니다. 명령 블록은 중괄호 {}로 묶어야 합니다. *Script_block* 은 **sqlps** 유틸리티가 **PowerShell** 또는 다른 **sqlps** 유틸리티 세션에서 호출된 경우에만 지정할 수 있습니다. *argument_array* 는 *script_block*의 PowerShell 명령에 대한 인수를 포함하는 PowerShell 변수 배열입니다.  
  
 *string* [ *command_parameters* ]  
 실행할 PowerShell 명령을 포함하는 문자열을 지정합니다. **"&{***command***}"** 형식을 사용합니다. 큰따옴표는 문자열을 나타내며 호출 연산자(&)는 **sqlps** 유틸리티가 명령을 실행하도록 합니다.  
  
 [ **-?** | **-Help** ]  
 **sqlps** 유틸리티 옵션의 구문 요약 정보를 표시합니다.  
  
## <a name="remarks"></a>Remarks  
 **sqlps** 유틸리티는 PowerShell 환경(PowerShell.exe)을 시작하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 모듈을 로드합니다. **sqlps**라고도 하는 이 모듈은 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 스냅인을 로드하고 등록합니다.  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 공급자 및 **Encode-SqlName** , **Decode-SqlName**과 같은 관련 cmdlet을 구현합니다.  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     **Invoke-Sqlcmd** 및 **Invoke-PolicyEvaluation** cmdlet을 구현합니다.  
  
 다음과 같은 작업에 **sqlps** 유틸리티를 사용할 수 있습니다.  
  
-   대화형으로 PowerShell 명령을 실행합니다.  
  
-   PowerShell 스크립트 파일을 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet을 실행합니다.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자 경로를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개체의 계층 구조를 탐색합니다.  
  
 기본적으로 **sqlps** 유틸리티는 스크립팅 실행 정책이 **Restricted**로 설정된 상태로 실행됩니다. 이는 모든 PowerShell 스크립트의 실행을 차단합니다. **Set-ExecutionPolicy** cmdlet을 사용하면 서명된 스크립트나 모든 스크립트를 실행하도록 설정할 수 있습니다. 신뢰할 수 있는 출처에서 제공하는 스크립트만 실행하고 적절한 NTFS 권한을 사용하여 모든 입력 및 출력 파일을 보호하십시오. PowerShell 스크립트를 설정하는 방법은 [Windows PowerShell 스크립트 실행](http://go.microsoft.com/fwlink/?LinkId=103166)을 참조하십시오.  
  
 **및** 의 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] sqlps [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 유틸리티 버전은 Windows PowerShell 1.0 미니 셸로 구현되었습니다. 미니 셸에는 사용자가 미니 셸에서 로드하는 스냅인 이외의 스냅인을 로드할 수 없는 것과 같은 몇 가지 제한 사항이 있습니다. 이러한 제한 사항은 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 모듈을 사용하도록 변경된 **sqlps** 이상 버전의 유틸리티에는 적용되지 않습니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 설정 또는 해제](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)  
  
  
