---
title: "가장 옵션 설정 (SSAS-다차원) | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.sqlserverstudio.impersonationinfo.f1
helpviewer_keywords: Impersonation Information dialog box
ms.assetid: 8e127f72-ef23-44ad-81e6-3dd58981770e
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b448d78a897c6e7c6aa6973b6e61b92ff7a9aade
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="set-impersonation-options-ssas---multidimensional"></a>가장 옵션 설정(SSAS - 다차원)
  Analysis Services 모델에서 **data source** 개체를 만들 때 구성해야 하는 설정 중 하나는 가장 옵션입니다. 이 옵션은 Analysis Services에서 OLE DB 데이터 공급자를 로드하거나 로밍 프로필을 지원하는 환경에서 사용자 프로필 정보를 분석하는 등 연결과 관련된 로컬 작업을 수행할 때 특정 Windows 사용자 계정의 ID를 가장할지 여부를 결정합니다.  
  
 Windows 인증을 사용하는 연결의 경우 가장 옵션에 따라 외부 데이터 원본에서 쿼리를 실행할 사용자 ID도 결정됩니다. 예를 들어 가장 옵션을 **contoso\dbuser**로 설정하면 처리 중 데이터를 검색하는 데 사용되는 쿼리가 데이터베이스 서버에서 **contoso\dbuser** 로 실행됩니다.  
  
 이 항목에서는 데이터 원본 개체를 구성할 때 **가장 정보** 대화 상자에서 가장 옵션을 설정하는 방법에 대해 설명합니다.  
  
## <a name="set-impersonation-options-in-sql-server-data-tools"></a>SQL Server Data Tools에서 가장 옵션 설정  
  
1.  솔루션 탐색기에서 데이터 원본을 두 번 클릭하여 데이터 원본 디자이너를 엽니다.  
  
2.  데이터 원본 디자이너에서 **가장 정보** 탭을 클릭합니다.  
  
3.  이 항목의 [가장 옵션](#bkmk_options) 에 설명된 옵션을 선택합니다.  
  
## <a name="set-impersonation-options-in-management-studio"></a>Management Studio에서 가장 옵션 설정  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 다음과 같은 대화 상자의 속성에 대한 줄임표( **...** ) 단추를 클릭하여**가장 정보**대화 상자를 엽니다.  
  
-   **데이터베이스 속성** 대화 상자, 데이터 원본 가장 정보 속성  
  
-   **데이터 원본 속성** 대화 상자, 가장 정보 속성  
  
-   **어셈블리 속성** 대화 상자, 가장 정보 속성  
  
##  <a name="bkmk_options"></a> 가장 옵션  
 대화 상자에서 모든 옵션을 사용할 수는 있지만 일부 경우에는 일부 옵션이 적절하지 않을 수 있습니다. 다음 정보를 사용하여 상황에 가장 적합한 옵션을 선택하십시오.  
  
 **특정 사용자 이름 및 암호 사용**  
 이 옵션을 선택는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이 형식에 지정 된 Windows 사용자 계정의 보안 자격 증명을 사용 하는 개체:  *\<도메인 이름 >*  **\\**   *\<사용자 계정 이름 >*합니다.  
  
 데이터 액세스용으로 특별히 만든 전용, 최소 권한 Windows 사용자 ID를 사용하려면 이 옵션을 선택합니다. 예를 들어 보고서에 사용되는 데이터를 검색하기 위한 일반 용도의 계정을 정기적으로 만들 경우 여기에서 해당 계정을 지정할 수 있습니다.  
  
 다차원 데이터베이스의 경우 지정한 자격 증명은 처리, ROLAP 쿼리, 아웃오브 라인 바인딩, 로컬 큐브, 마이닝 모델, 원격 파티션, 연결된 개체 및 대상과 원본 간의 동기화에 사용됩니다.  
  
 DMX OPENQUERY 문의 경우 이 옵션은 무시되고 지정한 사용자 계정 대신 현재 사용자의 자격 증명이 사용됩니다.  
  
 **서비스 계정 사용**  
 개체를 관리하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스와 연결된 보안 자격 증명을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 사용하려면 이 옵션을 선택합니다. 이 옵션이 기본 옵션입니다. 이전 릴리스에서는 이 옵션이 사용할 수 있는 유일한 옵션이었습니다. 개별 사용자 계정이 아닌 서비스 수준에서 데이터 액세스를 모니터링하려는 경우 이 옵션을 선호할 수 있습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 경우, 사용 중인 운영 체제에 따라 서비스 계정이 NetworkService이거나 특정 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대해 만들어진 기본 제공 계정일 수 있습니다. Windows 인증을 사용하는 연결에 대한 서비스 계정을 선택한 경우 이 계정에 대한 데이터베이스 로그인을 만들고 읽기 권한을 부여하십시오. 이 로그인은 처리 중 데이터를 검색하는 데 사용됩니다. 서비스 계정에 대한 자세한 내용은 [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하십시오.  
  
> [!NOTE]  
>  데이터베이스 인증을 사용할 때는 서비스가 Analysis Services에 대한 전용 가상 계정으로 실행되는 경우 **서비스 계정 사용** 가장 옵션을 선택해야 합니다. 이 계정에는 로컬 파일에 액세스할 수 있는 권한이 포함됩니다. 서비스가 NetworkService로 실행될 경우 더 나은 방법은 **로컬 로그온 허용** 권한을 갖는 최소 권한의 Windows 사용자 계정을 사용하는 것입니다. 제공하는 계정에 따라 Analysis Services 프로그램 폴더에 대한 파일 액세스 권한을 부여해야 할 수 있습니다.  
  
 다차원 데이터베이스의 경우 서비스 계정 자격 증명은 처리, ROLAP 쿼리, 원격 파티션, 연결된 개체 및 대상과 원본 간의 동기화에 사용됩니다.  
  
 DMX OPENQUERY 문, 로컬 큐브 및 마이닝 모델의 경우 서비스 계정 옵션을 선택하는 경우에도 현재 사용자의 자격 증명이 사용됩니다. 아웃오브 라인 바인딩에 대해서는 서비스 계정 옵션이 지원되지 않습니다.  
  
> [!NOTE]  
>  서비스 계정에 Analysis Services 인스턴스에 대한 관리자 권한이 없는 경우 큐브에서 데이터 마이닝 모델을 처리할 때 오류가 발생할 수 있습니다. 자세한 내용은 [마이닝 구조: 데이터 원본이 OLAP 큐브인 경우 처리 중 문제](http://go.microsoft.com/fwlink/?LinkId=251610)를 참조하세요.  
  
 **현재 사용자의 자격 증명 사용**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에서 아웃오브 라인 바인딩, DMX OPENQUERY, 로컬 큐브 및 마이닝 모델에 대해 현재 사용자의 보안 자격 증명을 사용하려면 이 옵션을 선택합니다.  
  
 로컬 큐브 및 아웃오브 라인 바인딩을 사용하는 처리를 제외하고 이 옵션은 다차원 데이터베이스에 대해 지원되지 않습니다.  
  
 **기본값** 또는 **상속**  
 대화 상자에서는 데이터베이스 수준에서 설정된 가장 옵션의 경우 **기본값** 을 사용하고, 데이터 원본 수준에서 설정된 가장 옵션의 경우 **상속** 을 사용합니다.  
  
 **데이터 원본 - 상속 옵션**  
  
 데이터 원본 수준에서 **상속** 은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 부모 개체의 가장 옵션을 사용하도록 지정합니다. 다차원 모델에서 부모 개체는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다. **상속** 옵션을 선택하면 이 데이터 원본 및 동일한 데이터베이스의 일부인 다른 데이터 원본의 가장 설정을 중앙에서 관리할 수 있습니다. 이 옵션이 의미 있는 옵션이 되려면 데이터베이스 수준에서 특정 Windows 사용자 이름 및 암호를 선택하십시오. 그렇지 않으면 데이터 원본의 **상속** 과 데이터베이스의 **기본값** 의 조합이 서비스 계정 옵션을 사용하는 것과 동일하게 됩니다.  
  
 데이터베이스 수준에서 Windows 사용자 이름 및 암호를 지정하려면 다음을 수행합니다.  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **데이터 원본 가장 정보**에서 Windows 사용자 이름 및 암호를 지정합니다.  
  
3.  각 데이터 원본을 마우스 오른쪽 단추로 클릭한 다음 해당 속성을 보고 각 데이터 원본에서 **상속** 옵션을 사용하고 있는지 확인합니다.  
  
 데이터베이스 수준의 기본 설정에 대한 자세한 내용은 [다차원 데이터베이스 속성 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)을 참조하세요.  
  
 **데이터베이스 - 기본 옵션**  

 다차원 데이터베이스의 경우 **기본값** 은 서비스 계정을 사용하고 데이터 마이닝 작업에 현재 사용자를 사용함을 의미합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 원본 만들기&#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [데이터 원본 속성 설정&#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)   

  
  
