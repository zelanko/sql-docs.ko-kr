---
title: XMLA를 사용 하 여 모델 솔루션 배포 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ce0f50d158d715ddbbc689c47a012a4e92ba7c4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022070"
---
# <a name="deploy-model-solutions-using-xmla"></a>XMLA를 사용하여 모델 솔루션 배포
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **데이터베이스 스크립팅** 명령의 **CREATE** 옵션은 전체 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 또는 해당 구성 개체 중 하나에 대해 XML 스크립트를 만듭니다. 그런 다음 결과로 얻은 스크립트를 다른 컴퓨터에서 실행하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 스키마(메타데이터)를 다시 만들 수 있습니다. 이 스크립트는 전체 데이터베이스를 생성합니다. 스크립트 사용 시 이미 배포된 개체를 증분 업데이트하는 메커니즘은 없습니다. 스크립트를 실행하고 데이터베이스를 배포한 후에는 새로 만든 데이터베이스를 처리해야만 사용자가 해당 데이터베이스를 찾아볼 수 있습니다.  
  
 **데이터베이스 스크립팅** 명령에 대한 자세한 내용은 [Analysis Services 데이터베이스 문서화 및 스크립트](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)를 참조하세요.  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>XML 스크립트에서 개체 속성 수정  
 **데이터베이스 스크립팅** 명령을 사용할 때는 데이터베이스 이름, 데이터 원본 연결 문자열 및 보안 설정과 같은 데이터베이스 개체의 특정 속성을 수정할 수 없습니다. 이러한 속성은 스크립트를 실행한 후 배포된 데이터베이스에서 스크립트가 생성되거나 수정된 이후에 해당 스크립트에서 수동으로 수정해야 합니다.  
  
> [!IMPORTANT]  
>  XML 스크립트가 데이터 원본이나 가장 용도의 연결 문자열에 지정된 경우 암호가 포함되지 않습니다. 이 시나리오에서는 처리 용도로 암호가 필요하기 때문에 XML 스크립트가 실행되기 전에 또는 XML 스크립트가 실행된 후에 해당 스크립트에 직접 추가해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [배포 마법사를 사용 하 여 모델 솔루션 배포](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)   
 [Analysis Services 데이터베이스 동기화](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
  
