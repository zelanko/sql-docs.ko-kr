---
title: 기계 학습 Python 사용 하 여 서비스 | Microsoft Docs
ms.date: 03/16/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 275eedc011367e51e97c6bddae03858cdda932ee
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="machine-learning-services-with-python"></a>기계 학습 Python 사용 하 여 서비스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python은 뛰어난 유연성과 다양 한 기계 학습 작업에 대 한 기능을 제공 하는 언어입니다. Python 용 오픈 소스 라이브러리 사용자 지정 가능한 신경망에 대 한 여러 플랫폼 물론 자연어 처리에 대 한 인기 있는 라이브러리를 포함합니다. 이제이 널리 사용 되는 언어는 SQL Server 2017 기계 학습에서 지원 됩니다.

Python 통합 되어는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진 보관 데이터 게 분석 하 고 비용 및 데이터 이동과 관련 된 보안 위험을 제거 합니다.  Visual Studio와 같은 편리 하 고 친숙 한 도구를 사용 하 여 Python을 기반으로 하는 컴퓨터 학습 솔루션을 배포할 수 있습니다. 프로덕션 응용 프로그램 예측, 모델을 얻을 수 또는 시각적 개체에서 Python 3.5 런타임에 단순히 T-SQL을 호출 하 여 저장 프로시저입니다.

이 릴리스는 python, Anaconda 배포도 [revoscalepy](../python/what-is-revoscalepy.md) 배율 및 기계 학습 솔루션의 성능을 개선 하기 위해 라이브러리입니다.

SQL Server 2017 설치 프로그램을 통해 python 시작 하는 데 필요한 모든를 설치할 수 있습니다.

+ [**기계 학습 Services (In-database)**](../install/sql-machine-learning-services-windows-install.md): SQL Server 데이터베이스 엔진에서 Python 스크립트의 보안 실행을 사용 하도록 설정 하려면 함께이 기능을 설치는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터입니다.
  
     이 기능을 선택 하면, 확장 Python 스크립트의 실행을 지원 하도록 데이터베이스 엔진에 설치 되 고 새 서비스를 만들면는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], Python 런타임 간의 통신을 관리 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.

+ [**기계 학습 서버 (독립 실행형)**](../install/sql-machine-learning-standalone-windows-install.md): SQL Server 통합을 필요 하지 않은 경우 분산된 기계 학습 Python 및 R 지원을 받으려면이 기능을 설치 합니다.

## <a name="see-also"></a>참고 항목

+ [SQL Server 컴퓨터 학습 및 R Services (In-database)](../r/sql-server-r-services.md)
+ [SQL Server 컴퓨터 학습 및 R Server (독립 실행형)](../r/r-server-standalone.md)
+ [Python 아키텍처](architecture-overview-sql-server-python.md)
+ [Python 자습서](../tutorials/sql-server-python-tutorials.md)
