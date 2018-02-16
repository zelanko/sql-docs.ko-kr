---
title: "Filestore 속성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Income property
- InitialBonus property
- PercentScanPerPrice property
- FileStore properties
- BackgroundTrimCost property
- Tax property
- PerformanceTrace property
- MinimumBalance property
- UnbufferedThreshold property
- BackgroundTrimAmount property
- MaximumBalance property
- MemoryLimitMin property
- MemoryLimit property
ms.assetid: 580cf0aa-7425-4d48-aa8d-128f5b488fcd
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 24a18751c7686de2d3d3731806374fe7a6db2080
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="filestore-properties"></a>FileStore 속성
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 다음 표에 나열된 파일 저장소 서버 속성을 사용할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 이 고급 속성을 변경하면 안 됩니다. 추가 서버 속성 및 해당 속성 설정 방법에 대한 자세한 내용은 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)을 참조하세요.  
  
 **적용 대상:** 다차원 및 테이블 형식 서버 모드  
  
## <a name="properties"></a>속성  
 **MemoryLimit**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryLimitMin**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **PercentScanPerPrice**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **PerformanceTrace**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **RandomFileAccessMode**  
 데이터베이스 파일 및 캐시된 파일을 임의 파일 액세스 모드로 액세스하는지 여부를 나타내는 부울 속성입니다. 이 속성은 기본적으로 해제되어 있습니다. 기본적으로 읽기 액세스를 위해 파티션 데이터 파일을 열 때 Analysis Services는 임의 파일 액세스 플래그를 설정하지 않습니다.  
  
 특히 대용량 리소스 및 여러 NUMA 노드가 있는 고성능 시스템에서는 임의 파일 액세스를 사용하는 편이 좋습니다. 임의 액세스 모드에서 Windows는 디스크에서 시스템 파일 캐시로 데이터를 읽는 페이지 매핑 작업을 건너뛰므로 캐시 경합을 줄일 수 있습니다.  
  
 이 속성을 변경한 결과로 쿼리 성능이 향상되는지 여부를 확인하려면 비교 테스트를 실행해야 합니다. 캐시를 지우고 일반적인 실수를 피하는 등 비교 테스트 실행에 대한 최상의 방법을 보려면 [SQL Server 2008 R2 Analysis Services 작업 가이드](http://go.microsoft.com/fwlink/?LinkID=225539)를 참조하십시오. 이 속성 사용 제어에 대한 자세한 내용은 [http://support.microsoft.com/kb/2549369](http://support.microsoft.com/kb/2549369)를 참조하세요.  
  
 Management Studio에서 이 속성을 보거나 수정하려면 서버 속성 페이지에서 고급 설정 목록을 사용합니다. msmdsrv.ini 파일에서 속성을 변경할 수도 있습니다. 이 속성을 설정한 후 서버를 다시 시작하는 것이 좋습니다. 그렇지 않으면 이미 열려 있는 파일이 이전 모드로 계속 액세스됩니다.  
  
 **UnbufferedThreshold**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="memory-model-category"></a>메모리 모델 범주  
 **MemoryModel\Tax**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryModel\Income**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryModel\MaximumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryModel\MinimumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryModel\InitialBonus**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
