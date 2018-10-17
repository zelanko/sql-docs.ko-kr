---
title: CPU 사용 정책에서 노이즈 줄이기(SQL Server 유틸리티) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql13.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5d88ea1e1cb3c7339715ddc5eea02eebf964f277
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809781"
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>CPU 사용 정책에서 노이즈 줄이기(SQL Server 유틸리티)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티 리소스 사용 정책에서 노이즈 및 원치 않는 위반이 보고되는 것을 줄이려면 다음 정책을 사용합니다.  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-overutilized"></a>프로세서 사용이 얼마나 자주 위반되면 사용 과다로 보고됩니까?  
 평가 기간 및 위반 비율 허용 오차는 모두 유틸리티 탐색기의 **유틸리티 관리** 노드에 있는 **정책** 탭 설정에서 구성할 수 있습니다. 정책을 변경하려면 정책 설명 오른쪽에 있는 슬라이더 컨트롤을 사용한 다음 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   데이터 수집 간격은 15분입니다. 이 값은 구성할 수 없습니다.  
  
-   프로세서 사용 정책의 기본 상한 임계값은 70%입니다. 옵션 범위는 0%에서 100% 사이입니다.  
  
-   프로세서 사용 과다의 기본 평가 기간은 1시간입니다. 옵션 범위는 1시간에서 1주일 사이입니다.  
  
-   CPU 과다 사용이 보고되는 데이터 요소의 기본 위반 비율은 20%입니다. 옵션 범위는 0%에서 100% 사이입니다.  
  
 예를 들어 기본값에 따라 매시간 데이터 요소 4개가 수집되고 정책 임계값은 20%라고 가정해 보겠습니다. 따라서 기본적으로 수집 기간 1시간 동안 데이터 요소 4개의 25%가 되면 위반입니다. 기본값에서는 모든 CPU 사용 과다 정책 임계값 위반이 보고됩니다.  
  
 단일 위반으로 생성되는 노이즈를 줄이려면 다음 옵션을 고려해 보십시오.  
  
-   평가 기간을 1증가분으로 6시간까지 늘립니다. 6시간 동안 샘플 크기 24의 데이터 요소 1개가 단일 위반이 됩니다. 이 경우 정책에서 6시간 동안 정책 임계값(데이터 요소의 16.7%) 위반이 4번 허용되지만 6시간의 수집 기간 동안 위반이 5번 이상(데이터 요소 > 20%)이면 과다 사용을 보고합니다.  
  
-   위반 비율 허용을 1증가분으로 30%까지 늘립니다. 1시간 동안 샘플 크기 4의 데이터 요소 1개가 단일 위반이 됩니다. 이 경우 정책에서 시간당 위반이 1번 허용되지만 1시간의 수집 기간 동안 2번 이상 위반(데이터 요소 > 30%)되면 과다 사용을 보고합니다.  
  
-   ph x="1" /&gt; 의 관리되는 인스턴스 및 데이터 계층 응용 프로그램 프로세서 사용의 정책 임계값을 늘립니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스 또는 데이터 계층 응용 프로그램의 전역 CPU 사용 정책을 변경하는 방법은 [유틸리티 관리&amp;amp;#40;SQL Server 유틸리티&amp;amp;#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)를 참조하세요. 개별 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 CPU 사용 정책을 변경하는 방법은 [관리되는 인스턴스 세부 정보&amp;#40;SQL Server 유틸리티&amp;#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)를 참조하세요. 개별 데이터 계층 응용 프로그램의 CPU 사용 정책을 변경하는 방법은 [배포된 데이터 계층 응용 프로그램 세부 정보&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)를 참조하세요.  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>프로세서 사용이 얼마나 자주 위반되면 사용 미달로 보고됩니까?  
 평가 기간 및 위반 비율 허용 오차는 모두 유틸리티 탐색기의 **유틸리티 관리** 노드에 있는 **정책** 탭 설정에서 구성할 수 있습니다. 정책을 변경하려면 정책 설명 오른쪽에 있는 슬라이더 컨트롤을 사용한 다음 **적용**을 클릭합니다. 아래쪽에 있는 단추를 사용하여 기본값으로 복원하거나 변경을 취소할 수도 있습니다.  
  
-   데이터 수집 간격은 15분입니다. 이 값은 구성할 수 없습니다.  
  
-   프로세서 사용 정책의 기본 하한 임계값은 0%입니다. 옵션 범위는 0%에서 100% 사이입니다.  
  
-   프로세서 사용 미달의 기본 평가 기간은 1주일입니다. 옵션 범위는 1일에서 1개월 사이입니다.  
  
-   CPU 과다 미달이 보고되는 데이터 요소의 기본 위반 비율은 90%입니다. 옵션 범위는 0%에서 100% 사이입니다.  
  
 기본값의 경우 매주 데이터 요소 672개가 수집되지만 정책 임계값은 0%입니다. 따라서 기본적으로 이 정책에서는 프로세서 사용 미달 위반이 발생하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 관리되는 인스턴스 또는 데이터 계층 응용 프로그램의 전역 CPU 사용 정책을 변경하는 방법은 [유틸리티 관리&amp;amp;#40;SQL Server 유틸리티&amp;amp;#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)를 참조하세요. 개별 SQL Server 인스턴스의 CPU 사용 정책을 변경하는 방법은 [관리되는 인스턴스 세부 정보&amp;#40;SQL Server 유틸리티&amp;#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2)를 참조하세요. 개별 데이터 계층 응용 프로그램의 CPU 사용 정책을 변경하는 방법은 [배포된 데이터 계층 응용 프로그램 세부 정보&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [유틸리티 관리&#40;SQL Server 유틸리티&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)   
 [SQL Server 유틸리티에서 SQL Server 인스턴스 모니터링](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [리소스 상태 정책 정의 수정&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
