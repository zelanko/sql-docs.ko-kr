---
title: 가장 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
author: minewiskan
ms.author: owend
ms.openlocfilehash: e04c7af85592d71d70abf8ea5f61518690599342
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938884"
---
# <a name="impersonation-ssas-tabular"></a>가장(SSAS 테이블 형식)
  이 항목에서는 테이블 형식의 모델 작성자를 대상으로 데이터 원본에 연결하여 데이터를 가져오고 처리(새로 고침)할 때 로그온 자격 증명이 Analysis Services에서 사용되는 방법에 대해 설명합니다.  
  
 이 자료에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [이점](#bkmk_how_imper)  
  
-   [Options](#bkmk_imp_info_options)  
  
-   [보안](#bkmk_impers_sec)  
  
-   [모델을 가져오는 경우의 가장](#bkmk_imp_newmodel)  
  
-   [가장 구성](#bkmk_conf_imp_info)  
  
##  <a name="benefits"></a><a name="bkmk_how_imper"></a> 이점  
 *가장* 은 Analysis Services와 같은 서버 애플리케이션이 클라이언트 애플리케이션의 ID를 가장하는 기능입니다. Analysis Services는 서비스 계정을 사용하여 실행되지만 서버에서 데이터 원본에 연결을 설정하는 경우에는 데이터 가져오기 및 처리에 대한 액세스 검사를 수행할 수 있도록 가장을 사용합니다.  
  
 가장에 사용되는 자격 증명은 현재 로그온한 사용자의 자격 증명과 다릅니다. 로그온한 사용자의 자격 증명은 모델을 작성할 때 특정 클라이언트 쪽 작업에 사용됩니다.  
  
 현재 로그온 한 사용자의 자격 증명과 다른 자격 증명을 사용 하는 컨텍스트 간의 차이점은 가장 자격 증명을 지정 하 고 보안 하는 방법을 이해 하는 것이 중요 합니다.  
  
 **서버 쪽 자격 증명 이해**  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 자격 증명은 테이블 가져오기 마법사의 **가장 정보** 페이지를 사용하거나 **기존 연결** 대화 상자의 기존 데이터 원본 연결을 편집하여 각 데이터 원본에 대해 지정됩니다.  
  
 데이터를 가져오거나 처리할 때 **가장 정보** 페이지에 지정된 자격 증명은 데이터 원본에 연결하고 데이터를 인출하는 데 사용됩니다. 이는 작업 영역 데이터베이스를 호스팅하는 Analysis Services 서버에서 데이터 원본에 연결하고 데이터를 인출하기 때문에 클라이언트 애플리케이션의 컨텍스트에서 실행되는 *서버 쪽* 작업입니다.  
  
 Analysis Services 서버에 모델을 배포하는 경우 모델을 배포할 때 작업 영역 데이터베이스가 메모리에 있으면 모델을 배포할 Analysis Services 서버에 자격 증명이 전달됩니다. 사용자 자격 증명이 디스크에 저장되는 경우는 없습니다.  
  
 배포된 모델에서 데이터 원본의 데이터를 처리할 때 메모리 내 데이터베이스에 유지되는 가장 자격 증명이 데이터 원본에 연결하고 데이터를 인출하는 데 사용됩니다. 이 프로세스는 model 데이터베이스를 관리하는 Analysis Services 서버에서 처리되기 때문에 역시 서버 쪽 작업입니다.  
  
 **클라이언트 쪽 자격 증명 이해**  
  
 새 모델을 작성하거나 기존 모델에 데이터 원본을 추가할 때 테이블 가져오기 마법사를 사용하여 데이터 원본에 연결하고 모델로 가져올 테이블과 뷰를 선택합니다. 테이블 가져오기 마법사의 **테이블 및 뷰 선택** 페이지에서 **미리 보기 및 필터** 기능을 사용하여 가져올 데이터의 샘플(50개 행으로 제한됨)을 볼 수 있습니다. 모델에 포함될 필요가 없는 데이터를 제외하기 위해 필터를 지정할 수도 있습니다.  
  
 이와 마찬가지로 이미 만들어진 기존 모델의 경우 **테이블 속성 편집** 대화 상자를 사용하여 테이블로 가져온 데이터를 미리 보고 필터링할 수 있습니다. 이 미리 보기 및 필터 기능은 테이블 가져오기 마법사의 **테이블 및 뷰 선택** 페이지에 있는 **미리 보기 및 필터** 기능과 동일합니다.  
  
 **미리 보기 및 필터** 기능과 **테이블 속성** 및 **파티션 관리자** 대화 상자는 in-process *클라이언트 쪽* 작업입니다. 즉, 이 작업 중에 수행되는 것은 서버 쪽 작업에서 수행되는 데이터 원본이 연결되고 데이터가 데이터 원본에서 인출되는 방법과 다릅니다. 데이터를 미리 보고 필터링하는 데 사용되는 자격 증명은 현재 로그온한 사용자의 자격 증명입니다. 클라이언트 쪽 작업은 항상 현재 사용자의 Windows 자격 증명을 사용 하 여 데이터 원본에 연결 합니다.  
  
 서버 쪽 작업과 클라이언트 쪽 작업 중에 사용되는 자격 증명의 이러한 구분으로 인해 **미리 보기 및 필터** 기능이나 **테이블 속성** 대화 상자(클라이언트 쪽 작업)를 사용하여 표시되는 것과 가져오기 또는 처리(서버 쪽 작업) 중에 인출되는 데이터가 일치하지 않을 수 있습니다. 현재 로그온한 사용자의 자격 증명과 지정된 가장 자격 증명이 다른 경우 **미리 보기 및 필터** 기능이나 **테이블 속성** 대화 상자에서 표시되는 데이터와 가져오기 또는 처리 중에 인출되는 데이터는 데이터 원본에 필요한 자격 증명에 따라 서로 다를 수 있습니다.  
  
> [!IMPORTANT]  
>  모델을 작성할 경우 현재 로그온한 사용자의 자격 증명과 가장에 대해 지정된 자격 증명에는 데이터 원본에서 데이터를 인출할 수 있는 충분한 권한이 있습니다.  
  
##  <a name="options"></a><a name="bkmk_imp_info_options"></a>옵션  
 가장을 구성하는 경우나 Analysis Services에서 기존 데이터 원본 연결의 속성을 편집하는 경우 다음 옵션 중 하나를 지정할 수 있습니다.  
  
|옵션|ImpersonationMode<sup>1</sup>|Description|  
|------------|-----------------------------------|-----------------|  
|**특정 Windows 사용자 이름 및 암호** <sup>2</sup>|ImpersonateWindowsUserAccount|이 옵션은 모델에서 Windows 사용자 계정을 사용하여 데이터 원본에서 데이터를 가져오거나 처리하도록 지정합니다. 사용자 계정의 도메인과 이름은 다음 형식을 사용 합니다.** \<Domain name> \\ 사용자 계정 이름 \><** 합니다. 테이블 가져오기 마법사를 사용하여 새 모델을 만드는 경우의 기본 옵션입니다.|  
|**서비스 계정**|ImpersonateServiceAccount|이 옵션은 모델에서 모델을 관리하는 Analysis Services 서비스 인스턴스와 연결된 보안 자격 증명을 사용하도록 지정합니다.|  
  
 <sup>1</sup> ImpersonationMode는 데이터 원본에서 [DataSourceImpersonationInfo 요소 &#40;&#41;](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) 속성의 값을 지정 합니다.  
  
 <sup>2</sup> 이 옵션을 사용 하는 경우 다시 부팅 하거나 작업 **영역 보존** 속성이 **메모리에서 언로드** 또는 **작업 영역에서 삭제**로 설정 되 고 모델 프로젝트가 닫히면 이후 세션에서 테이블 데이터를 처리 하려고 할 때 각 데이터 원본에 대 한 자격 증명을 입력 하 라는 메시지가 표시 됩니다. 이와 마찬가지로 배포된 model 데이터베이스가 메모리에서 제거된 경우 각 데이터 원본에 대한 자격 증명을 묻는 메시지가 표시됩니다.  
  
##  <a name="security"></a><a name="bkmk_impers_sec"></a> 보안  
 가장에서 사용되는 자격 증명은 작업 영역 데이터베이스 또는 배포된 모델을 관리하는 Analysis Services 서버와 연결된 xVelocity 메모리 내 분석 엔진(VertiPaq)™에 의해 메모리에 유지됩니다.  자격 증명이 디스크에 기록되는 경우는 없습니다. 모델이 배포될 때 작업 영역 데이터베이스가 메모리에 없으면 데이터 원본에 연결하고 데이터를 인출하는 데 사용되는 자격 증명을 입력하라는 메시지가 표시됩니다.  
  
> [!NOTE]  
>  가장 자격 증명에 대한 Windows 사용자 계정과 암호를 지정하는 것이 좋습니다. Windows 사용자 계정은 데이터 원본에 연결하고 데이터 원본에서 데이터를 읽는 데 필요한 최소한의 권한을 사용하도록 구성할 수 있습니다.  
  
##  <a name="impersonation-when-importing-a-model"></a><a name="bkmk_imp_newmodel"></a> 모델을 가져오는 경우의 가장  
 몇 가지 가장 모드를 사용하여 out-of-process 데이터 컬렉션을 지원할 수 있는 테이블 형식 모델과 달리 PowerPivot에서는 ImpersonateCurrentUser 모드만 사용합니다. PowerPivot은 항상 in-process로 실행되므로 현재 로그온한 사용자의 자격 증명을 사용하여 데이터 원본에 연결합니다. 테이블 형식 모델을 사용하는 경우 현재 로그온한 사용자의 자격 증명은 테이블 가져오기 마법사의 **미리 보기 및 필터** 기능과 **테이블 속성**보기에서만 사용됩니다. 가장 자격 증명은 데이터를 작업 영역 데이터베이스로 가져오거나 처리하는 경우 또는 데이터를 배포된 model로 가져오거나 처리하는 경우에 사용됩니다.  
  
 기존 PowerPivot 통합 문서를 가져와서 새 모델을 만드는 경우 기본적으로 모델 디자이너는 서비스 계정을 사용하도록 가장을 구성합니다(ImpersonateServiceAccount). PowerPivot에서 Windows 사용자 계정으로 가져온 모델에 대한 가장 자격 증명을 변경하는 것이 좋습니다. 모델 디자이너에서 PowerPivot 통합 문서를 가져오고 새 모델을 만든 후 **기존 연결** 대화 상자를 사용 하 여 자격 증명을 변경할 수 있습니다.  
  
 Analysis Services 서버에 있는 기존 모델에서 가져와서 새 모델을 만드는 경우 가장 자격 증명이 기존 model 데이터베이스에서 새 모델 작업 영역 데이터베이스로 전달됩니다. 필요한 경우 **기존 연결** 대화 상자를 사용하여 새 모델에 대한 자격 증명을 변경할 수 있습니다.  
  
##  <a name="configuring-impersonation"></a><a name="bkmk_conf_imp_info"></a> 가장 구성  
 모델이 있는 위치 및 컨텍스트에 따라 가장 정보를 구성하는 방법이 달라집니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 작성되는 모델의 경우 테이블 가져오기 마법사의 **가장 정보** 페이지를 사용하거나 **기존 연결** 대화 상자에서 데이터 원본 연결을 편집하여 가장 정보를 구성할 수 있습니다. 기존 연결을 보려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 **모델** 메뉴에서 **기존 연결**을 클릭합니다.  
  
 Analysis Services 서버에 배포 된 모델의 경우의 **데이터베이스 속성** 대화 상자에서 **데이터 원본 가장 정보** 속성의 줄임표 (...)를 클릭 하 여 가장 정보를 구성할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
## <a name="see-also"></a>참고 항목  
 [DirectQuery 모드 &#40;SSAS 테이블 형식&#41;](directquery-mode-ssas-tabular.md)   
 [데이터 원본 &#40;SSAS 테이블 형식&#41;](../data-sources-ssas-tabular.md)   
 [테이블 형식 모델 솔루션 배포&#40;SSAS 테이블 형식&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
