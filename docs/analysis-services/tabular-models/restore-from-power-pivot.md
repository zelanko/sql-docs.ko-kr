---
title: "파워 피벗에서 복원 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2cc8322e9a7208189ec7a8630e79a47baecaeb92
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="restore-from-power-pivot"></a>파워 피벗에서 복원
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]복원을 사용할 수 있습니다 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (테이블 형식 모드에서 실행 중), Analysis Services 인스턴스에서 새 테이블 형식 모델 데이터베이스를 만들려면 SQL Server Management Studio에서 기능 또는 기존 데이터베이스를 복원는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서 (.xlsx)입니다.  
  
> [!NOTE]  
>  SQL Server Data Tools의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 프로젝트 템플릿에서 가져오기 옵션도 비슷한 기능을 제공합니다. 자세한 내용은 [파워 피벗에서 가져오기&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)를 참조하세요.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서 복원을 사용할 때는 다음 사항에 유의해야 합니다.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서 복원을 사용하려면 Analysis Services 인스턴스에서 서버 관리자 역할의 멤버로 로그온해야 합니다.  
  
-   Analysis Services 인스턴스 서비스 계정은 복원할 통합 문서 파일에 대한 읽기 권한을 가지고 있어야 합니다.  
  
-   기본적으로 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서 데이터베이스를 복원하면 테이블 형식 model 데이터베이스의 데이터 원본 가장 정보 속성이 기본값으로 설정되어 Analysis Services 인스턴스 서비스 계정이 지정됩니다. 가장 자격 증명을 데이터베이스 속성의 Windows 사용자 계정으로 변경하는 것이 좋습니다. 자세한 내용은 [가장&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)을 참조하세요.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 모델의 데이터는 Analysis Services 인스턴스의 기존 또는 새 테이블 형식 model 데이터베이스로 복사됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 연결된 테이블이 있는 경우 해당 테이블은 새 테이블에 붙여넣기를 사용하여 만드는 테이블과 마찬가지로 데이터 원본이 없는 테이블로 다시 만들어집니다.  
  
### <a name="to-restore-from-power-pivot"></a>파워 피벗에서 복원하려면  
  
1.  SSMS의 복원하려는 Active Directory 인스턴스에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서 복원**을 클릭합니다.  
  
2.  **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에서 복원** 대화 상자의 **복원 원본**에 있는 **백업 파일**에서 **찾아보기**를 클릭한 다음 복원할 .abf 또는 .xslx 파일을 선택합니다.  
  
3.  **대상 복원**의 **데이터베이스 복원**에 새 데이터베이스 또는 기존 데이터베이스의 이름을 입력합니다. 이름을 지정하지 않으면 통합 문서의 이름이 사용됩니다.  
  
4.  **저장소 위치**에서 **찾아보기**를 클릭한 다음 데이터베이스를 저장할 위치를 선택합니다.  
  
5.  **옵션**에서 **보안 정보 포함** 을 선택합니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에서 복원할 때는 이 설정이 적용되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [테이블 형식 model 데이터베이스&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)   
 [파워 피벗에서 가져오기&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)  
  
  
