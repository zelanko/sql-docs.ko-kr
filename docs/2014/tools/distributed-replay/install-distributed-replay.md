---
title: 명령 프롬프트에서 Distributed Replay 설치 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ea1171da-f50e-4f16-bedc-5e468a46477f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 67d74db6faf9b40ad323ed2948c2c0a596a63016
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816065"
---
# <a name="install-distributed-replay-from-the-command-prompt"></a>명령 프롬프트에서 Distributed Replay 설치
  명령 프롬프트에서 Distributed Replay의 새 인스턴스를 설치할 경우 어떤 기능을 설치할지 지정하고 그 기능을 어떻게 구성할지 지정할 수 있습니다. 명령 프롬프트에서 설치하면 Distributed Replay 구성 요소를 설치, 복원, 업그레이드 및 제거할 수 있습니다. 명령 프롬프트에서 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 /Q 매개 변수를 사용하는 완전 자동 모드를 지원합니다.  
  
> [!NOTE]  
>  로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  
  
## <a name="installation-parameters"></a>설치 매개 변수  
 최상위 기능 목록에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]및 도구가 포함됩니다. 도구 기능은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 도구, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]및 기타 공유 구성 요소를 설치합니다. Distributed Replay 구성 요소를 설치하려면 다음 매개 변수를 지정합니다.  
  
|구성 요소|매개 변수|  
|---------------|---------------|  
|Distributed Replay Controller|**DREPLAY_CTLR**|  
|Distributed Replay Client|**DREPLAY_CLT**|  
|관리 도구|**Tools**|  
  
> [!IMPORTANT]  
>  Distributed Replay를 설치한 후에는 컨트롤러 및 클라이언트 컴퓨터에서 방화벽 규칙을 만들고 각 클라이언트 컴퓨터에 대상 서버에 대한 권한을 부여해야 합니다. 자세한 내용은 [설치 후 단계 완료](complete-the-post-installation-steps.md)를 참조하세요.  
  
 다음 표에 나와 있는 매개 변수를 사용하여 설치 명령줄 스크립트를 개발할 수 있습니다.  
  
|매개 변수|Description|지원되는 값|  
|---------------|-----------------|----------------------|  
|/CTLRSVCACCOUNT<br /><br /> **선택 사항**|Distributed Replay Controller 서비스의 서비스 계정|계정 및 암호 확인|  
|/CTLRSVCPASSWORD<br /><br /> **선택 사항**|Distributed Replay Controller 서비스 계정의 암호|계정 및 암호 확인|  
|/CTLRSTARTUPTYPE<br /><br /> **선택 사항**|Distributed Replay Controller 서비스의 시작 유형|자동<br /><br /> 사용 안 함<br /><br /> 수동|  
|/CTLRUSERS<br /><br /> **선택 사항**|Distributed Replay Controller 서비스에 대한 사용 권한을 가지는 사용자를 지정합니다.|구분 기호로 공백(“ ”)을 사용하는 일련의 사용자 계정 문자열<br /><br /> **중요 한**: Distributed Replay Controller 서비스를 구성할 때 Distributed Replay Client 서비스를 실행하는 데 사용할 사용자 계정을 하나 이상 지정할 수 있습니다. 다음은 지원되는 계정 목록입니다.<br /><br /> 도메인 사용자 계정<br /><br /> 사용자가 만든 로컬 사용자 계정<br /><br /> 관리자<br /><br /> 가상 계정 및 MSA(관리 서비스 계정)<br /><br /> Network Services, 로컬 서비스 및 시스템<br /><br /> <br /><br /> 그룹 계정(로컬 또는 도메인) 및 다른 기본 제공 계정(예: Everyone)은 사용할 수 없습니다.|  
|/CLTSVCACCOUNT<br /><br /> **선택 사항**|Distributed Replay Client 서비스의 서비스 계정|계정 및 암호 확인|  
|/CLTSVCPASSWORD<br /><br /> **선택 사항**|Distributed Replay Client 서비스 계정의 암호|계정 및 암호 확인|  
|/CLTSTARTUPTYPE<br /><br /> **선택 사항**|Distributed Replay Client 서비스의 시작 유형|자동<br /><br /> 사용 안 함<br /><br /> 수동|  
|/CLTCTLRNAME<br /><br /> **선택 사항**|클라이언트에서 Distributed Replay Controller 서비스를 위해 통신하는 컴퓨터 이름||  
|/CLTWORKINGDIR<br /><br /> **선택 사항**|Distributed Replay Client 서비스의 작업 디렉터리|올바른 경로|  
|/CLTRESULTDIR<br /><br /> **선택 사항**|Distributed Replay Client 서비스의 결과 디렉터리|올바른 경로|  
  
### <a name="sample-syntax"></a>예제 구문:  
 **Distributed Replay Controller 구성 요소를 설치하려면**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CTLR /IAcceptSQLServerLicenseTerms /CTLRUSERS="domain\user1" "domain\user2" /CTLRSVCACCOUNT="domain\svcuser" /CTLRSVCPASSWORD="password" /CTLRSTARTUPTYPE=Automatic  
```  
  
 **Distributed Replay Client 구성 요소를 설치하려면**  
  
```  
setup /q /ACTION=Install /FEATURES=DREPLAY_CLT /IAcceptSQLServerLicenseTerms /CLTSVCACCOUNT="domain\svcuser" /CLTSVCPASSWORD="password" /CLTSTARTUPTYPE=Automatic /CLTCTLRNAME=ControllerMachineName /CLTWORKINGDIR="C:\WorkingDir" /CLTRESULTDIR="C:\ResultDir  
```  
  
  
