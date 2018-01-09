---
title: "Microsoft R Server(독립 실행형) 시작 | Microsoft 문서"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 7c68e4a44ea410d3ad54ee39a103695eb47b6473
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="getting-started-with-machine-learning-server-standalone"></a>컴퓨터 학습 Server (독립 실행형) 시작
 
SQL Server 2016의 Microsoft R Server (독립 실행형) 작업 고성능 분석 솔루션 및 다른 비즈니스 응용 프로그램과 통합을 사용 하도록 설정 하려면 엔터프라이즈도 인기 있는 오픈 소스 R 언어를 가져올 수 있습니다.  

SQL Server 2017 년 1 이름은 반영 Python 언어에 대 한 지원 추가 하도록 학습 Server 컴퓨터 (독립 실행형)로 변경 되었습니다. 두 버전이 Enterprise Edition 또는 Software Assurance의 사용자에 게 무료로 제공 됩니다.

이 문서에서는 학습 Server 컴퓨터 (또는 R 서버)를 사용 하는 방법을 및 설치와 샘플을 시작 하는 방법에 대 한 고급 개요를 제공 합니다.

## <a name="why-use-a-standalone-server-for-machine-learning"></a>기계 학습에는 독립 실행형 서버를 사용 하는 이유

기계 학습 SQL Server 데이터를 사용 하 여 솔루션을 통합 하 필요 하지 않으면, 서버를 학습 하는 컴퓨터 R 및 Python에 대 한 동일한 분산 하 고 확장 가능한 지원을 제공 하 고 또한 Hadoop, Spark, 또는 Linux에 대 한 솔루션의 배포를 지원 합니다.

서버를 학습 하는 컴퓨터에 이미지 분석 및 응용 프로그램에서 즉시 사용할 수 있는 감성 분석을 위해 미리 학습 된 모델도 포함 됩니다.

서버를 학습 하는 컴퓨터의 해결해줍니다 기능 구축 하 고 원격 실행, Spark 및 Hadoop MapReduce 클러스터 토폴로지 함께 웹 서비스를 사용 하 여 Python 및 R 솔루션 배포를 지원 및 Windows 또는 Linux에 대 한 지원 합니다.

**SQL Server 2016**

+ SQL Server 2016 설치 프로그램에서 Microsoft R Server (독립 실행형)를 설치 합니다.

    이 옵션은 독립 실행형 서버와를는 완전히 독립적인 R Services (In-database)를 만듭니다. 이 버전에서는 R을만 지원 합니다. 독립 실행형 서버 설치는 SQL Server Enterprise Edition 지원 정책에 포함 됩니다. 자세한 내용은 [독립 실행형 R 서버 만들기](../../advanced-analytics/r/create-a-standalone-r-server.md)를 참조하세요.

+ 별도 Windows installer를 사용 하 여 R 서버를 설치 합니다.

    이 설치 관리자는 Microsoft 최신 소프트웨어 기간 지원 정책을 사용 하 여 Microsoft R Server의 새 인스턴스를 만듭니다. 또한 Linux에서 Cloudera, Teradata 등 및 Hadoop에 대 한 R Server를 설치할 수 있습니다.
    
    자세한 내용은 참조 [Windows 용 R 서버 9.1 설치](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)합니다.

**SQL Server 2017**

+ SQL Server 2017 설치 프로그램에서 컴퓨터 학습 서버 (독립 실행형)를 설치 합니다. 

    이 옵션은 기계 학습의 R, Python, 또는 둘 다의 화를 지원 하기 위해 독립 실행형 서버를 만듭니다. 독립 실행형 서버 설치는 SQL Server Enterprise Edition 지원 정책에 포함 됩니다. 자세한 내용은 [독립 실행형 R 서버 만들기](../../advanced-analytics/r/create-a-standalone-r-server.md)를 참조하세요.  

+ 새 독립 실행형 Windows installer를 사용 합니다.

    이 설치 방법은 Microsoft 최신 소프트웨어 기간 지원 정책을 사용 하 여 학습 서버 컴퓨터의 새 인스턴스를 만듭니다. 추가 비용 없이 Hadoop, Spark, 또는 Linux 컴퓨터 학습 서버를 설치할 수 있습니다.
    
    자세한 내용은 참조 [Windows 용 컴퓨터 학습 서버 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)합니다.

**기존 서버를 업그레이드 합니다.**

+ 기존 서버 또는 인스턴스를 업그레이드 하는 경우 다운로드 하 고 업데이트를 Windows 기반 설치 프로그램을 실행 합니다. 

    자세한 내용은 참조 [인스턴스를 업그레이드 하려면 사용 하 여 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="start-using-machine-learning-server"></a>서버를 학습 하는 컴퓨터를 사용 하 여 시작

 서버 구성 요소를 설정 하 컴퓨터 학습 서버 이진 파일을 사용 하 여 IDE를 구성한 후에 RevoScaleR 및 revoscalepy, MicrosoftML, olapR 등 새 Api를 사용 하 여 솔루션 개발을 시작할 수 있습니다.
    
시작 하려면이 가이드를 참조 합니다.

+ [솔루션 템플릿](https://docs.microsoft.com/machine-learning-server/r/sample-solutions)

    이러한 샘플은 기계 학습 특정 산업 분야에 적용 하는 방법을 보여 주는 솔루션입니다. 현재 시나리오는 소매, 재무, 보건, 및 마케팅입니다.

+ [R과 25 함수에서 ScaleR 탐색](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): 고성능 R 솔루션에 맞게 크기 조정 및 제공 하는 배포 가능한 분석 함수의이 컬렉션을 탐색 합니다. K-means 클러스터링, 의사 결정 트리, 의사 결정 포리스트, 데이터 조작 도구 등 가장 많이 사용되는 R 모델링 패키지의 병렬 처리 버전을 포함합니다.

- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx)

    MicrosoftML 패키지는 새 컴퓨터 학습 알고리즘은 빠르고 확장 가능한 Microsoft에서 개발 변환의 집합입니다. Python 또는 R에서 사용할 수 있습니다. 자세한 내용은 참조 [Python에 대 한 MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 및 [R에 대 한 MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)합니다.

## <a name="see-also"></a>관련 항목:

[SQL Server 컴퓨터 학습 서비스 시작](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)