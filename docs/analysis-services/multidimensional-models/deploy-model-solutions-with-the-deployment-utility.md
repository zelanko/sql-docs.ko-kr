---
title: 배포 유틸리티를 사용 하 여 모델 솔루션 배포 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 76d1a3e3cfff777f610bb00f52644af3903ac615
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37975164"
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>배포 유틸리티를 사용하여 모델 솔루션 배포
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  **Microsoft.AnalysisServices.Deployment** 유틸리티를 사용하여 명령 프롬프트에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 엔진을 시작할 수 있습니다. 입력 파일로서 이 유틸리티는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]프로젝트를 구축하여 생성된 XML 출력 파일을 사용합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 배포를 사용자 지정할 수 있도록 이 입력 파일을 쉽게 수정할 수 있습니다. 그런 다음 생성된 배포 스크립트를 즉시 실행하거나 나중에 배포할 때 사용할 수 있도록 저장할 수 있습니다.  
  
> [!NOTE]
> 합니다 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사/유틸리티와 함께 설치 됩니다 [SQL Server 관리 Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS). 최신 버전을 사용 해야 합니다. 기본적으로 최신 버전의 배포 마법사는 C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio에 설치 됩니다. 

## <a name="syntax"></a>구문  
  
```  
  
Microsoft.AnalysisServices.Deployment [ASdatabasefile]   
    {[/s[:logfile]] | [/a] | [[/o[:output_script_file]] [/d]]}  
```  
  
##  <a name="Arguments"></a> 인수  
 *ASdatabasefile*  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 스크립트(.asdatabase) 파일이 있는 폴더의 전체 경로입니다. 이 파일은 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 프로젝트를 배포할 때 생성되며 프로젝트 bin 폴더에 있습니다. .asdatabase 파일에는 배포할 개체 정의가 포함되어 있습니다. 이 인수를 지정하지 않으면 현재 폴더가 사용됩니다.  
  
 **/s**  
 자동 모드에서 유틸리티를 실행하며 대화 상자를 표시하지 않습니다. 모드에 대한 자세한 내용은 이 항목 뒷부분에 나오는 [모드](#Modes)섹션을 참조하십시오.  
  
 *logfile*  
 로그 파일의 전체 경로 및 파일 이름입니다. 추적 이벤트는 지정된 로그 파일에 기록됩니다. 로그 파일이 이미 있을 경우 파일 내용이 바뀝니다.  
  
 **/a**  
 응답 모드에서 유틸리티를 실행합니다. 유틸리티의 마법사 부분 중 수행한 모든 응답은 다시 입력 파일에 기록되어야 하지만 실제로 배포 대상은 변경되지 않습니다.  
  
 **/o**  
 출력 모드에서 유틸리티를 실행합니다. 배포가 발생하지 않지만 일반적으로 배포 대상으로 보내지는 XMLA(XML for Analysis) 스크립트가 지정된 출력 스크립트 파일에 대신 저장됩니다. *output_script_file* 을 지정하지 않으면 이 유틸리티에서는 배포 옵션 입력 파일(.deploymentoptions)에 지정된 출력 스크립트 파일을 사용합니다. 배포 옵션 입력 파일에서 출력 스크립트 파일을 지정하지 않은 경우 오류가 발생합니다.  
  
 모드에 대한 자세한 내용은 이 항목 뒷부분에 나오는 [모드](#Modes)섹션을 참조하십시오.  
  
 *output_script_file*  
 출력 스크립트 파일의 전체 경로 및 파일 이름입니다.  
  
 **/d**  
 **/o** 인수가 사용되는 경우 유틸리티에서 대상 인스턴스에 연결하지 않도록 지정합니다. 배포 대상에 대한 연결이 이루어지지 않기 때문에 출력 파일에서 검색된 정보만 사용하여 출력 스크립트가 생성됩니다.  
  
> [!NOTE]  
>  **/d** 인수는 출력 모드에서만 사용됩니다. 응답 모드나 자동 모드에서는 이 인수를 지정해도 무시됩니다. 모드에 대한 자세한 내용은 이 항목 뒷부분에 나오는 [모드](#Modes)섹션을 참조하십시오.  
  
## <a name="remarks"></a>Remarks  
 **Microsoft.AnalysisServices.Deployment** 유틸리티에서는 개체 정의, 배포 대상, 배포 옵션 및 구성 설정을 제공하는 일련의 파일을 사용하며 지정된 배포 옵션 및 구성 설정을 사용하여 지정된 배포 대상으로 개체 정의를 배포하려고 시도합니다. 이 유틸리티는 응답 파일이나 출력 모드에서 호출될 경우 사용자 인터페이스를 제공할 수 있습니다. 이 유틸리티에 제공된 사용자 인터페이스를 사용하여 응답 파일을 만드는 방법은 [배포 마법사를 사용하여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)를 참조하세요.  
  
 유틸리티는 \Program files (x86) \Microsoft SQL Server\140\Binn\ManagementStudio 폴더에 있습니다.  
  
##  <a name="Modes"></a> 모드  
 다음 표에 나열된 모드에서 유틸리티를 실행할 수 있습니다.  
  
|모드|Description|  
|----------|-----------------|  
|자동 모드|사용자 인터페이스는 표시되지 않으며 배포에 필요한 모든 정보는 입력 파일에서 제공됩니다. 자동 모드에서 실행되는 유틸리티는 진행률을 표시하지 않습니다. 대신 나중에 검토할 수 있도록 로그 파일(옵션)을 사용하여 진행률 및 오류 정보를 캡처할 수 있습니다.|  
|응답 모드|배포 마법사 사용자 인터페이스가 표시되며 사용자 응답은 나중에 배포할 때 사용할 수 있도록 지정된 입력 파일에 저장됩니다. 응답 모드에서는 배포가 이루어지지 않습니다. 응답 모드는 사용자 응답 캡처 전용 모드입니다.|  
|출력 모드|사용자 인터페이스는 표시되지 않으며 배포에 필요한 모든 정보는 입력 파일에서 제공됩니다.<br /><br /> 그러나 자동 모드와 달리 유틸리티의 출력은 출력 스크립트 파일에 쓰여지며 입력 파일에 지정된 배포 대상으로 보내지지 않습니다. **/d** 인수를 지정하지 않으면 출력 스크립트 파일을 생성하는 동안 유틸리티에서 각 배포 대상에 연결하여 메타데이터를 비교합니다.|  
  
 [인수로 돌아가기](#Arguments)  
  
## <a name="examples"></a>예  
 다음 예에서는 자동 모드에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 배포하고 나중에 검토할 수 있도록 진행률과 오류 메시지를 기록하는 방법을 보여 줍니다.  
  
 `Microsoft.AnalysisServices.Deployment.exe`  
  
 `<drive>:\My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin`  
  
 `/s: C:\ My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin\deployment.log`  
  
## <a name="see-also"></a>관련 항목  
 [명령 프롬프트 유틸리티 참조&#40;데이터베이스 엔진#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
