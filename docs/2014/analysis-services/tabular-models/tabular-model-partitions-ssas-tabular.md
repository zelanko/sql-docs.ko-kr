---
title: 테이블 형식 모델 파티션 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssms.partitions.partitionmgr.imbi.f1
ms.assetid: 041c269f-a229-4a41-8794-6ba4b014ef83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aaa2b608665e50b25b39d78a39a57bb08b55cf31
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66066393"
---
# <a name="tabular-model-partitions-ssas-tabular"></a>테이블 형식 모델 파티션(SSAS 테이블 형식)
  파티션은 테이블을 논리적 부분으로 나눕니다. 각 파티션은 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 모델 제작 중에 모델에 대해 정의한 파티션은 배포된 모델에서 복제됩니다. 배포한 후에는 **의** 파티션 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 대화 상자 또는 스크립트를 사용하여 파티션을 관리하고 새 파티션을 만들 수 있습니다. 이 항목에서 제공하는 정보는 배포된 테이블 형식 model 데이터베이스의 파티션에 대해 설명합니다. 모델을 제작하는 동안 파티션을 만들고 관리하는 방법에 대한 자세한 내용은 [파티션&#40;SSAS 테이블 형식&#41;](partitions-ssas-tabular.md)을 참조하세요.  
  
 이 항목의 섹션:  
  
-   [이점](#bkmk_benefits)  
  
-   [사용 권한](#bkmk_permissions)  
  
-   [파티션 처리](#bkmk_process_partitions)  
  
-   [관련 작업](#bkmk_related_tasks)  
  
##  <a name="bkmk_benefits"></a> 이점  
 효과적인 모델 디자인은 파티션을 이용하여 불필요한 처리 및 Analysis Services 서버에 대한 후속 프로세서 로드를 배제하는 동시에 데이터 원본의 최신 데이터를 반영하여 데이터를 자주 처리하고 새로 고칠 수 있습니다.  
  
 예를 들어 테이블 형식 모델에 현재 2011 회계 연도와 이전 회계 연도의 판매 데이터를 포함하는 Sales 테이블이 있을 수 있습니다. 모델의 Sales 테이블에 다음과 같은 세 개의 파티션이 있습니다.  
  
|Partition|데이터 출처|  
|---------------|---------------|  
|Sales2011|현재 회계 연도|  
|Sales2010-2001|회계 연도 2001, 2002, 2003, 2004, 2005, 2006. 2007, 2008, 2009, 2010|  
|SalesOld|지난 10년 이전의 모든 회계 연도.|  
  
 새 판매 데이터가 현재 2011 회계 연도에 추가되므로 현재 회계 연도 판매 데이터 분석에 정확하게 반영되도록 매일 데이터를 처리해야 합니다. 따라서 Sales2011 파티션은 야간에 처리됩니다.  
  
 Sales2010-2001 파티션의 데이터는 야간에 처리하지 않아도 되지만 이전 10년의 회계 연도 판매 데이터가 제품 반품 및 기타 조정으로 인해 가끔 변경될 수 있어 정기적으로 처리해야 하므로 Sales2010-2001 파티션의 데이터는 매월 처리됩니다. SalesOld 파티션의 데이터는 변경되지 않으므로 1년에 한 번만 처리됩니다.  
  
 2012 회계 연도 입력 하는 경우 새로운 Sales2012 파티션이 해당 모드의 Sales 테이블에 추가 됩니다. 그러면 Sales2011 파티션을 Sales2010-2001 파티션과 병합하여 Sales2011-2002로 이름을 변경할 수 있습니다. 2001 회계 연도의 데이터가 새 Sales2011-2002 파티션에서 제거되어 SalesOld 파티션으로 이동됩니다. 그런 다음 모든 파티션이 변경 내용을 반영하도록 처리됩니다.  
  
 조직의 테이블 형식 모델에 대 한 파티션 전략을 구현 하는 방법을 주로 됩니다에 특정 모델 데이터 처리 요구 사항 및 사용 가능한 리소스에 따라 달라 집니다.  
  
##  <a name="bkmk_permissions"></a> Permissions  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 파티션을 만들고 관리하고 처리하려면 보안 역할에 적절한 Analysis Services 사용 권한이 정의되어 있어야 합니다. 각 보안 역할의 사용 권한은 다음과 같습니다.  
  
|사용 권한|동작|  
|----------------|-------------|  
|관리자|읽기, 처리, 만들기, 복사, 병합, 삭제|  
|처리|읽기, 처리|  
|읽기 전용|읽기|  
  
 모델을 제작하는 동안 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 역할을 만드는 방법에 대한 자세한 내용은 [역할&#40;SSAS 테이블 형식&#41;](roles-ssas-tabular.md)을 참조하세요. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 배포된 테이블 형식 모델 역할의 역할 멤버를 관리하는 방법에 대한 자세한 내용은 [테이블 형식 모델 역할&#40;SSAS 테이블 형식&#41;](tabular-model-roles-ssas-tabular.md)을 참조하세요.  
  
##  <a name="bkmk_process_partitions"></a> 파티션 처리  
 **의** 파티션 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 대화 상자 또는 스크립트를 사용하여 파티션을 다른 파티션과 별개로 처리(새로 고침)할 수 있습니다. 처리 옵션은 다음과 같습니다.  
  
|모드|Description|  
|----------|-----------------|  
|기본값 처리|파티션 개체의 처리 상태를 검색하고 필요한 처리를 수행하여 처리되지 않거나 부분적으로 처리된 파티션 개체를 완전히 처리된 상태로 전달합니다. 빈 테이블 및 파티션에 대한 데이터를 로드하고 계층, 계산 열 및 관계를 작성 또는 다시 작성합니다.|  
|전체 처리|파티션 개체와 여기에 포함된 모든 개체를 처리합니다. 이미 처리된 개체에 대해 전체 처리를 실행하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 개체의 모든 데이터를 삭제한 다음 개체를 처리합니다. 개체에 구조적 변경이 발생한 경우 이러한 종류의 처리가 필요합니다.|  
|데이터 처리|계층 또는 관계를 다시 작성하거나 계산 열 및 측정값을 다시 계산하지 않고 파티션 또는 테이블에 데이터를 로드합니다.|  
|지우기 처리|파티션에서 모든 데이터를 제거합니다.|  
|증분 처리|새 데이터로 파티션을 증분 업데이트합니다.|  
  
##  <a name="bkmk_related_tasks"></a> 관련 작업  
  
|태스크|Description|  
|----------|-----------------|  
|[테이블 형식 모델 파티션 만들기 및 관리&#40;SSAS 테이블 형식&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)|배포된 테이블 형식 모델에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 파티션을 만들고 관리하는 방법에 대해 설명합니다.|  
|[테이블 형식 모델 파티션 처리&#40;SSAS 테이블 형식&#41;](process-tabular-model-partitions-ssas-tabular.md)|배포된 테이블 형식 모델에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 파티션을 처리하는 방법에 대해 설명합니다.|  
  
  
