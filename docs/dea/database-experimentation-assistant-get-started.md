---
title: 작업 비교 프로세스 개요
description: DEA (데이터베이스 실험 도우미)는 업그레이드 또는 새 인덱스와 같은 SQL Server 환경의 변경에 대 한 A/B 테스트 솔루션입니다.
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: rajsell
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 36e36060e16ff85ba2b1fa58d9d900231cf6581f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258519"
---
# <a name="overview-of-the-workload-comparison-process"></a>작업 비교 프로세스 개요

DEA (데이터베이스 실험 도우미)를 사용 하면 현재 환경에서 원본 서버의 워크 로드가 새 환경에서 어떻게 수행 될 것인지 평가할 수 있습니다. DEA 3 단계를 완료 하 여 A/B 테스트를 실행 하는 과정을 안내 합니다.

- 원본 서버에서 작업 추적 캡처
- 대상 1과 대상 2에서 캡처된 작업 추적을 재생 합니다.
- 대상 1과 대상 2에서 수집 된 재생 된 작업 추적을 분석 합니다.

이 문서에서는이 프로세스에 대 한 개요를 제공 합니다.

## <a name="capturing-a-workload-trace"></a>작업 추적 캡처

SQL Server A/B 테스트의 첫 번째 단계는 원본 서버에서 추적을 캡처하는 것입니다. 원본 서버는 일반적으로 프로덕션 서버입니다. 추적 파일은 타임 스탬프를 포함 하 여 해당 서버에서 전체 쿼리 작업을 캡처합니다.

고려 사항:

- 시작 하기 전에 추적을 캡처할 데이터베이스를 백업 해야 합니다.
- DEA 사용자는 Windows 인증을 사용 하 여 데이터베이스에 연결할 수 있어야 합니다.
- SQL Server 서비스 계정에서 원본 추적 파일 경로에 액세스할 수 있어야 합니다.
- DEA는 쿼리 성능이 향상 되는지 또는 저하 되는지 확인 하기 위해 캡처 기간 동안 쿼리를 15 번 이상 실행 해야 합니다.

## <a name="replaying-a-workload-trace"></a>작업 추적 재생

SQL Server A/B 테스트의 두 번째 단계는 두 개의 대상 서버에서 캡처한 추적 파일을 재생 하는 것입니다.

대상 1은 제안 된 대상 환경을 모방 하는 원본 서버 대상 2를 모방 합니다.

대상 1과 대상 2의 하드웨어 구성은 가능한 한 유사 하 여 SQL Server에서 제안 된 변경의 성능 효과를 정확 하 게 분석할 수 있도록 해야 합니다.

고려 사항:

- 작업 추적을 재생 하려면 컴퓨터에서 DReplay (Distributed Replay) 추적을 실행 하도록 설정 해야 합니다.
- 원본 서버의 백업을 사용 하 여 대상 서버에서 데이터베이스를 복원 해야 합니다.
- 평가 결과의 일관성을 향상 시키려면 서비스 응용 프로그램에서 SQL Server 서비스 (MSSQLSERVER)를 다시 시작 하는 것이 좋습니다. SQL Server의 쿼리 캐싱은 평가 결과에 영향을 줄 수 있습니다.

## <a name="analyzing-the-replayed-workload-traces"></a>재생 된 작업 추적 분석

프로세스의 마지막 단계는 재생 추적을 사용 하 여 분석 보고서를 생성 하 고, 제안 된 변경의 잠재적인 성능 영향에 대 한 정보를 얻기 위해 보고서를 검토 하는 것입니다.

고려 사항:

- 하나 이상의 구성 요소가 없는 경우 새 분석 보고서 (인터넷 연결 필요)를 생성 하려고 하면 다운로드 링크가 있는 필수 구성 요소 페이지가 나타납니다.
- 이전 버전의 도구에서 생성 된 보고서를 보려면 먼저 스키마를 업데이트 해야 합니다.

## <a name="see-also"></a>참고 항목

- 서버에서 발생 하는 이벤트 로그를 사용 하 여 추적 파일을 생성 하는 방법에 대 한 자세한 내용은 [데이터베이스 실험 도우미 추적 캡처](database-experimentation-assistant-capture-trace.md)문서를 참조 하세요.