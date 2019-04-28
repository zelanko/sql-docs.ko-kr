---
title: 패키지의 중요한 데이터에 대한 액세스 제어 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services], security
- protection levels for packages [Integration Services]
- configuration files [Integration Services]
- encryption [Integration Services]
- cryptography [Integration Services]
- security [Integration Services], protection levels
ms.assetid: d4b073c4-4238-41fc-a258-4e114216e185
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d59a42fa7b77e6800218f1eeca4986320c1dcef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766783"
---
# <a name="access-control-for-sensitive-data-in-packages"></a>패키지의 중요한 데이터에 대한 액세스 제어
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터를 보호하기 위해 중요한 데이터만 보호하거나 패키지의 모든 데이터를 보호하는 패키지 수준을 설정할 수 있습니다. 또한 패키지 데이터를 암호 또는 사용자 키로 암호화하거나 데이터베이스를 사용하여 암호화할 수도 있습니다. 패키지 보호 수준은 반드시 정적이지 않으며 패키지의 수명 주기 동안 변경됩니다. 즉, 개발 과정에서 설정하는 보호 수준과 배포 과정에서 설정하는 보호 수준이 서로 다른 경우가 자주 있습니다.  
  
> [!NOTE]  
>  이 항목에서 설명하는 보호 수준 외에도 고정 데이터베이스 수준 역할을 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 저장한 패키지를 보호할 수 있습니다.  
  
## <a name="definition-of-sensitive-information"></a>중요한 정보 정의  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서는 다음과 같은 정보가 *중요한 정보*로 정의됩니다.  
  
-   연결 문자열의 암호 부분. 그러나 전체 암호화 옵션을 선택할 경우 연결 문자열 전체가 중요한 정보로 간주됩니다.  
  
-   중요한 정보라는 태그가 지정된 태스크 생성 XML 노드. XML 노드의 태그는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 제어하며 사용자가 변경할 수 없습니다.  
  
-   중요한 정보로 표시된 모든 변수. 변수 표시는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 제어됩니다.  
  
 특정 속성이 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 중요한 속성으로 간주되는지 여부는 연결 관리자나 태스크와 같은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소의 개발자가 속성을 중요한 것으로 지정했는지 여부에 따라 달라집니다. 사용자는 중요한 것으로 간주되는 속성 목록에서 속성을 추가하거나 제거할 수 없습니다.  
  
## <a name="encryption"></a>암호화  
 패키지 보호 수준의 암호화는 CryptoAPI(암호화 API)의 일부인 [!INCLUDE[msCoName](../../includes/msconame-md.md)] DPAPI(데이터 보호 API)를 사용하여 수행됩니다.  
  
 암호를 사용하여 패키지를 암호화하는 패키지 보호 수준에서도 암호를 입력해야 합니다. 암호를 사용하지 않는 수준에서 암호를 사용하는 수준으로 보호 수준을 변경하는 경우 암호를 입력하라는 메시지가 표시됩니다.  
  
 또한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 암호를 사용하는 보호 수준에 FCL( [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스 라이브러리)에서 제공하는 Triple DES 암호화 알고리즘 및 192비트 키를 사용합니다.  
  
## <a name="protection-levels"></a>보호 수준  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 제공하는 보호 수준에 대해 설명합니다. 괄호 안의 값은 <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel> 열거형의 값입니다. 이러한 값은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 사용할 때 패키지의 속성을 구성하는 속성 창에 표시됩니다.  
  
|보호 수준|Description|  
|----------------------|-----------------|  
|중요한 정보 저장 안 함(`DontSaveSensitive`)|패키지를 저장할 때 중요한 속성의 값을 패키지에서 제외합니다. 이 보호 수준은 암호화는 사용하지 않지만 중요한 것으로 표시된 속성이 패키지로 저장되는 것을 방지하여 다른 사용자가 중요한 데이터를 사용하지 못하도록 합니다. 다른 사용자가 패키지를 여는 경우 중요한 정보는 빈칸으로 대체되므로 해당 사용자가 중요한 정보를 지정해야 합니다.<br /><br /> **dtutil** 유틸리티(dtutil.exe)에서 사용할 경우 이 보호 수준은 값 0에 해당합니다.|  
|암호로 모두 암호화(`EncryptAllWithPassword`)|암호를 사용하여 전체 패키지를 암호화합니다. 패키지를 만들거나 내보낼 때 사용자가 입력한 암호를 사용하여 패키지를 암호화합니다. 사용자는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지를 열거나 **dtexec** 명령 프롬프트 유틸리티를 사용하여 패키지를 실행할 때 패키지 암호를 입력해야 합니다. 암호를 입력하지 않으면 패키지를 실행할 수 없습니다.<br /><br /> **dtutil** 유틸리티에서 사용할 경우 이 보호 수준은 값 3에 해당합니다.|  
|사용자 키로 모두 암호화(`EncryptAllWithUserKey`)|현재 사용자 프로필을 기반으로 하는 키를 사용하여 전체 패키지를 암호화합니다. 패키지를 만들거나 내보낸 사용자만 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지를 열거나 **dtexec** 명령 프롬프트 유틸리티를 사용하여 패키지를 실행할 수 있습니다.<br /><br /> **dtutil** 유틸리티에서 사용할 경우 이 보호 수준은 값 4에 해당합니다.<br /><br /> 참고: 사용자 키를 사용 하는 보호 수준에 대 한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] DPAPI 표준을 사용 합니다. DPAPI에 대한 자세한 내용은 [https://msdn.microsoft.com/library](https://go.microsoft.com/fwlink/?LinkId=15408)에 있는 MSDN Library를 참조하세요.|  
|암호로 중요한 정보 암호화(`EncryptSensitiveWithPassword`)|암호를 사용하여 패키지에서 중요한 속성의 값만 암호화합니다. 이 암호화에는 DPAPI가 사용됩니다. 중요한 데이터는 패키지의 일부로 저장되지만 패키지를 만들거나 내보낼 때 사용자가 입력한 암호를 사용하여 암호화됩니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지를 열려면 패키지 암호를 입력해야 합니다. 임호를 입력하지 않으면 패키지의 중요한 정보가 제외되며 현재 사용자가 중요한 정보에 새 값을 입력해야 합니다. 암호를 입력하지 않으면 패키지를 실행할 수 없습니다. 암호 및 명령줄 실행에 대한 자세한 내용은 [dtexec Utility](../packages/dtexec-utility.md)를 참조하십시오.<br /><br /> **dtutil** 유틸리티에서 사용할 경우 이 보호 수준은 값 2에 해당합니다.|  
|사용자 키로 중요 정보 암호화(`EncryptSensitiveWithUserKey`)|현재 사용자 프로필을 기반으로 하는 키를 사용하여 패키지에서 중요한 속성의 값만 암호화합니다. 동일한 프로필을 사용하는 동일한 사용자만 패키지를 로드할 수 있습니다. 다른 사용자가 패키지를 여는 경우 중요한 정보는 빈칸으로 대체되므로 현재 사용자가 중요한 데이터에 새 값을 지정해야 합니다. 사용자가 패키지를 실행하려고 시도하는 경우 패키지 실행이 실패합니다. 이 암호화에는 DPAPI가 사용됩니다.<br /><br /> **dtutil** 유틸리티에서 사용할 경우 이 보호 수준은 값 1에 해당합니다.<br /><br /> 참고: 사용자 키를 사용 하는 보호 수준에 대 한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] DPAPI 표준을 사용 합니다. DPAPI에 대한 자세한 내용은 [https://msdn.microsoft.com/library](https://go.microsoft.com/fwlink/?LinkId=15408)에 있는 MSDN Library를 참조하세요.|  
|암호화에 서버 저장소 사용(`ServerStorage`)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 역할을 사용하여 전체 패키지를 보호합니다. 이 옵션은 패키지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 데이터베이스에 저장할 때 지원됩니다. 또한 SSISDB 카탈로그에서는 `ServerStorage` 보호 수준을 사용합니다.<br /><br /> 이 옵션은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 파일 시스템에 패키지를 저장하는 경우에는 지원되지 않습니다.|  
  
## <a name="protection-level-setting-and-the-ssisdb-catalog"></a>보호 수준 설정 및 SSISDB 카탈로그  
 SSISDB 카탈로그에서는 `ServerStorage` 보호 수준을 사용합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포하는 경우 카탈로그에서 패키지 데이터와 중요한 값을 자동으로 암호화합니다. 카탈로그에서는 검색하는 데이터의 암호도 자동으로 해제합니다.  
  
 프로젝트(.ispac 파일)를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에서 파일 시스템으로 내보내는 경우 보호 수준이 `EncryptSensitiveWithUserKey`로 자동으로 변경됩니다. 사용 하 여 프로젝트를 가져오는 경우는 **Integration Services 프로젝트 가져오기 마법사** 에 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **ProtectionLevel** 속성에는 **속성** 창 값이 표시 `EncryptSensitiveWithUserKey`합니다.  
  
## <a name="protection-level-setting-based-on-package-life-cycle"></a>패키지 수명 주기 기반의 보호 수준 설정  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 보호 수준은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지 개발을 시작할 때 처음 설정할 수 있습니다. 나중에 패키지를 배포하거나 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]로 패키지를 가져오거나 또는 내보낼 때 그리고 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 저장소 또는 파일 시스템으로 복사할 때 패키지 보호 수준을 업데이트할 수 있습니다. 예를 들어 사용자 키 보호 수준 옵션 중 하나를 사용하여 사용자 컴퓨터에 패키지를 만들고 저장한 경우 해당 패키지를 다른 사용자에게 전달하기 전에 보호 수준을 변경해야 합니다. 그렇지 않으면 패키지를 열 수 없습니다.  
  
 다음은 일반적으로 보호 수준을 변경하는 단계를 순서대로 나열한 것입니다.  
  
1.  개발 과정에서는 패키지의 보호 수준을 기본값인 `EncryptSensitiveWithUserKey`로 설정된 상태로 둡니다. 이 설정을 사용하면 개발자만 패키지의 중요한 데이터를 볼 수 있습니다. 또는 `EncryptAllWithUserKey` 또는 `DontSaveSensitive`를 사용할 수도 있습니다.  
  
2.  패키지를 배포할 때는 보호 수준을 개발자의 사용자 키가 필요 없는 보호 수준으로 변경해야 합니다. 따라서 대부분의 경우 `EncryptSensitiveWithPassword` 또는 `EncryptAllWithPassword`를 선택해야 합니다. 프로덕션 환경의 운영 팀도 알고 있는 임시 강력한 암호를 할당하여 패키지를 암호화합니다.  
  
3.  프로덕션 환경에 패키지가 배포된 후에는 운영 팀이 자신들만 알고 있는 강력한 암호를 할당하여 배포된 패키지를 다시 암호화할 수 있습니다. 또는 운영 팀이 `EncryptSensitiveWithUserKey` 또는 `EncryptAllWithUserKey`를 선택하고 패키지를 실행할 계정의 로컬 자격 증명을 사용하여 배포된 패키지를 암호화할 수도 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [패키지 보호 수준 설정 또는 변경](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>관련 항목  
 [패키지 가져오기 및 내보내기&#40;SSIS 서비스&#41;](../import-and-export-packages-ssis-service.md)   
 [Integration Services&#40;SSIS&#41; 패키지](../integration-services-ssis-packages.md)   
 [보안 개요&#40;Integration Services&#41;](security-overview-integration-services.md)  
  
  
