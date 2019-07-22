---
title: 가용성 그룹에 대한 압축 튜닝 | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 7632769c-b246-4766-886f-7c60ec540be8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3891d30ef5bfffb19ca1d4bfcaab290e3903816b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013670"
---
# <a name="tune-compression-for-availability-group"></a>가용성 그룹에 대한 압축 조정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
기본적으로 SQL Server는 가용성 그룹에 적절한 데이터 스트림을 압축합니다. 압축은 네트워크 트래픽을 줄이고 CPU 부하를 증가시키며 대기 시간을 유도할 수 있습니다. 압축을 사용하도록 설정하려면 sysadmin 고정 서버 역할이 있는 멤버여야 합니다. 다음 표는 SQL Server가 가용성 그룹 로그 스트림에 대해 압축을 사용하는 경우를 보여 줍니다.

| 시나리오 | 압축 설정
| ---- | ----
| 동기-커밋 복제본 | 압축되지 않음
| 비동기-커밋 복제본 | Compressed
| 자동 시드 중 | 압축되지 않음

## <a name="trace-flags-for-availability-group-compression"></a>가용성 그룹 압축에 대한 추적 플래그 

대부분의 시나리오에서 이러한 설정을 변경하지 않는 것이 좋습니다. 전역 추적 플래그를 사용하여 이러한 설정 변경을 테스트할 수 있습니다. SQL Server는 인스턴스 전체에 전역 추적 플래그를 적용합니다. 인스턴스의 모든 가용성 그룹은 이러한 설정에 영향을 받습니다.  

다음 표는 SQL Server에 대한 기본 압축 동작을 변경하는 추적 플래그를 보여 줍니다. 

추적 플래그 | 설명
------------- | -------------
1462          | 비동기 복제본에서 가용성 그룹에 대한 로그 스트림 압축을 사용하지 않도록 설정합니다. 이 기능은 네트워크 대역폭을 최적화하기 위해 비동기 복제본에서 기본적으로 설정되어 있습니다.
9567          | 자동 시드 중 가용성 그룹에 대한 데이터 스트림 압축을 사용하도록 설정합니다. 자동 시드 중 압축은 전송 시간을 크게 줄일 수 있으며 프로세서 부하가 증가됩니다.
9592          | 동기 복제본에서 가용성 그룹에 대한 로그 스트림 압축을 사용하도록 설정합니다. 압축이 대기 시간을 추가하기 때문에 이 기능은 동기 복제본에서 기본적으로 해제되어 있습니다. 비동기 복제본에서 로그 스트림 압축은 기본적으로 설정되어 있습니다.


## <a name="resources"></a>리소스


[데이터베이스 엔진 시작 옵션](../../../database-engine/configure-windows/database-engine-service-startup-options.md)

[자동 시드](https://msdn.microsoft.com/library/mt735149(SQL.130).aspx)

[Always On 필수 조건](prereqs-restrictions-recommendations-always-on-availability.md) 
