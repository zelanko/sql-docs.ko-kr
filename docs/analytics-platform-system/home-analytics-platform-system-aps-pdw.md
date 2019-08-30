---
title: Analytics Platform System 설명서 | Microsoft Docs
description: 데이터 웨어하우징 및 빅 데이터 분석을 위해 설계된 데이터 플랫폼인 Microsoft APS(Analytics Platform System)는 완벽한 데이터 통합, 고속 쿼리 처리, 확장성이 우수한 스토리지, 종단 간 비즈니스 인텔리전스 솔루션에 대한 간단한 유지 관리를 제공합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/18/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 08f70ff74c5743f202867ae2a57adc1c6b9d677d
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153366"
---
# <a name="microsoft-analytics-platform-system"></a>Microsoft Analytics Platform System

데이터 웨어하우징 및 빅 데이터 분석을 위해 설계된 데이터 플랫폼인 Microsoft APS(Analytics Platform System)는 완벽한 데이터 통합, 고속 쿼리 처리, 확장성이 우수한 스토리지, 종단 간 비즈니스 인텔리전스 솔루션에 대한 간단한 유지 관리를 제공합니다.

![어플라이언스 아키텍처](media/architecture-high-level.png "어플라이언스 아키텍처")

Analytics Platform System은 MPP(대량 병렬 처리) 데이터 웨어하우스를 실행하는 소프트웨어인 SQL Server PDW(병렬 데이터 웨어하우스)를 호스트합니다.

PolyBase 기술은 관계형 PDW 데이터를 Windows Server의 Hortonworks, linux의 Hortonworks, linux 및 HDInsight의 Azure blob storage를 비롯 한 여러 원본의 Hadoop 데이터와 결합 합니다. 이러한 고급 데이터 통합 기능을 제공하고 비즈니스 인텔리전스 도구와 완벽하게 통합된 Analytics Platform System은 기업의 의사 결정권자가 보다 합리적이고 통찰력 있는 비즈니스 의사 결정을 내릴 수 있도록 통합된 분석 결과를 반환합니다.

Analytics Platform System은 하드웨어 및 소프트웨어가 미리 설치되고 여러 워크로드를 실행하도록 미리 구성된 어플라이언스로 데이터 센터에 제공됩니다. Analytics Platform System을 구입할 때 기업의 요구 사항에 따라 PDW에 대한 컴퓨팅 노드를 구입합니다.

Analytics Platform System은 빠르고 확장 가능할 뿐 아니라 높은 이중화 및 고가용성을 제공하도록 설계되었기 때문에 비즈니스에 가장 중요한 데이터에도 믿고 사용할 수 있는 안정적인 플랫폼입니다. Analytics Platform System은 쉽게 배우고 쉽게 관리할 수 있도록 단순성 위주로 설계되었습니다. Hadoop 데이터 분석에 PDW의 PolyBase 기술을 사용하고 비즈니스 인텔리전스 도구와 완벽하게 통합하여 엔드투엔드 솔루션을 빌드하기 위한 포괄적 플랫폼으로 만듭니다.

## <a name="parallel-data-warehouse-software-designed-for-massively-parallel-processing"></a>대량 병렬 처리를 위해 설계된 소프트웨어인 병렬 데이터 웨어하우스

PDW를 종단 간 비즈니스 인텔리전스 솔루션의 핵심 관계형 데이터 웨어하우징 구성 요소로 사용하세요. PDW의 MPP(대량 병렬 처리) 디자인은 일반적으로 SMP(대칭 다중 처리) 데이터베이스 관리 시스템에서 빌드된 기존 데이터 웨어하우스보다 쿼리 완료 속도가 50배 빠릅니다.

> [!NOTE]
> 50배 빠르다는 것은 수시간이 아닌 수분 내에 또는 수분이 아닌 수초 내에 쿼리가 완료된다는 의미입니다. 이처럼 획기적인 성능을 제공하므로 비즈니스 분석가가 보다 방대한 결과를 보다 빠르게 생성하고, 손쉽게 임시 쿼리를 수행하거나 세부 정보로 드릴다운할 수 있습니다. 결과적으로 기업에서 보다 합리적인 결정을 보다 신속하게 내릴 수 있습니다.

PDW를 사용하면 획기적인 쿼리 성능 외에도 다음 작업을 간편하게 수행할 수 있습니다.

- 기존 시스템에 "크기 조정 단위"를 추가 하 여 단일 어플라이언스에서 최대 6 페타바이트 데이터에 대 한 데이터 웨어하우스를 확장 합니다.

- 기본 제공 되는 높은 중복성 및 고가용성으로 인해 필요할 때 데이터를 신뢰할 수 있습니다.

- 데이터 로드 및 통합에 대 한 최신 데이터 문제를 해결 합니다.

- PDW의 매우 병렬화 된 PolyBase 기술을 사용 하 여 빠른 분석을 위해 Hadoop 데이터를 관계형 데이터와 통합 합니다.

- 비즈니스 인텔리전스 도구를 사용하여 포괄적인 종단 간 솔루션 빌드

## <a name="next-steps"></a>다음 단계

PDW의 이점에 대한 자세한 내용은 MSDN의 [차세대 데이터 웨어하우징 및 빅 데이터 솔루션을 위한 획기적인 플랫폼](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/dn520808%28v=msdn.10%29) 백서를 참조하세요.
