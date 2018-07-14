---
title: 명령 프롬프트에서 업그레이드 관리자 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- command prompt [Upgrade Advisor]
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: a6841cc2-ca13-4b1c-9343-9e4d54312c3a
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 83d6e2fce7d4a9f2f5066aa568ecda57fd313efd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270269"
---
# <a name="installing-upgrade-advisor-from-the-command-prompt"></a>명령 프롬프트에서 업그레이드 관리자 설치
  설치 마법사를 사용하거나 명령 프롬프트에서 업그레이드 관리자를 설치할 수 있습니다. 명령 프롬프트를 사용하여 무인 및 자동 설치를 수행할 수 있습니다.  
  
## <a name="installation-syntax"></a>설치 구문  
 명령 프롬프트에서 업그레이드 관리자를 설치하는 기본 구문은 다음과 같습니다.  
  
 `SQLUA.msi [options]`  
  
 다음 표에서는 가장 일반적인 옵션을 보여 줍니다.  
  
|인수|Description|  
|--------------|-----------------|  
|/q [n&#124;b&#124;r&#124;f]|다음과 같이 UI(사용자 인터페이스) 수준을 설정합니다.<br /><br /> n = UI 표시 안 함<br /><br /> b = 기본 UI(진행률만 표시하고 프롬프트는 표시 안 함)<br /><br /> r = 축소된 UI(설치가 끝날 때 대화 상자 표시)<br /><br /> f = 전체 UI|  
|/L|로그 파일 옵션을 지정합니다. 모든 메시지를 기록할 *log_file_name*를 사용 하 여 **-L\*v * log_file_name*합니다. 사용 하 여 오류 메시지에만 기록할 `-Le` *log_file_name*합니다.|  
|ADDLOCAL = ALL&AMP;#124; 제거 = ALL&AMP;#124;REINSTALL = ALL|업그레이드 관리자의 설치(ADDLOCAL), 제거(REMOVE) 또는 다시 설치(REINSTALL)를 지정합니다.|  
|UAINSTALLDIR=path|경로를 사용하여 지정한 위치에 업그레이드 관리자를 설치합니다.|  
  
## <a name="installation-examples"></a>설치 예  
 다음 예에서는 명령 프롬프트를 사용하여 업그레이드 관리자를 설치하는 방법을 보여 줍니다.  
  
```  
SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 이 명령을 실행할 때는 다음과 같이 Msiexec 프로그램을 사용할 수도 있습니다.  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 이렇게 하면 추가 설치 옵션을 사용해야 하는 경우에 유용할 수 있습니다.  
  
## <a name="removal-examples"></a>제거 예  
 다음 예에서는 명령 프롬프트를 사용하여 업그레이드 관리자를 제거하는 방법을 보여 줍니다.  
  
```  
SQLUA.msi /qn REMOVE=ALL  
```  
  
 이 명령을 실행할 때는 다음과 같이 Msiexec 프로그램을 사용할 수도 있습니다.  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn REMOVE=ALL  
```  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 설치](../../../2014/sql-server/install/installing-upgrade-advisor.md)   
 [업그레이드 관리자 필수 구성 요소](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
