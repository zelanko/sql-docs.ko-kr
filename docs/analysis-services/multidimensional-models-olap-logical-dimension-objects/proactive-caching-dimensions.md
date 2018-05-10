---
title: 자동 관리 캐싱 (차원) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf1dee51b8ff659257eb290907dafa8536c386f1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="proactive-caching-dimensions"></a>자동 관리 캐싱(차원)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  자동 관리 캐싱은 OLAP 개체에 자동 MOLAP 캐시 생성 및 관리 기능을 제공합니다. 큐브는 데이터베이스로부터 알림을 수신하는 즉시 데이터베이스에 있는 데이터의 변경 내용을 통합합니다. 자동 관리 캐싱의 목표는 ROLAP에서 제공하는 즉시성과 관리 용이성을 유지하면서 기존 MOLAP의 성능을 제공하는 것입니다.  
  
 단순 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체는 타이밍 사양과 테이블 알림으로 구성되어 있습니다. 타이밍 사양은 변경 알림을 수신한 후 캐시를 업데이트하는 시간을 정의합니다. 테이블 알림은 데이터 테이블과 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체 간의 알림 스키마를 정의합니다.  
  
  
