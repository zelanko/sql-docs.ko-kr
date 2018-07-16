---
title: 새로운&#39;CLR 통합의 새로운 | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 55cb6537db540fb5d916b72cb1b469dc3846f419
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356215"
---
# <a name="clr-integration---what39s-new"></a>CLR 통합-새로운&#39;새로운
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 CLR 통합에 새로 추가된 기능은 다음과 같습니다.  
  
-   CLR 버전 4에서는 CLR 데이터베이스 개체가 더 이상 손상된 상태 예외를 catch하지 않습니다. 이러한 예외는 이제 CLR 통합 호스팅 계층에서 catch됩니다. 이러한 예외 수 코드 특성을 설정 하 여 여전히 CLR 데이터베이스 구성 요소에서 발생 하는 수 ([\<legacyCorruptedStateExceptionsPolicy > 요소](http://go.microsoft.com/fwlink/?LinkId=204954)). 그러나 손상된 상태 예외가 발생할 때 결과를 신뢰할 수 없으므로 이 방법은 사용하지 않는 것이 좋습니다.  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]의 엄격한 보안 요구 사항으로 인해 CLR 데이터베이스 구성 요소가 CLR 버전 2.0에 정의된 코드 액세스 보안 모델을 계속해서 사용합니다.  
  
-   Clr 버전 4에 형식 오류가 **System.TimeSpan** 값 생성을 **System.FormatExceptions**합니다. 이전에 형식 오류가 clr 버전 4 **System.TimeSpan** 값 무시 되었습니다. CLR 버전 4 이전의 동작에 의존 하는 데이터베이스 응용 프로그램 데이터베이스 호환성 수준으로 실행 해야 합니다 (**ALTER DATABASE 호환성 수준**)이 100입니다. 자세한 내용은 [< TimeSpan_LegacyFormatMode > 요소](http://go.microsoft.com/fwlink/?LinkId=205109)합니다.  
  
-   CLR 버전 4는 유니코드 5.1을 지원하므로 일부 악센트 표시 및 기호가 관련된 정렬 작업이 개선됩니다. 응용 프로그램이 레거시 정렬 동작에 의존하는 경우에는 호환성 문제가 발생할 수 있습니다. 레거시 정렬을 데이터베이스 호환성 수준을 사용 하도록 설정 하려면 (**ALTER DATABASE 호환성 수준**) 100 이하로 설정 해야 합니다. 이를 지원하기 위해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서는 .NET Framework 4 디렉터리(C:\Windows\Microsoft.NET\Framework\v4.0.30319)에 sort00001000.dll을 설치합니다. 자세한 내용은 [ \<CompatSortNLSVersion > 요소](http://go.microsoft.com/fwlink/?LinkId=205110)합니다.  
  
-   다음 열에 추가 되었습니다 [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**합니다 **total_allocated_memory_kb**, 및 **survived_ memory_kb**합니다.  
  
  
