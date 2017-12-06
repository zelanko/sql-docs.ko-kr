---
title: "Linux에서 SQL Server로 Oracle HR 스키마 마이그레이션 | Microsoft Docs"
description: "Linux에서 SQL Server로 샘플 Oracle 스키마 변환"
author: edmacauley
ms.author: edmacauley
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 32ecce66caea01798b3c189108a5e196b04999d0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>SQL Server 2017 linux와 SQL Server Migration Assistant로 Oracle 스키마 마이그레이션

이 자습서를 사용 하 여 SQL Server Migration Assistant (SSMA) Windows에서 Oracle에 대 한 Oracle 샘플 변환 **HR** 스키마를 [SQL Server 2017 linux](../../linux/sql-server-linux-overview.md)합니다.

> [!div class="checklist"]
> * 다운로드 하 여 Windows에 SSMA를 설치 합니다.
> * 마이그레이션 관리를 위한 SSMA 프로젝트 만들기
> * Oracle에 연결
> * 마이그레이션 보고서를 실행 합니다.
> * 샘플 HR 스키마 변환
> * 데이터 마이그레이션

## <a name="prerequisites"></a>필수 구성 요소

- 인스턴스가 Oracle 12c (12.2.0.1.0)는 **HR** 스키마 설치
- Linux에서 SQL Server의 작업 인스턴스

> [!NOTE]
> 동일한 단계를 windows에서 SQL Server 대상에 사용할 수 있지만 Windows에서 선택 해야 합니다는 **마이그레이션 대상** 프로젝트 설정 합니다.

## <a name="download-and-install-ssma-for-oracle"></a>다운로드 및 Oracle 용 SSMA를 설치 합니다.

원본 데이터베이스에 따라 사용 가능한 여러 가지 버전의 SQL Server Migration Assistant 있습니다.  현재 버전의 다운로드 [SQL Server Migration Assistant for Oracle](http://aka.ms/ssmafororacle) 다운로드 페이지에 나오는 지침을 사용 하 여 설치 하 고 있습니다.

> [!NOTE]
> 이번에 **Oracle 확장 팩 용 SSMA** linux에서 지원 되지 않습니다 이지만이 자습서에서는 필요 하지 않습니다.

## <a name="create-and-set-up-project"></a>만들기 및 설치 프로젝트

새 SSMA 프로젝트를 만들려면 다음 단계를 사용 합니다.

1. Oracle 용 SSMA를 열고 선택 **새 프로젝트** 에서 **파일** 메뉴.

1. 프로젝트에 이름을 지정 합니다.

1. "SQL Server 2017 (Linux)-미리 보기"를 선택는 **마이그레이션 대상** 필드입니다.

Oracle 용 SSMA는 기본적으로 Oracle 샘플 스키마를 사용 하지 않습니다. HR 스키마를 사용 하려면 다음 단계를 사용 합니다.

1. SSMA를에서 선택 된 **도구** 메뉴.

1. 선택 **기본 프로젝트 설정**를 선택한 후 **시스템 개체를 로드**합니다.

1. 확인 **HR** 선택 되 고 선택 **확인**합니다.

## <a name="connect-to-oracle"></a>Oracle에 연결

다음 SSMA Oracle에 연결 합니다.

1. 도구 모음에서 클릭 **Connect to Oracle**합니다.

1. 서버 이름, 포트, Oracle SID, 사용자 이름 및 암호를 입력 합니다.

   ![Oracle에 연결](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 그런 다음 **연결**을 클릭합니다. 몇 분 안에 SSMA for Oracle 데이터베이스에 연결 하 고 해당 메타 데이터를 읽습니다.

## <a name="create-a-report"></a>보고서 만들기

마이그레이션 보고서를 생성 하려면 다음 단계를 사용 합니다.

1. 에 **Oracle 메타 데이터 탐색기**, 해당 서버 노드를 확장 합니다.

1. 확장 **스키마**를 마우스 오른쪽 단추로 클릭 **HR**를 선택 하 고 **보고서 만들기**합니다.

   ![Oracle 메타 데이터 탐색기는 보고서 만들기](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 모든 경고 및 변환와 관련 된 오류를 나열 하는 보고서는 새 브라우저 창이 열립니다.

   > [!NOTE]
   > 이 자습서에 대 한 목록을가지고 어떤 작업도 수행할 필요가 없습니다. 사용자 고유의 Oracle 데이터베이스에 대해 이러한 단계를 수행 하는 경우 데이터베이스에 대 한 중요 한 변환 문제를 해결 하려면 보고서를 검토 해야 합니다.

   ![예제 마이그레이션 보고서](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>SQL Server에 연결

그런 다음 선택 **SQL Server에 연결** 적절 한 연결 정보를 입력 합니다.  값이 없으면 데이터베이스 이름을 사용 하는 경우 존재, Oracle 용 SSMA를 만듭니다.

![SQL Server에 연결](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>스키마 변환

마우스 오른쪽 단추로 클릭 **HR** 에 **Oracle 메타 데이터 탐색기**를 변환 하는 스키마를 선택 합니다.

![스키마 변환](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>데이터베이스 동기화

그런 다음 데이터베이스를 동기화 합니다.

1. 변환이 완료 되 면 사용는 **SQL Server 메타 데이터 탐색기** 이전 단계에서 만든 데이터베이스를 이동할 수 있습니다.

1. 사용자 데이터베이스를 마우스 오른쪽 단추로 클릭 **데이터베이스와 동기화**, 한 다음 확인을 클릭 합니다.

   ![데이터베이스와 동기화](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>데이터 마이그레이션

마지막 단계 데이터를 마이그레이션할입니다.

1. 에 **Oracle 메타 데이터 탐색기**를 마우스 오른쪽 단추로 클릭 **HR**를 선택 하 고 **데이터 마이그레이션**합니다.

1. 데이터 마이그레이션 단계는 Oracle 및 SQL Server 자격 증명을 다시 입력 해야 합니다.

1. 완료 되 면 다음 스크린샷과 유사 하 게 같아야 합니다. 된 데이터 마이그레이션 보고서를 검토 합니다.

   ![데이터 마이그레이션 보고서](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>다음 단계

더 복잡 한 Orcale 스키마, 변환 프로세스는 더 많은 시간, 테스트 및 클라이언트 응용 프로그램을 가능한 변경 포함 됩니다. 이 자습서의 목적은 전체 마이그레이션 프로세스의 일부로 oracle SSMA를 사용 하는 방법을 보여 줍니다.

이 자습서에서는 알아보았습니다 하는 방법:
> [!div class="checklist"]
> * SSMA Windows에 설치
> * 새 SSMA 프로젝트 만들기
> * 평가 하 고 Oracle에서 마이그레이션을 실행합니다

다음으로 SSMA를 사용 하는 다른 방법을 살펴봅니다.

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant 설명서](../sql-server-migration-assistant.md)
