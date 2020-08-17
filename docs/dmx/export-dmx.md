---
description: EXPORT(DMX)
title: 내보내기 (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 689ab632604d26a349dbb3f2a40d5f1b7cf8d702
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353229"
---
# <a name="export-dmx"></a>EXPORT(DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  서버의 마이닝 모델 또는 마이닝 구조 개체를 Analysis Services 백업 파일(.abf)로 추출합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>인수  
 *개체 유형*  
 선택 사항입니다. 마이닝 모델 또는 마이닝 구조 중 내보낼 개체의 유형입니다.  
  
 *개체 이름*  
 (선택 사항) 내보낼 개체 이름입니다.  
  
 *filename*  
 문자열로 내보낼 파일의 이름과 위치입니다.  
  
## <a name="remarks"></a>설명  
 문에서 마이닝 모델을 지정하는 경우 결과 파일에는 연결된 마이닝 구조도 포함됩니다. 문에서 **종속성**을 지정 하는 경우 개체를 처리 하는 데 필요한 모든 개체 (예: 데이터 원본 및 데이터 원본 뷰)는 .abf 파일에 포함 됩니다.  
  
 데이터베이스에서 개체를 내보내거나 가져오려면 데이터베이스 관리자 또는 서버 관리자 여야 합니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="export-mining-structure-example"></a>마이닝 구조 내보내기 예  
 다음 예에서는 Targeted Mailing 및 Forecasting 마이닝 구조와 Association 마이닝 모델을 특정 파일 위치로 내보냅니다. Association 모델은 Market Basket 마이닝 구조의 일부이므로 이 예에서는 Market Basket 구조도 내보냅니다. **마이닝 구조가**아닌 **마이닝 모델**을 사용 하 여 연결 모델을 내보냈지만 시장 바구니 마이닝 구조의 일부로 존재할 수 있는 다른 모든 마이닝 모델은 내보내지지 않습니다.  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>마이닝 모델 내보내기 예  
 다음 예에서는 Association 마이닝 모델을 지정한 파일 위치로 내보냅니다. 문이 **종속성을 사용**하 여를 지정 하기 때문에 데이터 원본 및 데이터 원본 뷰 개체도 .abf 파일에 포함 됩니다.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX &#40;&#41;가져오기 ](../dmx/import-dmx.md)   
 [데이터 마이닝 개체 내보내기 및 가져오기](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
