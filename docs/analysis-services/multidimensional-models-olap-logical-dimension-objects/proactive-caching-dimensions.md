---
title: "자동 관리 캐싱 (차원) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], proactive caching
- proactive caching [Analysis Services]
ms.assetid: 7d57fe93-6e5f-4a50-844f-dd2bbdbb94a5
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 619a731b497f40cb359d61e5fa0c4d987d1fae72
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="proactive-caching-dimensions"></a>자동 관리 캐싱(차원)
  자동 관리 캐싱은 OLAP 개체에 자동 MOLAP 캐시 생성 및 관리 기능을 제공합니다. 큐브는 데이터베이스로부터 알림을 수신하는 즉시 데이터베이스에 있는 데이터의 변경 내용을 통합합니다. 자동 관리 캐싱의 목표는 ROLAP에서 제공하는 즉시성과 관리 용이성을 유지하면서 기존 MOLAP의 성능을 제공하는 것입니다.  
  
 단순 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체는 타이밍 사양과 테이블 알림으로 구성되어 있습니다. 타이밍 사양은 변경 알림을 수신한 후 캐시를 업데이트하는 시간을 정의합니다. 테이블 알림은 데이터 테이블과 <xref:Microsoft.AnalysisServices.ProactiveCaching> 개체 간의 알림 스키마를 정의합니다.  
  
  

