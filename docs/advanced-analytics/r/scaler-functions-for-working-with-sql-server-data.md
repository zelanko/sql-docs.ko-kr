---
title: "SQL Server 데이터 작업을 위한 RevoScaleR 함수 | Microsoft Docs"
ms.custom: 
ms.date: 08/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: b1567bd6e4a419b293a963a7b3afe96c24409bcc
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="revoscaler-functions-for-working-with-sql-server-data"></a>SQL Server 데이터 작업을 위한 RevoScaleR 함수
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 항목에서는 SQL Server 데이터 작업을 위한 RevoScaleR에서 제공 하는 주요 기능에 대 한 개요를 제공 합니다.

ScaleR 함수 및 사용 하는 방법의 전체 목록에 대 한 참조는 [Microsoft R Server](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 참조 합니다.

## <a name="create-sql-server-data-sources"></a>SQL Server 데이터 원본 만들기

다음 함수를 사용하여 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터 원본을 정의할 수 있습니다. 데이터 원본 개체는 원하는 데이터 집합과 함께 연결 문자열을 지정하는 컨테이너로서, 테이블, 뷰 또는 쿼리로 정의됩니다. 저장 프로시저 호출은 지원되지 않습니다.

+ [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) -정의 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터 원본 개체입니다.

+ [RxOdbcData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxodbcdata) -다른 ODBC 데이터베이스에 대 한 데이터 개체를 만듭니다. 

## <a name="perform-ddl-statements"></a>DDL 문을 수행 합니다.

인스턴스 및 데이터베이스에 대해 필요한 권한이 있는 경우 R에서 DDL 문을 실행할 수 있습니다. 다음 함수는 DDL 문을 실행 하거나 데이터베이스 스키마를 검색할 ODBC 호출을 사용 합니다.

+ `rxSqlServerTableExists`및 [rxSqlServerDropTable](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdroptable) -Drop는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 테이블을 쿼리하거나 데이터베이스 테이블 또는 개체의 존재 여부 확인

+ [rxExecuteSQLDDL](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxexecutesqlddl) -정의 또는 데이터베이스 개체를 조작 하는 데이터 정의 언어 (DDL) 명령을 실행 합니다. 이 함수는 데이터를 반환할 수 없습니다 하며 검색 하거나 수정할 개체 스키마 또는 메타 데이터에만 사용 됩니다.

## <a name="define-or-manage-compute-contexts"></a>정의 또는 계산 컨텍스트를 관리 합니다.

다음 함수를 사용하여 새 계산 컨텍스트를 정의하거나, 계산 컨텍스트를 전환하거나, 현재 계산 컨텍스트를 식별할 수 있습니다.

+ [RxComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxcomputecontext) - 계산 컨텍스트를 만듭니다.

+ [rxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver) - **ScaleR** 함수를 SQL Server R Services에서 실행하는 데 사용되는 SQL Server 계산 컨텍스트를 생성합니다. 이 계산 컨텍스트는 현재 Windows의 SQL Server 인스턴스에 대해서만 지원됩니다.

+ `rxGetComputeContext`및 [rxSetComputeContext](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxgetcomputecontext) -Get 또는 활성 계산 컨텍스트를 설정 합니다.

## <a name="move-data-and-transform-data"></a>데이터 이동 하 고 데이터 변환

데이터 원본 개체를 만든 후 데이터를 로드, 데이터를 변환 또는 지정된 된 대상에 새 데이터를 작성 하는 개체를 사용할 수 있습니다. 원본의 데이터 크기에 따라 일괄 처리 크기를 데이터 원본의 일부로 정의하고 데이터를 청크로 이동할 수도 있습니다.

+ [rxOpen 메서드](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxopen-methods) -열고 데이터 소스를 사용할 수 있는지 여부를 확인 또는 데이터 원본, 데이터 원본에서 읽어, 대상에 데이터를 쓸 닫은 닫습니다 데이터 원본

+ [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) -파일 저장소 또는 데이터 프레임에 데이터 원본에서 데이터를 이동 합니다.

+ [rxDataStep](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdatastep) -데이터 원본 간에 이동 하는 동안 데이터를 변환 합니다.

다음 함수는 XDF 형식의 로컬 데이터 저장소를 만드는 데 사용할 수 있습니다. 이 파일은 데이터베이스에서 하나의 일괄 처리로 전송될 수 있는 것보다 많은 데이터 또는 메모리에 맞출 수 있는 것보다 많은 데이터를 사용할 경우 유용할 수 있습니다.

예를 들어 정기적으로 이동 하면 많은 양의 데이터 데이터베이스에서 로컬 워크스테이션을 쿼리 하는 대신 각 R 작업에 대 한 반복 해 서 데이터베이스 사용할 수 있습니다 XDF 파일 캐시의 한 종류로 데이터를 로컬로 저장 한 다음 R 작업 영역에서 작업.

+ [RxXdfData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxxdfdata) -XDF 데이터 개체 만들기

+ [rxReadXdf](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxreadxdf) -을 데이터 프레임으로 XDF 파일에서 데이터를 읽고

이러한 함수 사용에 대 한 자세한 내용은 아닌 다른 원본 데이터를 사용 하는 등 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 참조 [Microsoft R의 데이터 분석을 위해 방법 안내](https://docs.microsoft.com/r-server/r/how-to-introduction)합니다.
