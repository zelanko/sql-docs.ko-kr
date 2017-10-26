---
title: EXPORT (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXPORT
dev_langs:
- DMX
helpviewer_keywords:
- exporting mining models
- exporting mining structures
- mining structures [DMX], exporting
- EXPORT statement
ms.assetid: 97617071-e560-4080-81af-a80276fc0823
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bfc3e8344d1c6967185979c0970be6d49b572500
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="export-dmx"></a>EXPORT(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버의 마이닝 모델 또는 마이닝 구조 개체를 Analysis Services 백업 파일(.abf)로 추출합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>인수  
 *개체 유형*  
 (마이닝 모델 또는 마이닝 구조)을 내보낼 개체 유형의 선택 사항입니다.  
  
 *개체 이름*  
 (선택 사항) 내보낼 개체 이름입니다.  
  
 *파일 이름*  
 문자열로 내보낼 파일의 이름과 위치입니다.  
  
## <a name="remarks"></a>주의  
 문에서 마이닝 모델을 지정하는 경우 결과 파일에는 연결된 마이닝 구조도 포함됩니다. 문을 지정 하는 경우 **WITH DEPENDENCIES**, 개체 (예를 들어 데이터 원본 및 데이터 원본 뷰)를 처리 하는 데 필요한 모든 개체가.abf 파일에 포함 됩니다.  
  
 데이터베이스 여야 합니다 또는에서 개체를 가져오거나 내보내는 데 서버 관리자는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스입니다.  
  
## <a name="export-mining-structure-example"></a>마이닝 구조 내보내기 예  
 다음 예에서는 Targeted Mailing 및 Forecasting 마이닝 구조와 Association 마이닝 모델을 특정 파일 위치로 내보냅니다. Association 모델은 Market Basket 마이닝 구조의 일부이므로 이 예에서는 Market Basket 구조도 내보냅니다. 연결 모델을 사용 하 여 내보낸 부분에서는 Market Basket 마이닝 구조를 내보낼 수는 존재할 수 있는 다른 모든 마이닝 모델 **마이닝 모델**이 아니라 **마이닝 구조**합니다.  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>마이닝 모델 내보내기 예  
 다음 예에서는 Association 마이닝 모델을 지정한 파일 위치로 내보냅니다. 문을 지정 하기 때문에 **WITH DEPENDENCIES**, 데이터 원본 및 데이터 원본 뷰 개체도.abf 파일에 포함 됩니다.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>참고 항목  
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [가져오기 &#40; DMX &#41;](../dmx/import-dmx.md)   
 [데이터 마이닝 개체 내보내기 및 가져오기](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

