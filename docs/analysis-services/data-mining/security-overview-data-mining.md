---
title: 보안 개요 (데이터 마이닝) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- security [Analysis Services - data mining], about security
ms.assetid: 387bde00-bcf3-4612-b27b-f9f608dbf71e
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5907b147aa4e06adfadaa2b56820088846d3fdd7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="security-overview-data-mining"></a>보안 개요(데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]보안 설정 과정 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 여러 수준에서 발생 합니다. 권한이 있는 사용자만 선택된 차원, 마이닝 모델 및 데이터 원본에 대한 읽기 또는 읽기/쓰기 권한을 갖도록 각 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 해당 데이터 원본의 보안을 설정해야 합니다. 또한 권한이 없는 사용자가 중요한 비즈니스 정보를 고의로 손상시킬 수 없도록 기본 데이터 원본의 보안을 설정해야 합니다. 다음 항목에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 보안 설정 과정을 설명합니다.  
  
##  <a name="bkmk_Architecture"></a> 보안 아키텍처  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 사용자 액세스 인증에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Windows 인증을 사용하는 방법을 비롯하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인스턴스의 기본 보안 아키텍처에 대한 자세한 내용은 다음 리소스를 참조하십시오.  
  
-   [보안 역할&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
-   [보안 속성](../../analysis-services/server-properties/security-properties.md)  
  
-   [서비스 계정 구성&#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)  
  
-   [개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_Logon"></a> Analysis Services에 대한 로그온 계정 구성  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 대한 적절한 로그온 계정을 선택하고 해당 계정의 사용 권한을 지정해야 합니다. 이때 기본 데이터 원본에 대한 적절한 사용 권한과 필수 태스크를 수행하는 데 필요한 사용 권한만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 로그온 계정에 지정합니다.  
  
 데이터 마이닝의 경우 모델을 작성하고 처리하려면 모델을 보거나 쿼리하는 데 필요한 권한과 다른 권한 집합이 필요합니다. 모델에 대한 예측을 만드는 것은 쿼리의 일종이므로 관리 권한이 필요하지 않습니다.  
  
##  <a name="bkmk_Instance"></a> Analysis Services 인스턴스 보안 설정  
 다음으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 컴퓨터, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 컴퓨터의 Windows 운영 체제, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 자체 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용하는 데이터 원본의 보안을 설정해야 합니다.  
  
##  <a name="bkmk_Access"></a> Analysis Services에 대한 액세스 구성  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 대해 권한 있는 사용자를 설정하고 정의하려면 특정 데이터베이스 개체를 관리할 수 있는 권한을 함께 부여할 사용자, 개체의 정의를 보거나 모델을 찾아볼 수 있는 사용자 및 데이터 원본에 직접 액세스할 수 있는 사용자를 결정해야 합니다.  
  
##  <a name="bkmk_DMspecial"></a> 데이터 마이닝에 대한 특별 고려 사항  
 분석가나 개발자가 데이터 마이닝 모델을 만들고 테스트할 수 있게 하려면 마이닝 모델이 저장되는 데이터베이스에 대한 관리 권한을 부여해야 합니다. 이로 인해 데이터 마이닝 분석가나 개발자가 데이터 마이닝과 관련되지 않은 다른 개체를 만들거나 삭제할 수도 있습니다. 이러한 개체로는 다른 분석가나 개발자가 만들어 사용 중인 데이터 마이닝 개체, 데이터 마이닝 솔루션에 포함되지 않은 OLAP 개체 등이 있습니다.  
  
 따라서 데이터 마이닝 솔루션을 만들 때는 분석가나 개발자가 모델을 개발, 테스트 및 조정하는 데 필요한 사항과 다른 사용자의 필요 사항을 균형 있게 조정하고 기존 데이터베이스 개체를 보호하는 조치를 취해야 합니다. 예를 들어 별도의 데이터 마이닝 전용 데이터베이스를 만들거나 각 분석가가 사용할 별도의 데이터베이스를 만들 수 있습니다.  
  
 모델을 만들려면 가장 높은 수준의 권한이 필요하지만, 역할 기반 보안을 사용하면 데이터 마이닝 모델에 대해 처리, 찾아보기 또는 쿼리 등의 다른 작업을 수행하는 데 필요한 사용자의 액세스 권한을 제어할 수 있습니다. 역할을 만들 때 데이터 마이닝 개체에만 적용되는 사용 권한을 설정할 수 있습니다. 역할의 멤버는 해당 역할에 연결된 모든 사용 권한을 자동으로 갖게 됩니다.  
  
 또한 데이터 마이닝 모델에서 중요한 정보가 들어 있는 데이터 원본을 참조하는 경우가 많습니다. 사용자가 모델에서 구조의 데이터로 드릴스루할 수 있도록 마이닝 구조 및 마이닝 모델이 구성된 경우 예방 조치를 통해 중요한 정보를 마스킹하거나 기본 데이터에 액세스할 수 있는 사용자를 제한해야 합니다.  
  
 Integration Services 패키지를 사용하여 데이터를 정리하거나 마이닝 모델을 업데이트하거나 예측을 만드는 경우 Integration Services 서비스에 모델이 저장된 데이터베이스에 대한 적절한 사용 권한과 원본 데이터에 대한 적절한 사용 권한이 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [역할 및 권한&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)  
  
  
