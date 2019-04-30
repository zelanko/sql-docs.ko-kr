---
title: XTP 가상 프로세서 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 14c34bb0d7520b914d8dbfc1cfc8174341722ece
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150981"
---
# <a name="xtp-phantom-processor"></a>XTP 가상 프로세서
  XTP 가상 프로세서 성능 개체에는 XTP 엔진의 가상 처리 하위 시스템과 관련된 카운터가 포함됩니다. 이 구성 요소는 SERIALIZABLE 격리 수준에서 실행되는 트랜잭션에서 가상 행을 검색합니다.  
  
 이 표에서는 **XTP 가상 프로세서** 카운터에 대해 설명합니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|**Dusty corner scan retries/sec (Phantom-issued)**|가상 프로세서에 의해 실행된 불량 영역 청소(dusty corner sweeps) 중 발생한 초당 검색 재시도 횟수입니다(평균). 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|  
|**Phantom expired rows removed/sec**|가상 검사에 의해 제거된 만료된 초당 행 수입니다(평균).|  
|**Phantom expired rows touched/sec**|가상 검사에 의해 처리된 만료된 초당 행 수입니다(평균).|  
|**Phantom expiring rows touched/sec**|가상 검사에 의해 처리된 만료되는 초당 행 수입니다(평균).|  
|**Phantom rows touched/sec**|가상 검사에 의해 처리된 초당 행 수입니다(평균).|  
|**Phantom scans started/sec**|초당 시작된 가상 검사 수입니다(평균).|  
  
## <a name="see-also"></a>관련 항목  
 [XTP &#40;메모리 내 OLTP&#41; 성능 카운터](../../integration-services/performance/performance-counters.md)  
  
  
