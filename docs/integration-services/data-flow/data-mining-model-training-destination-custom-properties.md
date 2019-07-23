---
title: 데이터 마이닝 모델 학습 대상 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f0a70216-fdac-44ae-af29-35f65626217c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 028aceabe89183d4aec0c75606f6fe58c91192d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049464"
---
# <a name="data-mining-model-training-destination-custom-properties"></a>데이터 마이닝 모델 학습 대상 사용자 지정 속성

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  데이터 마이닝 모델 학습 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 데이터 마이닝 모델 학습 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성|데이터 형식|설명|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|연결 관리자의 고유 식별자입니다.|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 대한 연결 문자열입니다.|  
|ObjectRef|String|변환에서 사용하는 데이터 마이닝 구조를 식별하는 XML 태그입니다.|  
  
 데이터 마이닝 모델 학습 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Data Mining Model Training Destination](../../integration-services/data-flow/data-mining-model-training-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
