---
title: "아키텍처 개요 (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c4a4f66-ea3e-4a73-acf2-6c8aeafc94b0
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# 아키텍처 개요 (SQL Server R Services)
이 섹션에서는의 아키텍처에 대 한 개요를 제공 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], 보안, R 지원 구성 요소와 SQL Server에서 실행 되는 오픈 소스 R 스크립트의 상호 운용성에 SQL Server 데이터베이스 엔진에 추가 된 새 구성 요소를 포함 합니다.


## 목표


아키텍처 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] 오픈 소스 R 언어를 지원 하도록 설계 되었습니다. R의 현재 사용자가 포트는 R 코드를 비교적 약간만 수정 해도 T-SQL에서 실행할 수 있어야 합니다.

그러나 SQL Server R 서비스 성능이 향상된 되 고 더 빠른 데이터 처리량 및 처리를 활성화 하 고 엔터프라이즈 솔루션의 개발을 R에 대 한 장애물을 줄이려면 R 언어에 대 한 자세히 데이터베이스 통합을 제공 하는 혁신적인 기술을 제공 합니다. 이러한 기술 혁신 오픈 소스 및 Microsoft에서 개발한 독점 구성 요소를 모두 포함 됩니다.


SQL Server와의 통합의 기본적인 목표는 데이터를 안전 하 게 관리 하는 동안, R에 대 한 향상 된 성능과 확장성을 제공 되도록 합니다. 이 목표를 향해 SQL Server R 서비스 Windows 통합된 인증 및 SQL 로그인 암호 기반을 모두 지 원하는 다중 프로세스 인프라를 제공 합니다. 

+ [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] R, R 작업을 병렬로 실행할 수 있는 기능과 ScaleR 패키지와 함께 기본 배포를 제공 합니다.
+ 외부 스크립트를 실행 하기 위한 안전 하 고 성능이 뛰어난 프레임 워크를 제공 하는 SQL Server의 새로운 구성 요소입니다.
+ R 작업 높은 관리 효율성 및 보안을 제공 하는 SQL Server 프로세스 외부에서 실행 합니다.
+ [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] R의 모든 프로세스의 보안을 관리합니다. 

이 섹션의 항목을 기존 R 코드를 최적화 하 고 이러한 향상 된이 기능을 활용할 수 있도록 자세히 새 아키텍처에 설명 합니다. 데이터 처리 및 분석 하 여 처리 방법을 이해 함으로써 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], 데이터를 수집 하는 방법, 기능 엔지니어링을 가장 효율적으로 수행 하는 방법 및 결과 사용 하는 방법에 대 한 적절 한 생생한 결정할 수 있습니다.
 

## 섹션 내용
+ [R의 상호 운용성](../../advanced-analytics/r-services/r-interoperability-in-sql-server-r-services.md)
+ [R 서비스에 대 한 SQL Server의 새로운 구성 요소](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)
+ [보안 개요](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)

## 참고 항목
[R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)
