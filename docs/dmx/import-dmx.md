---
title: IMPORT (DMX) | Microsoft Docs
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
- IMPORT
dev_langs:
- DMX
helpviewer_keywords:
- IMPORT statement
- mining structures [DMX], importing
ms.assetid: c053bc88-2daf-4ebb-81d7-5a330250536d
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5510631430ed75a04dd9685d1197f60c64a85aa8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="import-dmx"></a>IMPORT(DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Analysis Services 백업 파일(.abf)의 마이닝 모델 또는 마이닝 구조를 서버로 로드합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>인수  
 *파일 이름*  
 가져올 파일의 이름과 위치가 들어 있는 문자열입니다.  
  
## <a name="remarks"></a>주의  
 개체를 지정하지 않은 경우 .dmb 파일의 전체 내용이 로드됩니다. 서버에 없는 데이터베이스가 .dmb 파일에 포함된 경우 이 데이터베이스가 만들어집니다.  
  
 개체를 내보내거나 가져오려면 데이터베이스 관리자 또는 서버 관리자 권한이 필요합니다.  
  
## <a name="import-from-file-example"></a>파일에서 가져오기 예  
 다음 예에서는 연결 모델 및 구조가 들어 있는 파일의 전체 내용을 현재 서버로 가져옵니다.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [내보내기 &#40; DMX &#41;](../dmx/export-dmx.md)   
 [데이터 마이닝 개체 내보내기 및 가져오기](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

