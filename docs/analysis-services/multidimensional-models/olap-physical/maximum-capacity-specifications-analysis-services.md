---
title: "최대 용량 사양 (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb411a22638d709e633504675bd91dbcfa835810
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="maximum-capacity-specifications-analysis-services"></a>최대 용량 사양 (Analysis Services)
  다음 표에서는 여러 다른 서버 배포 모드에서 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 구성 요소에 정의된 다양한 개체의 최대 크기 및 개수를 보여 줍니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [다차원 및 데이터 마이닝 (DeploymentMode = 0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode = 1)](#bkmk_sharepoint)  
  
 [테이블 형식 (DeploymentMode = 2)](#bkmk_vertipaq)  
  
##  <a name="bkmk_OLAP"></a>다차원 및 데이터 마이닝 (DeploymentMode = 0)  
 데이터와 메타데이터가 저장되는 MOLAP 저장소 모드에서는 파일 크기에 대한 추가적인 물리적 제한이 있습니다. 기본적으로 문자열 저장소 파일의 최대 크기는 4GB입니다. 더 큰 문자열 저장소 파일이 필요한 경우 다른 문자열 저장소 아키텍처를 지정할 수 있습니다. 자세한 내용은 참조 [차원 및 파티션에 대 한 문자열 저장소 구성](../../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md)합니다.  
  
|개체|최대 크기/개수|  
|------------|----------------------------|  
|인스턴스의 데이터베이스|2^31-1 = 2,147,483,647|  
|데이터베이스의 차원|2^31-1 = 2,147,483,647|  
|차원의 특성|2^31-1 = 2,147,483,647|  
|차원 특성의 멤버|2^31-1 = 2,147,483,647|  
|차원의 사용자 정의 계층|2^31-1 = 2,147,483,647|  
|사용자 정의 계층 수준|2^31-1 = 2,147,483,647|  
|데이터베이스의 큐브|2^31-1 = 2,147,483,647|  
|큐브의 측정값 그룹|2^31-1 = 2,147,483,647|  
|측정값 그룹의 측정값|2^31-1 = 2,147,483,647|  
|큐브의 계산|2^31-1 = 2,147,483,647|  
|큐브의 KPI|2^31-1 = 2,147,483,647|  
|큐브의 동작|2^31-1 = 2,147,483,647|  
|큐브의 파티션|2^31-1 = 2,147,483,647|  
|큐브의 번역|2^31-1 = 2,147,483,647|  
|파티션의 집계|2^31-1 = 2,147,483,647|  
|쿼리에서 반환된 셀|2^31-1 = 2,147,483,647|  
|원본 쿼리의 레코드 크기|64K|  
|개체 이름의 길이|최대 100 자|  
|데이터 마이닝 모델 특성 열의 고유한 최대 상태 수|2^31-1 = 2,147,483,647|  
|고려되는 최대 특성 수(기능 선택)|2^31-1 = 2,147,483,647|  
  
 개체 이름 지정 지침에 대 한 자세한 내용은 참조 [ASSL 개체 및 개체 특징](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)합니다.  
  
 온라인 분석 처리 (OLAP) 및 데이터 마이닝의 데이터 원본 제한에 대 한 자세한 내용은 참조 하세요. [지원 데이터 원본 &#40; SSAS-다차원 데이터 &#41; ](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md), [데이터 원본 &#40; 지원 SSAS-다차원 데이터 &#41; ](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md), 및 [ASSL 개체 및 개체 특징](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)합니다.  
  
##  <a name="bkmk_sharepoint"></a>SharePoint (DeploymentMode = 1)  
  
|개체|최대 크기/개수|  
|------------|----------------------------|  
|인스턴스의 데이터베이스|2^31-1 = 2,147,483,647|  
|데이터베이스의 테이블|2^31-1 = 2,147,483,647|  
|테이블의 열|2^31-1 = 2,147,483,647<br /><br /> **경고:** 동일한 테이블에 연결 된 계산 열 및 전체 테이블의 열 개수 측정값의 총 수에 따라 달라 집니다.<br /><br /> 테이블의 '열 + 측정값 + 계산 열' 개수의 최대값은 2^31-1 = 2,147,483,647입니다.|  
|테이블의 행|제한 없음<br /><br /> **경고:** 제한이 단일 열이 없는 1,999,999,997 개 이상의 고유 값에 포함 될 수 있습니다.|  
|테이블의 계층|2^31-1 = 2,147,483,647|  
|계층의 수준|2^31-1 = 2,147,483,647|  
|관계|2^31-1 = 2,147,483,647|  
|테이블의 키 열|2^31-1 = 2,147,483,647|  
|테이블의 측정값|2^31-1 = 2,147,483,647<br /><br /> **경고:** 동일한 테이블에 연결 된 계산 열 및 테이블의 총 측정값 개수 열의 총 수에 따라 달라 집니다.<br /><br /> 테이블의 '열 + 측정값 + 계산 열' 개수의 최대값은 2^31-1 = 2,147,483,647입니다.|  
|테이블의 계산 열|2^31-1 = 2,147,483,647<br /><br /> **경고:** 동일한 테이블에 연결 된 측정값 및 테이블의 계산 된 열의 총 수 열의 총 수에 따라 달라 집니다.<br /><br /> 테이블의 '열 + 측정값 + 계산 열' 개수의 최대값은 2^31-1 = 2,147,483,647입니다.|  
|쿼리에서 반환된 셀|2^31-1 = 2,147,483,647|  
|원본 쿼리의 레코드 크기|64K|  
|개체 이름의 길이|최대 100 자|  
  
##  <a name="bkmk_vertipaq"></a>테이블 형식 (DeploymentMode = 2)  
다음은 이론적 제한 합니다. 성능에 더 낮은 숫자 낮아집니다.   

|개체|최대 크기/개수|  
|------------|----------------------------|  
|인스턴스의 데이터베이스|16,000|  
|데이터베이스의 테이블 및 열의 총된 수|16,000|  
|테이블의 행|제한 없음<br /><br /> **경고:** 테이블의 단일 열 1,999,999,997 개 이상의 고유 값은 제한이 있습니다.|  
|테이블의 계층|15,999|  
|계층의 수준|15,999|  
|관계|8,000|  
|모든 테이블의 키 열|15,999|  
|한 테이블의 측정값|2^31-1 = 2,147,483,647|  
|쿼리에서 반환된 셀|2^31-1 = 2,147,483,647|  
|원본 쿼리의 레코드 크기|64K|  
|개체 이름의 길이|문자 수가 512 개|  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 인스턴스의 서버 모드 확인](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [일반 속성](../../../analysis-services/server-properties/general-properties.md)  
  
  

