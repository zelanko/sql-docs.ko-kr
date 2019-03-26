---
title: DataReader 대상 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 701fbe45a5f6e7f1d0056aa4d549b1ba32246459
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58279287"
---
# <a name="datareader-destination-custom-properties"></a>DataReader 대상 사용자 지정 속성
  DataReader 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 DataReader 대상의 사용자 지정 속성을 설명합니다. **DataReader** 를 제외한 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|설명|  
|-------------------|---------------|-----------------|  
|DataReader|String|DataReader 대상의 클래스 이름입니다.|  
|FailOnTimeout|Boolean|**ReadTimeout** 이 발생하는 경우의 실패 여부를 나타냅니다. 이 속성의 기본값은 **False**입니다.|  
|ReadTimeout|정수|시간이 초과되기 전의 시간(밀리초)입니다. 이 속성의 기본값은 30000(30초)입니다.|  
  
 DataReader 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [DataReader Destination](../../integration-services/data-flow/datareader-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
