---
title: DataReader 대상 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bdbfcd41afdfe7fd27651efbabf0983a56c786e0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187443"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 대상 사용자 지정 속성
  DataReader 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 DataReader 대상의 사용자 지정 속성을 설명합니다. 모든 속성을 제외 하 고 `DataReader` 읽기/쓰기입니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 대상의 클래스 이름입니다.|  
|FailOnTimeout|Boolean|`ReadTimeout`이 발생하는 경우의 실패 여부를 나타냅니다. 이 속성의 기본값은 **False**입니다.|  
|ReadTimeout|정수|시간이 초과되기 전의 시간(밀리초)입니다. 이 속성의 기본값은 30000(30초)입니다.|  
  
 DataReader 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [DataReader Destination](datareader-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Common Properties](../common-properties.md)  
  
  
