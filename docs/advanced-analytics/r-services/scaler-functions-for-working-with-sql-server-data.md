---
title: "SQL Server 데이터를 사용 하기 위한 scaleR 기능 | Microsoft Docs"
ms.custom: ""
ms.date: "01/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5f3c9864-9c75-4688-947d-0940045b2671
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# SQL Server 데이터를 사용 하기 위한 scaleR 기능
이 항목에서는 SQL Server와 해당 구문에 대 한 의견을 함께 사용 하기 위해 ScaleR 하는 주요 기능에 대해 간략하게를 제공 합니다.

ScaleR 기능 및 사용 하는 방법의 전체 목록에 대 한 참조는 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/index#) MSDN library에서 참조 합니다. 

## SQL Server 데이터 원본을 사용 하기 위한 기능
다음과 같은 기능을 통해 정의할 수는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터 원본입니다. 데이터 원본 개체는 테이블, 뷰 또는 쿼리 것으로 정의 된 원하는 데이터 집합을 함께 연결 문자열을 지정 하는 컨테이너입니다. 저장된 프로시저 호출이 지원 되지 않습니다.  

데이터 소스를 정의 하는 것 외에도 인스턴스 및 데이터베이스에 필요한 권한이 있는 경우 r, DDL 문을 실행할 수 있습니다. 
+ [RxSqlServerData](https://msdn.microsoft.com/microsoft-r/scaler/RxSqlServerData) -정의 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 데이터 원본 개체
+ [rxSqlServerDropTable](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerDropTable) -삭제는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 테이블
+ [rxSqlServerTableExists](https://msdn.microsoft.com/microsoft-r/scaler/rxSqlServerTableExists) -데이터베이스 테이블 또는 개체의 존재 여부 확인
+ [rxExecuteSQLDDL](https://msdn.microsoft.com/microsoft-r/scaler/rxExecuteSQLDDL) -정의 조작 또는 SQL 데이터를 제어 하는 명령을 실행 하지만 데이터를 반환 하지  

## 정의 또는 계산 컨텍스트 관리에 대 한 함수
다음 함수를 사용 하면 새 계산 컨텍스트를 정의 계산 컨텍스트 전환 또는 현재 계산 컨텍스트를 식별 합니다.
+ [RxComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/RxComputeContext) -계산 컨텍스트를 만듭니다. 
+ [rxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxInSqlServer) -수 있게 해 주는 SQL Server 계산 컨텍스트를 생성할 **ScaleR** SQL Server R 서비스의 기능을 실행 합니다.
+ [rxGetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxGetComputeContext) -현재 계산 컨텍스트를 가져옵니다. 
+ [rxSetComputeContext](https://msdn.microsoft.com/microsoft-r/scaler/rxSetComputeContext) -어떤 계산 사용할 컨텍스트를 지정 합니다. 

## 데이터 원본 사용에 대 한 함수
데이터 원본 개체를 만든 후에 데이터를 가져오는 열 수도 있고 새 데이터를 쓸 수 있습니다. 소스에 있는 데이터의 크기에 따라 데이터 원본의 일부로 서 일괄 처리 크기를 정의 하 고 청크에서 데이터를 이동할 수도 있습니다. 
+ [rxIsOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxIsOpen) -데이터 소스를 사용할 수 있는지 확인 하십시오.
+ [rxOpen](https://msdn.microsoft.com/microsoft-r/scaler/rxOpen) -읽기에 대 한 데이터 원본을 열
+ [rxReadNext](https://msdn.microsoft.com/microsoft-r/scaler/rxReadNext) -원본에서 데이터 읽기
+ [rxWriteNext](https://msdn.microsoft.com/microsoft-r/scaler/rxWriteNext) -대상에 데이터를 작성 합니다.
+ [rxClose](https://msdn.microsoft.com/microsoft-r/scaler/rxclose) -데이터 소스를 닫습니다.

이러한 ScaleR 함수 사용에 대 한 자세한 내용은 작업 하는 데이터 원본과 이외의 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 참조 [ Microsoft R Server-시작](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started)합니다.

## XDF 파일을 사용 하는 함수
다음 함수는 XDF 형식에서 로컬 데이터 캐시를 만드는 데 사용할 수 있습니다. 이 파일의 데이터베이스에 하나의 일괄 처리에서 전송할 수 보다 더 많은 데이터 또는 메모리에 들어갈 수 있는 양보다 많은 데이터를 작업할 때 유용할 수 있습니다.

데이터베이스에서 많은 양의 데이터를 로컬 워크스테이션 이동 정기적으로, 하는 경우 쿼리 하는 대신 각 R 작업에 대 한 반복 해 서 데이터베이스 사용할 수 있습니다 XDF 파일 데이터를 로컬에서 저장 한 다음 작업을 R 작업 영역에 캐시로 XDF 파일을 사용 하 여.

+ `rxImport` -XDF 파일에는 ODBC 원본에서 데이터 이동
+ `RxXdfData` -XDF 데이터 개체 만들기
+ `RxDataStep` -에서 데이터를 읽을 XDF int 데이터 프레임
+ `rxXdfToDataFrame` -에서 데이터를 읽을 XDF 데이터 프레임으로
+ `rxReadXdf` -에서 데이터를 읽고 XDF 데이터 프레임으로

XDF 파일을 사용 하는 방법의 예를 들어가이 자습서를 참조 하십시오.:  [데이터 과학 심층 분석-ScaleR 함수를 사용 하 여](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)

다양 한 소스에서 데이터 전송에 사용할 수 있는 이러한 ScaleR 함수에 대 한 자세한 내용은 참조[ Microsoft R Server-시작](http://msdn.microsoft.com/microsoft-r/rserver/rserver-getting-started)합니다.

## 참고 항목
[기본 R 및 ScaleR 함수 비교](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)
