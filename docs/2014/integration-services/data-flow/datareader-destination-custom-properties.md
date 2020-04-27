---
title: DataReader 대상 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 948ebbc696048915662caaa24b791e6258c459be
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827625"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 대상 사용자 지정 속성
  DataReader 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 DataReader 대상의 사용자 지정 속성을 설명합니다. `DataReader`를 제외한 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 대상의 클래스 이름입니다.|  
|FailOnTimeout|부울|`ReadTimeout`이 발생하는 경우의 실패 여부를 나타냅니다. 이 속성의 기본값은 **False**입니다.|  
|ReadTimeout|정수|시간이 초과되기 전의 시간(밀리초)입니다. 이 속성의 기본값은 30000(30초)입니다.|  
  
 DataReader 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [DataReader Destination](datareader-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Common Properties](../common-properties.md)  
  
  
