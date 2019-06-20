---
title: IMPORT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4987701deb466148253c8418c88683d2dbfbc16b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62506065"
---
# <a name="import-dmx"></a>IMPORT(DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Analysis Services 백업 파일(.abf)의 마이닝 모델 또는 마이닝 구조를 서버로 로드합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>인수  
 *filename*  
 가져올 파일의 이름과 위치가 들어 있는 문자열입니다.  
  
## <a name="remarks"></a>Remarks  
 개체를 지정하지 않은 경우 .dmb 파일의 전체 내용이 로드됩니다. 서버에 없는 데이터베이스가 .dmb 파일에 포함된 경우 이 데이터베이스가 만들어집니다.  
  
 개체를 내보내거나 가져오려면 데이터베이스 관리자 또는 서버 관리자 권한이 필요합니다.  
  
## <a name="import-from-file-example"></a>파일에서 가져오기 예  
 다음 예에서는 연결 모델 및 구조가 들어 있는 파일의 전체 내용을 현재 서버로 가져옵니다.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [내보내기 &AMP;#40;DMX&AMP;#41;](../dmx/export-dmx.md)   
 [데이터 마이닝 개체 내보내기 및 가져오기](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  
