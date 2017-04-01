---
title: "SQL Server R 서비스 성능 조정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cf6f3b7d-f9f9-4e45-b0d1-07850b53e0c5
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# SQL Server R 서비스 성능 조정
[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 은 새로운 발견하는 지능형 응용 프로그램 개발을 위한 플랫폼을 제공합니다. 데이터 과학자가을 학습 시키고 모델 내부에 저장 된 데이터를 사용 하 여 R 언어의 강력한 기능을 사용할 수 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 모델을 프로덕션 준비가 되 면 데이터 과학자가 작업할 수 데이터베이스 관리자와 SQL 엔지니어 프로덕션 환경에서 해당 솔루션을 배포 합니다. 이 섹션의 정보는 프로덕션에 모델을 배포할 때 만들 때 모델을 학습 하 고 모두의 성능 튜닝에 높은 수준의 지침을 제공 합니다.

이 문서의 정보를 잘 알고 있다고 가정 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 개념 및 용어입니다. R 서비스에 대 한 일반적인 정보를 참조 하십시오. [SQL Server R 서비스](../../advanced-analytics/r-services/sql-server-r-services.md)합니다.

> [!NOTE]
> 이 섹션에 있는 정보의 대부분은 구성에 대 한 일반 지침 동안 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 일부 정보는 RevoScaleR 분석 함수에만 있습니다.

## 섹션 내용

* [SQL Server 구성](../../advanced-analytics/r-services/sql-server-configuration-r-services.md):이 문서에서는 하드웨어를 구성 하기 위한 지침을 제공 하는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 에 설치 됩니다. 에 가장 유용한 __데이터베이스 관리자가__합니다.

* [R 및 데이터 최적화](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md): R 스크립트를 사용 하 여 R 서비스와 지침을 제공 합니다. 에 가장 유용한 __데이터 과학자__합니다.

* [성능 사례 연구](../../advanced-analytics/r-services/performance-case-study-r-services.md):이 문서에서는 테스트 데이터 및 이전 문서에서 제공 하는 지침의 영향을 테스트 하는 데 사용할 수 있는 R 스크립트를 제공 합니다.

## 참조

다음은이 문서의 개발에 사용 되는 정보에 대 한 링크입니다.

* [64 비트 버전의 Windows에 대 한 적절 한 페이지 파일 크기를 결정 하는 방법](https://support.microsoft.com/kb/2860880)

* [데이터 압축](../../relational-databases/data-compression/data-compression.md)

* [테이블 또는 인덱스에 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [테이블 또는 인덱스에서 압축 해제](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

* [DISKSPD 저장소 부하 생성기/성능 테스트 도구](https://github.com/microsoft/diskspd)

* [FSUtil 유틸리티 참조](https://technet.microsoft.com/library/cc753059.aspx)

* [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

* [R Services](../../advanced-analytics/r-services/r-services.md)

* [RxDForest 및 rxDTree에 대 한 성능 튜닝 옵션](https://support.microsoft.com/kb/3104235)

* [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)

* [RevoScaleR 사용자 가이드](https://packages.revolutionanalytics.com/doc/7.0.0/win/RevoScaleR_Users_Guide.pdf)

* [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)

## 관련 항목:

 
 [R 서비스에 대 한 SQL Server 구성](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [성능 사례 연구](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R 및 데이터 최적화](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)