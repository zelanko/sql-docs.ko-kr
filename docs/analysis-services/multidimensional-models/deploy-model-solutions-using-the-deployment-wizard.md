---
title: 배포 마법사를 사용 하 여 모델 솔루션 배포 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cde312f2bfad67c6cfe61a9b8379973c1f59a56c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026070"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>배포 마법사를 사용하여 모델 솔루션 배포
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 생성 된 JSON 출력 파일을 사용 하는 배포 마법사는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 입력 파일로 프로젝트. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 배포를 사용자 지정할 수 있도록 이러한 입력 파일을 쉽게 수정할 수 있습니다. 그런 다음 생성된 배포 스크립트를 즉시 실행하거나 나중에 배포할 때 사용할 수 있도록 저장할 수 있습니다.  

> [!NOTE]
> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사/유틸리티와 함께 설치 됩니다 [SQL Server 관리 Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS). 최신 버전을 사용 하는 확인 해야 합니다. 기본적으로 명령 프롬프트에서 실행 하는 경우 최신 버전의 배포 마법사는 C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio에 설치 됩니다. 
  
 여기에 설명된 대로 마법사를 사용하여 배포할 수 있습니다. 또한 배포를 자동화하거나 동기화 기능을 사용할 수 있습니다. 배포된 데이터베이스가 큰 경우 대상 시스템에서 파티션 사용을 고려하세요. 테이블 형식 개체 모델 (TOM), Scriting 언어 TMSL (Tabular Model), Analysis Management Objects (AMO)를 사용 하 여 파티션 만들기 및 채우기를 자동화할 수 있습니다.  
  
> [!IMPORTANT]  
>  출력 파일 아니고 배포 스크립트가 포함 됩니다 사용자 id 또는 암호가 연결 문자열에 데이터 원본이 나 가장 용도의 지정 되는 경우. 이 시나리오에서는 처리 용도로 이러한 사용자 ID와 암호가 필요하므로 이러한 정보를 직접 추가하세요. 배포에 처리가 포함되지 않은 경우 배포 후 필요에 따라 이 연결 및 가장 정보를 추가할 수 있습니다. 배포에 처리가 포함될 경우 마법사 내에 이 정보를 추가하거나 이 정보가 저장된 후 배포 스크립트에 추가할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사, 입력 파일 및 배포 스크립트를 사용하는 방법에 대해 설명합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[Analysis Services 배포 마법사 실행](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사를 실행할 수 있는 여러 방법에 대해 설명합니다.|  
|[배포 스크립트를 만드는 데 입력된 파일 이해](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사가 입력 값으로 사용하는 파일 및 이러한 각 파일에 포함되는 내용에 대해 설명하고 각 입력 파일에서 값을 수정하는 방법을 설명하는 항목 링크를 제공합니다.|  
|[Analysis Services 배포 스크립트 이해](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|배포 스크립트에 포함된 내용 및 스크립트 실행 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [XMLA를 사용 하 여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Analysis Services 데이터베이스 동기화](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [배포 스크립트를 만드는 데 입력된 파일 이해](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)   
 [배포 유틸리티를 사용 하 여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
