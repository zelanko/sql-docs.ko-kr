---
title: 프로젝트 및 패키지 배포 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 50da655d029228c4fc2339b49245cd11f5967305
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182840"
---
# <a name="deployment-of-projects-and-packages"></a>프로젝트 및 패키지 배포
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 프로젝트 배포 모델 및 패키지 배포 모델의 두 가지 배포 모델을 지원합니다. 프로젝트 배포 모델을 사용하면 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다.  
  
 프로젝트를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포하는 방법에 대한 자세한 내용은 [Integration Services 서버에 프로젝트 배포](../deploy-projects-to-integration-services-server.md)를 참조하세요.  
  
 패키지 배포 모델에 대 한 자세한 내용은 참조 [패키지 배포 &#40;SSIS&#41;](legacy-package-deployment-ssis.md)합니다.  
  
## <a name="compare-project-deployment-and-package-deployment"></a>프로젝트 배포와 패키지 배포 비교  
 프로젝트에 대해 선택한 배포 모델 유형에 따라 해당 프로젝트에 사용할 수 있는 배포 및 관리 옵션이 달라집니다. 다음 표에서는 프로젝트 배포 모델을 사용하는 경우와 패키지 배포 모델을 사용하는 경우의 차이점과 유사점을 보여 줍니다.  
  
|프로젝트 배포 모델을 사용하는 경우|패키지 배포 모델을 사용하는 경우|  
|---------------------------------------------|---------------------------------------------|  
|프로젝트가 배포 단위입니다.|패키지가 배포 단위입니다.|  
|패키지 속성에 값을 할당하는 데 매개 변수가 사용됩니다.|패키지 속성에 값을 할당하는 데 구성이 사용됩니다.|  
|패키지 및 매개 변수를 포함하는 프로젝트가 프로젝트 배포 파일(.ispac 확장명)에 기본 제공됩니다.|패키지(.dtsx 확장명) 및 구성(.dtsConfig 확장명)이 파일 시스템에 개별적으로 저장됩니다.|  
|패키지와 매개 변수를 포함하는 프로젝트가 SQL Server 인스턴스의 SSISDB 카탈로그에 배포됩니다.|패키지 및 구성이 다른 컴퓨터의 파일 시스템에 복사됩니다. SQL Server 인스턴스의 MSDB 데이터베이스에 패키지를 저장할 수도 있습니다.|  
|데이터베이스 엔진에서 CLR 통합이 필요합니다.|데이터베이스 엔진에서 CLR 통합이 필요하지 않습니다.|  
|환경 관련 매개 변수 값이 환경 변수에 저장됩니다.|환경 관련 구성 값이 구성 파일에 저장됩니다.|  
|카탈로그에 있는 프로젝트 및 패키지를 실행하기 전에 서버에서 유효성을 검사할 수 있습니다. SQL Server Management Studio, 저장 프로시저 또는 관리 코드를 사용하여 유효성 검사를 수행할 수 있습니다.|패키지를 실행하기 바로 전에 유효성을 검사합니다. 또한 dtExec 또는 관리 코드를 사용하여 패키지의 유효성을 검사할 수도 있습니다.|  
|데이터베이스 엔진에서 실행을 시작하는 방식으로 패키지를 실행합니다. 실행을 시작하기 전에 실행에 프로젝트 식별자, 명시적 매개 변수 값(옵션) 및 환경 참조(옵션)를 할당합니다.<br /><br /> 또한 `dtExec`를 사용하여 패키지를 실행할 수도 있습니다.|패키지를 사용 하 여 실행 된 `dtExec` 및 `DTExecUI` 실행 유틸리티입니다. 해당 구성이 명령 프롬프트 인수(옵션)로 식별됩니다.|  
|실행 시 패키지에 의해 생성된 이벤트가 자동으로 캡처되고 카탈로그에 저장됩니다. Transact-SQL 뷰를 사용하여 이러한 이벤트를 쿼리할 수 있습니다.|실행 시 패키지에 의해 생성된 이벤트가 자동으로 캡처되지 않습니다. 이벤트를 캡처하려면 로그 공급자를 패키지에 추가해야 합니다.|  
|패키지가 별도의 Windows 프로세스에서 실행됩니다.|패키지가 별도의 Windows 프로세스에서 실행됩니다.|  
|SQL Server 에이전트를 사용하여 패키지 실행을 예약합니다.|SQL Server 에이전트를 사용하여 패키지 실행을 예약합니다.|  
  
## <a name="features-of-project-deployment-model"></a>프로젝트 배포 모델의 기능  
 다음 표에서는 프로젝트 배포 모델에만 배포되는 프로젝트에 사용할 수 있는 기능을 나열합니다.  
  
|기능|Description|  
|-------------|-----------------|  
|매개 변수|매개 변수는 패키지에서 사용할 데이터를 지정합니다. 패키지 매개 변수 및 프로젝트 매개 변수를 사용하여 각각 패키지 수준 또는 프로젝트 수준으로 매개 변수 범위를 지정할 수 있습니다. 매개 변수를 식 또는 태스크에서 사용할 수 있습니다. 프로젝트가 카탈로그에 배포되면 각 매개 변수의 리터럴 값을 할당하거나 디자인 타임에 할당된 기본값을 사용할 수 있습니다. 리터럴 값 대신 환경 변수를 참조할 수도 있습니다. 환경 변수 값은 패키지 실행 시 확인됩니다.|  
|환경|환경은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트에서 참조할 수 있는 변수의 컨테이너입니다. 각 프로젝트는 환경 참조를 여러 개 가질 수 있지만 단일 패키지 실행 인스턴스는 단일 환경의 변수만 참조할 수 있습니다. 환경을 사용하여 패키지에 할당할 값을 구성할 수 있습니다. 예를 들어 "Dev", "test" 및 "Production"이라는 환경이 있을 수 있습니다.|  
|환경 변수|환경 변수는 패키지 실행 시 매개 변수에 할당할 수 있는 리터럴 값을 정의합니다. 환경 변수를 사용하려면 실행 인스턴스를 구성할 때 매개 변수가 있는 환경에 해당하는 프로젝트에 환경 참조를 만들고, 환경 변수 이름에 매개 변수 값을 할당하고, 해당 환경 참조를 지정합니다.|  
|SSISDB 카탈로그|모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체는 SSISDB 카탈로그라는 데이터베이스의 SQL Server 인스턴스에 저장되고 관리됩니다. 카탈로그를 통해 폴더를 사용하여 프로젝트 및 환경을 구성할 수 있습니다. 각 SQL Server 인스턴스는 카탈로그를 하나만 가질 수 있습니다. 각 카탈로그는 0개 이상의 폴더를 가질 수 있습니다. 각 폴더는 0개 이상의 프로젝트 및 0개 이상의 환경을 가질 수 있습니다. 카탈로그의 폴더를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체에 대한 사용 권한의 경계로 사용할 수도 있습니다.|  
|카탈로그 저장 프로시저 및 뷰|많은 수의 저장 프로시저 및 뷰를 사용하여 카탈로그의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체를 관리할 수 있습니다. 예를 들어 매개 변수 및 환경 변수에 값을 지정하고, 실행을 생성 및 시작하고, 카탈로그 작업을 모니터링할 수 있습니다. 실행이 시작되기 전에 패키지에서 사용될 값을 정확히 확인할 수도 있습니다.|  
  
## <a name="project-deployment"></a>프로젝트 배포  
 프로젝트 배포 모델의 중앙에는 프로젝트 배포 파일(.ispac extension)이 있습니다. 프로젝트 배포 파일은 프로젝트의 패키지 및 매개 변수에 대한 중요 정보만 포함하는 자체 포함된 배포 단위입니다. 프로젝트 배포 파일은 Integration Services 프로젝트 파일(.dtproj 확장명)에 포함된 모든 정보 중 일부만 캡처합니다. 예를 들어 메모를 작성하는 데 사용하는 추가 텍스트 파일은 프로젝트 배포 파일에 저장되지 않으므로 카탈로그에 배포되지 않습니다.  
  
## <a name="required-tasks"></a>필수 태스크  
  
-   [Integration Services 서버에 프로젝트 배포](../deploy-projects-to-integration-services-server.md)  
  
## <a name="related-content"></a>관련 내용  
 mattmasson.com의 블로그 항목 [SSIS 프로젝트의 분기 전략에 대한 고려 사항](http://go.microsoft.com/fwlink/?LinkId=245739)  
  
## <a name="see-also"></a>관련 항목  
 [dtexec 유틸리티](dtexec-utility.md)  
  
  