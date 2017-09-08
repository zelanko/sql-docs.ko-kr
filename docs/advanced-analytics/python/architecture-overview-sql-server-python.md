---
title: "아키텍처 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1328a346dd9852cba349e38204b49faf32573611
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="architecture-overview-for-machine-learning-services-with-python"></a>Python 컴퓨터 학습 서비스에 대 한 아키텍처 개요

이 항목에서는 Python SQL Server, 보안 모델, 구성 요소를 포함 하 여 외부 스크립트 실행을 지 원하는 데이터베이스 엔진 및 SQL Server와 Python의 상호 운용성을 사용 하도록 설정 하는 새 구성 요소와 통합 되어 방법의 개요를 제공 합니다. 자세한 내용은 링크 된 항목을 참조 합니다.

> [!IMPORTANT]
> Python에 대 한 지원은 SQL Server 2017 CTP 2.0부터 사용 가능 합니다. 이 시험판 기능은 변경 될 수 있습니다.

## <a name="python-interoperability"></a>Python 상호 운용성

SQL Server 컴퓨터 학습 Services (In-database)의 Python의 Anaconda 배포 Python 3.5 런타임 및 인터프리터를 설치합니다. 이렇게 하면 표준 Python 솔루션과 호환성 거의 완료 합니다. Python은 데이터베이스 작업 손상 되지 않도록 보장 하기 위해 SQL Server에서 별도의 프로세스로 실행 됩니다.

Python SQL Server와의 상호 작용 하는 방법에 대 한 자세한 내용은 참조 [Python 상호 운용성](../../advanced-analytics/python/python-interoperability.md)

## <a name="components-that-support-python-integration"></a>Python의 통합을 지원 하는 구성 요소

이제 SQL Server 2016에 도입 된 확장성 프레임 워크의 새로운 언어별 구성 요소 추가 통해 Python 스크립트 실행을 지원 합니다. 이러한 구성 요소는 외부 스크립트를 실행 하기 위한 안전한 고성능 플랫폼을 제공 하는 동안 압축 및 데이터 교환 속도 향상.

에 대 한 자세한 설명은 Python와 같은 지 원하는 구성 요소는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 및 참조 PythonLauncher [새 구성 요소](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md)합니다.

## <a name="security"></a>보안

보안 및 큰 관리 효율성을 제공 하는 SQL Server 프로세스 외부 Python 작업 실행 됩니다.

모든 작업은 Windows 작업 개체 또는 SQL Server 보안에 의해 보안 됩니다. 데이터는 테이블, 데이터베이스 및 인스턴스 수준에서 SQL Server 보안을 적용 하 여 준수 경계 내에서 유지 됩니다. 데이터베이스 관리자를 Python 작업을 실행 하 고, 사용자는 Python 스크립트를 사용 하 여 모니터링, 사용 되는 리소스를 볼 수 있는 사용자를 제어할 수 있습니다.

자세한 내용은 참조 [Python에 대 한 보안](../../advanced-analytics/python/security-overview-sql-server-python-services.md)

## <a name="resource-governance"></a>리소스 관리

SQL Server Enterprise Edition에서 관리 하 고 R 스크립트 및 Python 스크립트를 포함 하 여 외부 스크립트 작업의 리소스 사용 모니터링 리소스 관리자를 사용할 수 있습니다.

자세한 내용은 참조 [R에 대 한 리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md)합니다.

## <a name="next-steps"></a>다음 단계

[T-SQL을 사용 하 여 Python 실행](../tutorials/run-python-using-t-sql.md)
