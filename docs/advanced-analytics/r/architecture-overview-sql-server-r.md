---
title: "아키텍처 개요(SQL Server R Services) | Microsoft 문서"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2fb02e5c71ae74afb4dd48e6a02e36a1c7dce9b7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="architecture-overview-for-r-in-sql-server"></a>SQL Server의 R에 대 한 아키텍처 개요

이 섹션에서는 SQL Server 2017 컴퓨터 학습 서비스 및 SQL Server 2016 R Services의 아키텍처의 개요를 제공 합니다.

확장성 아키텍처에 대 한 아키텍처는 동일 하거나 SQL Server 2016에 대 한 매우 유사한 및 SQL Server 2017 릴리스도 R 및 Python 유사 합니다. 그러나 토론을 단순화 하려면이 항목에서는 설명만 R 구성 요소, 외부 스크립트 실행, 보안, R 라이브러리 및 오픈 소스 오른쪽와의 상호 운용성을 지원 하기 위해 SQL Server 데이터베이스 엔진에 추가 된 새 구성 요소를 포함 하 여

자세한 내용은 각 섹션에 대 한 링크에 제공 됩니다.

## <a name="r-interoperability"></a>R 상호 운용성

SQL Server 2016 R 서비스와 SQL Server 2017 컴퓨터 학습 Services (In-database) R, 분산 및/또는 병렬 처리를 지원 하는 Microsoft에서 제공 하는 패키지의 오픈 소스 배포를 설치 합니다.

아키텍처는 SQL Server에서 별도 프로세스에서 R을 사용 하 여 외부 스크립트 실행 되도록 설계 되었습니다. R의 현재 사용자는 R 코드를 포팅하고 비교적 사소한 내용만 수정하여 T-SQL에서 실행할 수 있습니다.

를 솔루션의 크기를 조정 하거나 병렬 처리를 사용 하 여 사용 하는 권장는 [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 패키지 또는 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package) 패키지 합니다. 이러한 라이브러리에서 제공 하는 분산된 컴퓨팅 기능을 사용 하지 않는 경우 SQL Server의 컨텍스트에서 R 코드를 실행 하 여 약간의 성능 향상을 얻을 수 있습니다.

설치 된 스크립팅 외부 구성 요소 또는 R로 SQL Server와의 상호 작용 하는 방법에 대 한 자세한 내용은 참조 [R 상호 운용성](../../advanced-analytics/r/r-interoperability-in-sql-server.md)

## <a name="components-to-support-r-integration"></a>R 통합을 지원 하도록 구성 요소

SQL Server 2016에 도입 된 확장성 프레임 워크는 SQL Server 2017에서 계속 됩니다. 확장성 구성 요소는 SQL Server에서 R, R과 데이터베이스 엔진 간에 데이터를 전달 하 고 R 작업에 필요한 병렬 작업을 조정할 수에 대 한 외부 런타임을 시작 하는 데 사용 됩니다.

외부 스크립트를 실행 하기 위한 안전한 고성능 플랫폼을 제공 하는 동안 압축 및 데이터 교환 속도 개선 하기 위해 추가 구성 요소가 이러한 역할이입니다.

에 대 한 자세한 설명은 같은 R을 지 원하는 구성 요소는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 및 참조 RLauncher [새 구성 요소](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md)합니다.

## <a name="security"></a>보안

컴퓨터 학습 서비스 또는 SQL Server R Services를 사용 하 여 R 코드를 실행 하면 모든 R 스크립트 보안 및 큰 관리 효율성을 제공 하는 SQL Server 프로세스 외부 실행 됩니다. 이 격리 프로세스의 저장된 프로시저의 일부로 R 스크립트를 실행 하거나 원격 컴퓨터에서 SQL Server 컴퓨터 작업에 연결 및 계산 컨텍스트로 써 서버를 사용 하는 작업을 시작 하는지 여부에 관계 없이 마찬가지입니다.

SQL Server 작업에 대 한 모든 요청을 차단 하 고, 작업 및 Windows 작업 개체를 사용 하 여 해당 데이터 보안을 설정, SQL Server 사용자 계정 및 데이터베이스 역할을 사용 하 여 데이터에 대해 보안을 유지 관리.

데이터는 테이블, 데이터베이스 및 인스턴스 수준에서 SQL Server 보안을 적용 하 여 준수 경계 내에서 유지 됩니다. 데이터베이스 관리자는 R 작업을 실행할 수 있는 사용자 및 설치 하거나 R 패키지를 공유할 수 있는 사용자 제어할 수 있습니다. 관리자도 원격 또는 로컬 사용자가 R 스크립트 사용을 모니터링 하 고 모니터링 및 관리할 수 리소스를 사용 합니다.

## <a name="next-steps"></a>다음 단계

[R 통합을 지원하는 구성 요소](new-components-in-sql-server-to-support-r.md)

[R 상호 운용성](r-interoperability-in-sql-server.md)

[보안 개요](security-overview-sql-server-r.md)
