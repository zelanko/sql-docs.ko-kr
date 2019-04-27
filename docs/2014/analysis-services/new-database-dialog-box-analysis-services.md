---
title: 새 데이터베이스 대화 상자 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.newdatabase.f1
ms.assetid: ddc7804b-acb0-4ae4-a88f-e8cdf704c341
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1bef5adba44a5202e3cc0fc7f2eb48fae08a0e3c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743722"
---
# <a name="new-database-dialog-box-analysis-services"></a>새 데이터베이스 대화 상자(Analysis Services)
  **의** 새 데이터베이스 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 대화 상자를 사용하여 빈 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 새로 만들 수 있습니다. **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스의 **데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 선택하여 **새 데이터베이스** 대화 상자를 표시할 수 있습니다.  
  
## <a name="options"></a>변수  
  
|용어|정의|  
|----------|----------------|  
|**데이터베이스 이름**|새 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 이름을 입력합니다.|  
|**특정 사용자 이름 및 암호 사용**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에서 지정한 사용자 계정의 보안 자격 증명을 사용하려면 선택합니다. 지정한 자격 증명은 처리, ROLAP 쿼리, 아웃오브 라인 바인딩, 로컬 큐브, 마이닝 모델, 원격 파티션, 연결된 개체 및 대상과 원본 간의 동기화에 사용됩니다. 그러나 DMX OPENQUERY 문의 경우 현재 사용자의 자격 증명이 사용됩니다.|  
|**사용자 이름**|선택한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에서 사용할 사용자 계정의 도메인 및 이름을 입력합니다. 다음 형식을 사용합니다.<br /><br /> *\<도메인 이름 >* **\\**  *\<사용자 계정 이름 >*<br /><br /> 참고: 이 옵션은 경우에 사용할 수 **특정 사용자 이름 및 암호를 사용 하 여** 을 선택 합니다.|  
|**암호**|**사용자 이름**에서 지정한 사용자 계정의 암호를 입력합니다.|  
|**서비스 계정 사용**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에서 해당 데이터베이스를 관리하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서비스에 연결된 보안 자격 증명을 사용하려면 선택합니다. 서비스 계정 자격 증명은 처리, ROLAP 쿼리, 원격 파티션, 연결된 개체, 대상과 원본 간의 동기화 등에 사용됩니다. DMX OPENQUERY 문, 로컬 큐브 및 마이닝 모델의 경우 현재 사용자의 자격 증명이 사용됩니다. 아웃오브 라인 바인딩에 대해서는 이 옵션이 지원되지 않습니다.|  
|**현재 사용자의 자격 증명 사용**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에서 아웃오브 라인 바인딩, DMX OPENQUERY 문, 로컬 큐브 및 마이닝 모델에 대해 현재 사용자의 보안 자격 증명을 사용하려면 선택합니다. 처리, ROLAP 쿼리, 원격 파티션, 연결된 개체 및 대상과 원본 간의 동기화에 대해서는 이 옵션이 지원되지 않습니다.|  
|**Default**|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에 대한 기본 사용자 계정의 자격 증명을 사용하려면 선택합니다. 이 옵션은 데이터베이스의 기본 설정을 사용하여 개체를 처리하고 서버를 동기화하며 **Open Query** 데이터 마이닝 문을 실행합니다. 데이터베이스 수준에서의 기본 설정 지정에 대한 자세한 내용은 [다차원 데이터베이스 속성 설정&#40;Analysis Services&#41;](multidimensional-models/set-multidimensional-database-properties-analysis-services.md)을 참조하세요.<br /><br /> 기본적으로는 `DataSourceImpersonationInfo` 데이터베이스 속성 **서비스 계정을 사용 하 여**입니다. `DataSourceImpersonationInfo` 속성 값에 관계없이 아웃오브 라인 바인딩, ROLAP 쿼리, 로컬 큐브 및 데이터 마이닝 모델에 대해서는 현재 사용자의 자격 증명이 사용됩니다.|  
|**설명**|새 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스에 대한 설명을 입력합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [다차원 model 데이터베이스&#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
