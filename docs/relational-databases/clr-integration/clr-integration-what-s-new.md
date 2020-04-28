---
title: CLR 통합의 새로운 기능 | Microsoft Docs
description: Clr Microsoft SQL Server clr 통합 이라고 합니다. 이 문서에서는 SQL Server 2012에서 CLR 통합의 새로운 기능에 대해 설명 합니다.
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: d27bf0d925d3a98dda488fb85aff7446434cc8ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488092"
---
# <a name="clr-integration---what39s-new"></a>CLR 통합-새로운&#39;s
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 CLR 통합에 새로 추가된 기능은 다음과 같습니다.  
  
-   CLR 버전 4에서는 CLR 데이터베이스 개체가 더 이상 손상된 상태 예외를 catch하지 않습니다. 이러한 예외는 이제 CLR 통합 호스팅 계층에서 catch됩니다. 이러한 예외는 CLR 데이터베이스 구성 요소에서 코드 특성 ([\<legacyCorruptedStateExceptionsPolicy> 요소](https://go.microsoft.com/fwlink/?LinkId=204954))을 설정 하 여 계속 catch 할 수 있습니다. 그러나 손상된 상태 예외가 발생할 때 결과를 신뢰할 수 없으므로 이 방법은 사용하지 않는 것이 좋습니다.  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 엄격한 보안 요구 사항으로 인해 CLR 데이터베이스 구성 요소가 CLR 버전 2.0에 정의된 코드 액세스 보안 모델을 계속해서 사용합니다.  
  
-   CLR 버전 4에서 **timespan.zero** 값의 형식 오류는 **system.object 예외**를 생성 합니다. CLR 버전 4 이전에는 **TimeSpan** 값에 형식 오류가 무시 되었습니다. CLR 버전 4 이전의 동작에 의존 하는 데이터베이스 응용 프로그램은 데이터베이스 호환성 수준 (**ALTER Database Compatibility level**)에서 100 이하로 실행 해야 합니다. 자세한 내용은 [<TimeSpan_LegacyFormatMode> 요소](https://go.microsoft.com/fwlink/?LinkId=205109)를 참조 하세요.  
  
-   CLR 버전 4는 유니코드 5.1을 지원하므로 일부 악센트 표시 및 기호가 관련된 정렬 작업이 개선됩니다. 애플리케이션이 레거시 정렬 동작에 의존하는 경우에는 호환성 문제가 발생할 수 있습니다. 레거시 정렬을 사용 하려면 데이터베이스 호환성 수준 (**ALTER Database 호환성 수준**)을 100 이하로 설정 해야 합니다. 이를 지원하기 위해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서는 .NET Framework 4 디렉터리(C:\Windows\Microsoft.NET\Framework\v4.0.30319)에 sort00001000.dll을 설치합니다. 자세한 내용은 [ \<CompatSortNLSVersion> 요소](https://go.microsoft.com/fwlink/?LinkId=205110)를 참조 하세요.  
  
-   다음 열이 [dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)에 추가 되었습니다. **total_processor_time_ms**, **total_allocated_memory_kb**및 **survived_memory_kb**.  
  
  
