---
title: CLR 통합의 새로운 기능 (&#39;) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 45e4f0578d06eeafc545bea2b6374a37b8ef7cbc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874061"
---
# <a name="what39s-new-in-clr-integration"></a>CLR 통합의 새로운 기능&#39;
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 CLR 통합에 새로 추가된 기능은 다음과 같습니다.  
  
-   CLR 버전 4에서는 CLR 데이터베이스 개체가 더 이상 손상된 상태 예외를 catch하지 않습니다. 이러한 예외는 이제 CLR 통합 호스팅 계층에서 catch됩니다. 이러한 예외는 CLR 데이터베이스 구성 요소에서 코드 특성 ([\<legacyCorruptedStateExceptionsPolicy> 요소](https://go.microsoft.com/fwlink/?LinkId=204954))을 설정 하 여 계속 catch 할 수 있습니다. 그러나 손상된 상태 예외가 발생할 때 결과를 신뢰할 수 없으므로 이 방법은 사용하지 않는 것이 좋습니다.  
  
-   [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]의 엄격한 보안 요구 사항으로 인해 CLR 데이터베이스 구성 요소가 CLR 버전 2.0에 정의된 코드 액세스 보안 모델을 계속해서 사용합니다.  
  
-   CLR 버전 4에서 `System.TimeSpan` 값에 형식 오류가 있으면 `System.FormatExceptions`가 생성됩니다. CLR 버전 4 이전에는 `System.TimeSpan` 값에 형식 오류가 있어도 무시되었습니다. CLR 버전 4 이전의 동작에 의존하는 데이터베이스 애플리케이션을 실행하려면 데이터베이스 호환성 수준(`ALTER DATABASE Compatibility Level`)이 100 이하여야 합니다. 자세한 내용은 [<TimeSpan_LegacyFormatMode> 요소](https://go.microsoft.com/fwlink/?LinkId=205109)를 참조 하세요.  
  
-   CLR 버전 4는 유니코드 5.1을 지원하므로 일부 악센트 표시 및 기호가 관련된 정렬 작업이 개선됩니다. 애플리케이션이 레거시 정렬 동작에 의존하는 경우에는 호환성 문제가 발생할 수 있습니다. 레거시 정렬을 사용하도록 설정하려면 데이터베이스 호환성 수준(`ALTER DATABASE Compatibility Level`)을 100 이하로 설정해야 합니다. 이를 지원하기 위해 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서는 .NET Framework 4 디렉터리(C:\Windows\Microsoft.NET\Framework\v4.0.30319)에 sort00001000.dll을 설치합니다. 자세한 내용은 [ \<CompatSortNLSVersion> 요소](https://go.microsoft.com/fwlink/?LinkId=205110)를 참조 하세요.  
  
-   다음 열 `total_processor_time_ms`이 [sys. dm_clr_appdomains](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql)에 추가 되었습니다., `total_allocated_memory_kb`및 `survived_memory_kb`.  
  
  
