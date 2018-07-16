---
title: 캐싱 페이지, 공유 데이터 집합 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eac372e9-d2a1-48a8-bbe5-09d101df16ea
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5fdd495e3110deb2cc8c9fc7b8a4848f0252f206
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247993"
---
# <a name="caching-page-shared-datasets-report-manager"></a>캐싱 페이지, 공유 데이터 집합(보고서 관리자)
  캐싱 속성 페이지를 사용하여 공유 데이터 집합의 캐시 옵션을 설정할 수 있습니다.  
  
> [!NOTE]  
>  이 기능은 일부 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에서는 사용할 수 없습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
### <a name="to-open-the-caching-properties-page-for-a-shared-dataset"></a>공유 데이터 집합의 캐싱 속성 페이지를 열려면  
  
1.  보고서 관리자를 열고 공유 데이터 집합 속성을 구성할 보고서를 찾습니다.  
  
2.  공유 데이터 집합을 가리키고 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 목록에서 **관리**를 클릭합니다. 보고서의 일반 속성 페이지가 열립니다.  
  
4.  **캐싱** 탭을 클릭합니다.  
  
## <a name="options"></a>변수  
 **공유 데이터 집합 캐시**  
 사용자가 이 공유 데이터 집합을 사용하는 보고서를 처음에 열 때 캐시에 데이터를 임시로 복사합니다. 캐싱 기간 내에 보고서를 실행하는 이후 사용자는 데이터의 캐시된 복사본을 받게 됩니다. 캐시를 사용하면 데이터 집합 쿼리를 다시 실행하지 않고 캐시에서 바로 가져오기 때문에 일반적으로 성능이 향상됩니다.  
  
 **시간 (분)이 지나면 캐시 만료**  
 데이터의 캐시된 복사본을 저장할 시간(분)을 지정합니다. 임시 복사본이 만료된 직후부터 더 이상 캐시에서 데이터가 반환되지 않습니다. 이후에 사용자가 이 공유 데이터 집합을 사용하는 보고서를 열면 데이터 집합 쿼리가 실행되고 보고서 서버가 새로 고친 데이터의 복사본을 캐시에 저장합니다.  
  
 **다음 일정에 따라 캐시 만료**  
 캐시된 데이터가 더 이상 유효하지 않게 되며 캐시에서 제거되는 시간을 예약합니다. 일정을 공유 일정으로 지정하거나 현재 공유 데이터 집합 전용 일정으로 지정할 수 있습니다.  
  
 **데이터 집합별 일정**  
 이 데이터 집합에서만 사용되는 일정을 지정합니다.  
  
 **공유 일정**  
 보고서, 구독 및 기타 공유 데이터 집합에서 공유되는 일정을 지정합니다.  
  
 **적용**  
 변경 내용을 저장합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자 &#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)   
 [공유 데이터 집합 캐시&#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)   
 [일정](subscriptions/schedules.md)  
  
  
