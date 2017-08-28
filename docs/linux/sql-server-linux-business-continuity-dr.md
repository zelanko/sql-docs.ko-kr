---
title: "Linux에서 SQL Server에 대 한 재해 복구 | Microsoft Docs"
description: 
author: mihaelab
ms.author: mihaelab
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: c75717c8-c677-4033-8ca6-d0ac93aee04d
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 86f41971e06efb767dde336cf93f9224a204176d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="business-continuity-and-database-recovery-sql-server-on-linux"></a>비즈니스 연속성 및 데이터베이스 복구 Linux에서 SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Linux에서 SQL Server는 다양 한 종류의 다양 한 비즈니스 요구 사항에 맞게 서비스 수준 계약 목표를 달성할 수가 있습니다.

가장 간단한 솔루션은 높은 수준의 내결함성 하드웨어 오류 및 탄력성 및 리소스 활용 최대화에 대 한 호스트 수준 오류에 대 한 복구를 달성 하기 위해 가상화 기술을 활용 합니다. 이러한 시스템 사설 또는 공용 클라우드 또는 하이브리드 환경에 온-프레미스, 실행할 수 있습니다. 가장 간단한 형태의 재해 복구 및 보호에는 데이터베이스 백업입니다. SQL Server 2017 r c 2에서 제공 되는 간단한 솔루션은 다음과 같습니다.

- **VM 장애 조치**
    - 게스트 및 OS 수준 오류 로부터 복구
    - 계획 되지 않은 및 계획 된 이벤트
    - 패치 및 업그레이드를 위해 최소 가동 중지 시간
    - RTO (분)


- [**데이터베이스 백업 및 복원**](sql-server-linux-backup-and-restore-database.md) 
    - 데이터 우발적 이거나 악의적인 손상 으로부터 보호
    - 재해 복구 보호가
    - RTO 시간 (분)

표준 고가용성 및 재해 복구 기술 신뢰할 수 있는 공유 저장소 인프라와 결합 하는 인스턴스 수준의 보호를 제공 합니다. SQL Server 2017 RC2 표준 고가용성 포함 됩니다.

- [**장애 조치 클러스터**](sql-server-linux-shared-disk-cluster-configure.md)
    - 인스턴스 수준의 보호
    - 자동 오류 검색 및 장애 조치
    - 운영 체제 및 SQL Server 오류에 대비해 복원 력
    - RTO 분 (초)


## <a name="summary"></a>요약

Linux에서 SQL Server 2017 RC2 고가용성 및 재해 복구를 지원 하기 위해 가상화, 백업 및 복원 및 장애 조치 클러스터를 포함 합니다. 
