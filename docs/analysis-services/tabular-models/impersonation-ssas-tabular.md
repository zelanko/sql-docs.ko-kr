---
title: "Analysis Services 테이블 형식 모델에서 가장 | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: e0acafbad6d869b31b7560f059adb0a7a3e8da03
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="impersonation"></a>가장 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]이 항목에서는 테이블 형식 모델 작성자 사용 하는 방법 로그온 자격 증명은 Analysis Services에서 데이터 원본에 연결할 때를 가져오고 데이터 처리 (새로 고침) 이해를 제공 합니다.  

##  <a name="bkmk_conf_imp_info"></a>가장 구성  
 모델이 있는 위치 및 컨텍스트에 가장 정보를 구성 하는 방법을 결정 합니다. 새 모델 프로젝트를 만들 때에 가장 데이터를 가져오는 데이터 원본에 연결할 때 SQL Server Data Tools (SSDT)에 구성 됩니다. 모델을 배포한 후 SQL Server Management Studio (SSMS)를 사용 하 여 모델 데이터베이스 연결 문자열 속성의 가장을 구성할 수 있습니다. Azure Analysis Services에서 테이블 형식 모델에 대 한 SSMS를 사용할 수 있습니다 또는 **로 볼: 스크립트** json에서 Model.bim 파일을 편집 하려면 브라우저 기반 디자이너의 모드입니다.
  
##  <a name="bkmk_how_imper"></a>가장을 사용 하는 방법  
 *가장* 은 Analysis Services와 같은 서버 응용 프로그램이 클라이언트 응용 프로그램의 ID를 가장하는 기능입니다. 하지만 Analysis Services 서비스 계정을 사용 하 여 실행 서버에서 데이터 원본에 대 한 연결을 설정 하는 경우 사용 하 여 가장 데이터 가져오기 및 처리에 대 한 액세스 검사를 수행할 수 있습니다.  
  
 가장에 사용 되는 자격 증명으로 현재 로그온 자격 증명에서 서로 다릅니다. 로그온 한 사용자 자격 증명은 모델을 작성할 때 특정 클라이언트 쪽 작업에 사용 됩니다.  
  
 가장 자격 증명은 지정 하 고, 컨텍스트의 모두 로그온 한 차이점 뿐만 아니라에 확보 하는 방법을 이해 해야 사용자 자격 증명을 사용 하 고 다른 가장 자격 증명이 사용 되는 경우 유용 합니다.  
  
 **서버 쪽 자격 증명 이해**  
 
데이터를 가져오거나 처리 하는 경우 데이터 소스에 연결 하 고 데이터를 인출 가장 자격 증명이 사용 됩니다. 이 한 *서버 쪽* 작업 영역 데이터베이스를 호스팅하는 Analysis Services 서버 데이터 원본에 연결 하 고 데이터를 인출 하기 때문에 클라이언트 응용 프로그램의 컨텍스트에서 실행 되는 작업입니다.  
  
 Analysis Services 서버에 모델을 배포하는 경우 모델을 배포할 때 작업 영역 데이터베이스가 메모리에 있으면 모델을 배포할 Analysis Services 서버에 자격 증명이 전달됩니다. 사용자 자격 증명이 디스크에 저장되는 경우는 없습니다.  
  
 배포 된 모델에서 데이터 원본에서 데이터를 처리 하는 경우 데이터 원본에 연결 하 고 데이터를 인출 메모리 내 데이터베이스에 유지 되는 가장 자격 증명이 사용 됩니다. Model 데이터베이스를 관리 하는 Analysis Services 서버에서이 프로세스를 처리 하기 때문에이 역시 서버 쪽 작업입니다.  
  
 **클라이언트 쪽 자격 증명 이해**  
  
 새 모델을 작성 하거나 기존 모델에 데이터 원본 추가, 데이터 원본에 연결 하 고 선택 하면 테이블 및 뷰를 모델로 가져올 수 있습니다. 테이블 가져오기 마법사 또는 가져오기 Data\Query 디자이너 미리 보기 및 필터 기능을 가져오는 데이터의 샘플을 볼 수 있습니다. 모델에 포함될 필요가 없는 데이터를 제외하기 위해 필터를 지정할 수도 있습니다.  
  
 이와 마찬가지로 이미 만들어진 기존 모델에 대 한 사용 하면는 **테이블 속성** 테이블로 가져온 데이터를 미리 보기 및 필터 대화 상자.  
  
 미리 보기 및 필터 기능 **테이블 속성**, 및 **파티션 관리자** 대화 상자는 in-process *클라이언트 쪽* 작업, 즉,이 프로세스 동안 수행 되는 작업 작업와 데이터가; 데이터 원본에서 인출 되는 데이터 원본에 어떻게 연결 되어 다르며 서버 쪽 작업입니다. 데이터를 미리 보고 필터링하는 데 사용되는 자격 증명은 현재 로그온한 사용자의 자격 증명입니다. 실제로 자격 증명입니다. 
  
 서버 쪽 중 사용 되는 자격 증명의 구분 및 불일치로 표시 되 고 데이터 가져오기 또는 처리 (서버 쪽 작업) 중에 인출 되는 클라이언트 쪽 작업이 발생할 수 있습니다. 자격 증명 현재 로그온 된 경우 지정 된 가장 자격 증명이 서로 다른 데이터에에서 나와 있는 미리 보기 및 필터 기능 또는 **테이블 속성** 대화 상자와 가져오는 동안 인출 된 데이터 또는 프로세스는 데이터 원본에 필요한 자격 증명에 따라 달라질 수 있습니다.  
  
> [!IMPORTANT]  
>  모델을 작성할 때으로 로그온 자격 증명을 확인 하며 가장에 대 한 지정 된 자격 증명 데이터 원본에서 데이터를 인출할 수 있는 권한이 충분 합니다.  
  
##  <a name="bkmk_imp_info_options"></a> 옵션  
 가장을 구성 하거나 기존 데이터 원본 연결에 대 한 속성을 편집할 때 다음 옵션 중 하나를 지정 합니다.  
  
**1400 이상에 대 한 테이블 형식 모델**
 
|옵션|Description|  
|------------|-----------------|  
|**계정 가장**|모델 사용 가져오거나 데이터 원본에서 데이터를 처리 하는 Windows 사용자 계정을 지정 합니다. 다음과 같은 형식을 사용 하 여 도메인 및 사용자 계정의 이름을:**\<도메인 이름 >\\< 사용자 계정 이름을\>**합니다.|  
|**현재 사용자를 가장**|요청을 보낸 사용자에 게의 id를 사용 하 여 데이터 원본에서 데이터에 액세스 해야 지정 합니다. 이 모드는 직접 쿼리 모드에만 적용 됩니다.|  
|**Id를 가장**|데이터 원본에 액세스 하려면 사용자 이름을 지정 하지만 계정의 암호를 지정할 필요가 없습니다. 이 모드는 Kerberos 위임을 사용 하 고 S4U 인증을 사용 하도록 지정 하는 경우에 적용 됩니다.|  
|**서비스 계정 가장**|모델 사용 하 여 모델을 관리 하는 Analysis Services 서비스 인스턴스와 연결 된 보안 자격 증명을 지정 합니다.|  
|**무인된 계정 가장**|Analysis Services 엔진 데이터에 액세스 하는 미리 구성 된 무인된 계정을 사용 하도록 지정 합니다.|  


**테이블 형식 1200 모델**
 
|옵션|Description|  
|------------|-----------------|  
|**특정 Windows 사용자 이름 및 암호**|이 옵션은 모델을 사용을 가져오거나 데이터 원본에서 데이터를 처리 하는 Windows 사용자 계정을 지정 합니다. 다음과 같은 형식을 사용 하 여 도메인 및 사용자 계정의 이름을:**\<도메인 이름 >\\< 사용자 계정 이름을\>**합니다. 테이블 가져오기 마법사를 사용하여 새 모델을 만드는 경우의 기본 옵션입니다.|  
|**서비스 계정**|이 옵션은 모델에서 모델을 관리하는 Analysis Services 서비스 인스턴스와 연결된 보안 자격 증명을 사용하도록 지정합니다.|  
  
##  <a name="bkmk_impers_sec"></a> 보안  
 가장과 함께 사용 하는 자격 증명이 메모리에 유지 VertiPaq™ 엔진에 의해입니다. 자격 증명은 작성 되지 않습니다는 디스크에 있습니다. 작업 영역 데이터베이스가 메모리에 모델을 배포할 때을 없으면 데이터 원본 및 fetch 데이터에 연결 하는 데 사용 되는 자격 증명을 입력 사용자 라는 메시지가 표시 됩니다.  
  
> [!NOTE]  
>  가장 자격 증명에 대한 Windows 사용자 계정과 암호를 지정하는 것이 좋습니다. Windows 사용자 계정은 연결 하 고 데이터 원본에서 데이터를 읽으려고 하는 데 필요한 최소한의 권한을 사용 하도록 구성할 수 있습니다.  
  

  
## <a name="see-also"></a>관련 항목:  
 [DirectQuery 모드](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [데이터 원본](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [테이블 형식 모델 솔루션 배포](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
