---
title: "방법 설명서 | Microsoft Docs"
ms.prod: world-wide-importers
ms.prod_service: sql-non-specified
ms.service: samples
ms.component: 
ms.technology: samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 17cabd9d-cb2f-436c-ad9c-ce02225808b7
caps.latest.revision: "3"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 367581f176b148fe65f8fee44bfdbb7a6eb5e8ec
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="wide-world-importers-documentation"></a>방법 설명서
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Wide World Importers는 SQL Server 2016에 대 한 새 예제 데이터베이스 및 Azure SQL 데이터베이스는 합니다. 트랜잭션 처리 (OLTP), 데이터 웨어하우징 및 분석 (OLAP) 워크 로드도 하이브리드 트랜잭션 및 분석 처리 (HTAP) 워크 로드에 대 한 SQL Server 2016 및 Azure SQL 데이터베이스의 핵심 기능을 보여 줍니다.

## <a name="about-this-sample"></a>이 샘플에 대 한

Wide World Importers은 포괄적인 데이터베이스 샘플에서는 데이터베이스 디자인 및 응용 프로그램에서 SQL Server 기능 수 활용 하는 방법을 보여 줍니다. 모두입니다.

일반적인 데이터베이스의 대표 여야 하는 샘플은 의미 있는 참고 합니다. SQL Server의 모든 기능은 포함 되지 않습니다. 데이터베이스의 디자인 표준 집합을 하나의 공통 집합 뒤에 하지만 여러 가지 방법으로 하나의 데이터베이스를 만들 수 있습니다.

**최신 릴리스**: [wide world-가져오기 도구 릴리스](http://go.microsoft.com/fwlink/?LinkID=800630)

**소스 코드 샘플에 대 한**: [wide world-importer](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers)합니다.

**피드백**:을 보내 주십시오 [ sqlserversamples@microsoft.com ](mailto:sqlserversamples@microsoft.com)합니다.

이 샘플에 대 한 설명서는 다음과 같이 구성 되어 있습니다.

## <a name="overview"></a>개요

Wide World Importers 샘플 회사의 개요 및 워크플로 샘플이 주소를 지정 합니다.

## <a name="main-oltp-database-wideworldimporters"></a>주 OLTP 데이터베이스 WideWorldImporters

설치 및 구성의 핵심에 대 한 지침에는 WideWorldImporters 트랜잭션 처리 (OLTP-온라인 트랜잭션 처리) 및 운영 분석 (HTAP-하이브리드 트랜잭션/분석 처리)에 사용 되는 데이터베이스입니다.

스키마와 WideWorldImporters 데이터베이스에 사용 되는 테이블의 설명입니다.  

WideWorldImporters 핵심 SQL Server 기능을 활용 하는 방법을 설명 합니다.

WideWorldImporters 데이터베이스에 대 한 샘플 쿼리 합니다.

## <a name="data-warehousing-and-analytics-database-wideworldimportersdw"></a>데이터 웨어하우징 및 분석 데이터베이스 WideWorldImportersDW

OLAP의 구성과 설치에 대 한 지침 WideWorldImportersDW 데이터베이스입니다.

스키마와 데이터 웨어하우징 및 분석 처리 (OLAP)에 대 한 예제 데이터베이스인 WideWorldImportersDW 데이터베이스에 사용 되는 테이블의 설명입니다.

데이터 웨어하우스에 WideWorldImportersDW WideWorldImporters 트랜잭션 데이터베이스에서 데이터를 마이그레이션합니다는 ETL (추출, 변환, 로드) 프로세스를 위한 워크플로.

WideWorldImportersDW 분석 처리에 대 한 SQL Server 기능을 활용 하는 방법을 설명 합니다.

샘플 분석 쿼리 WideWorldImportersDW 데이터베이스를 활용 합니다.

## <a name="data-generation"></a>데이터 생성

어떻게 추가 데이터를 설명 합니다. 예를 들어 sales를 삽입 하는 예제 데이터베이스에 생성 될 수 있고 현재 날짜 까지의 데이터를 구입 합니다.
