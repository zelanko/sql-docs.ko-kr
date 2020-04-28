---
title: Oracle HR 스키마를 SQL Server on Linux |로 마이그레이션 Microsoft Docs
description: 샘플 Oracle 스키마를 SQL Server on Linux 변환
author: shamikg
ms.author: shamikg
manager: shamikg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: 1926c13b739de8294966fd6ce84df3d1e02a676e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266524"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>SQL Server Migration Assistant를 사용 하 여 Oracle 스키마를 Linux에서 SQL Server 2017로 마이그레이션

이 자습서에서는 Windows의 Oracle 용 SSMA (SQL Server Migration Assistant)를 사용 하 여 Oracle 샘플 **HR** 스키마를 [Linux의 SQL Server 2017](../../linux/sql-server-linux-overview.md)로 변환 합니다.

> [!div class="checklist"]
> * Windows에서 SSMA 다운로드 및 설치
> * SSMA 프로젝트를 만들어 마이그레이션을 관리 합니다.
> * Oracle에 연결
> * 마이그레이션 보고서 실행
> * 샘플 HR 스키마 변환
> * 데이터 마이그레이션

## <a name="prerequisites"></a>전제 조건

- **HR** 스키마가 설치 된 Oracle 12c (12.2.0.1.0)의 인스턴스
- SQL Server on Linux의 작업 인스턴스입니다.

> [!NOTE]
> 동일한 단계를 사용 하 여 Windows에서 SQL Server를 대상으로 지정할 수 있지만 프로젝트 **를 프로젝트로 마이그레이션** 설정에서 windows를 선택 해야 합니다.

## <a name="download-and-install-ssma-for-oracle"></a>Oracle 용 SSMA 다운로드 및 설치

원본 데이터베이스에 따라 여러 버전의 SQL Server Migration Assistant 사용할 수 있습니다.  최신 버전의 [Oracle SQL Server Migration Assistant](https://aka.ms/ssmafororacle) 다운로드 하 고 다운로드 페이지에 있는 지침을 사용 하 여 설치 합니다.

> [!NOTE]
> 현재는 **Oracle 용 Ssma 확장 팩** 이 Linux에서 지원 되지 않지만이 자습서에서는 필요 하지 않습니다.

## <a name="create-and-set-up-project"></a>프로젝트 만들기 및 설정

다음 단계를 사용 하 여 새 SSMA 프로젝트를 만듭니다.

1. Oracle 용 SSMA를 열고 **파일** 메뉴에서 **새 프로젝트** 를 선택 합니다.

1. 프로젝트에 이름을 지정합니다.

1. **마이그레이션 대상** 필드에서 "SQL Server 2017 (Linux)-미리 보기"를 선택 합니다.

Oracle 용 SSMA는 기본적으로 Oracle 샘플 스키마를 사용 하지 않습니다. HR 스키마를 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. SSMA에서 **도구** 메뉴를 선택 합니다.

1. **기본 프로젝트 설정**을 선택 하 고 **시스템 개체 로드**를 선택 합니다.

1. **HR** 이 선택 되어 있는지 확인 하 고 **확인**을 선택 합니다.

## <a name="connect-to-oracle"></a>Oracle에 연결

그런 다음 Oracle에 SSMA를 연결 합니다.

1. 도구 모음에서 **Oracle에 연결**을 클릭 합니다.

1. 서버 이름, 포트, Oracle SID, 사용자 이름 및 암호를 입력 합니다.

   ![Oracle에 연결](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 그런 다음 **연결**을 클릭합니다. 잠시 후 Oracle 용 SSMA는 데이터베이스에 연결 하 여 메타 데이터를 읽습니다.

## <a name="create-a-report"></a>보고서 만들기

다음 단계를 사용 하 여 마이그레이션 보고서를 생성 합니다.

1. **Oracle 메타 데이터 탐색기**에서 서버 노드를 확장 합니다.

1. **스키마**를 확장 하 고 **HR**을 마우스 오른쪽 단추로 클릭 한 다음 **보고서 만들기**를 선택 합니다.

   ![Oracle 메타 데이터 탐색기 보고서 만들기](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 변환과 관련 된 모든 경고 및 오류를 나열 하는 보고서가 포함 된 새 브라우저 창이 열립니다.

   > [!NOTE]
   > 이 자습서에서는 해당 목록에서 어떤 작업도 수행할 필요가 없습니다. Oracle 데이터베이스에 대해 이러한 단계를 수행 하는 경우 보고서를 검토 하 여 데이터베이스에 대 한 중요 한 변환 문제를 해결 해야 합니다.

   ![샘플 마이그레이션 보고서](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>SQL Server에 연결

그런 다음 **SQL Server에 연결을** 선택 하 고 적절 한 연결 정보를 입력 합니다.  아직 존재 하지 않는 데이터베이스 이름을 사용 하는 경우 Oracle 용 SSMA에서 해당 이름을 만듭니다.

![SQL Server에 연결](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>스키마 변환

**Oracle 메타 데이터 탐색기**에서 **HR** 을 마우스 오른쪽 단추로 클릭 하 고 스키마 변환을 선택 합니다.

![스키마 변환](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>데이터베이스 동기화

그런 다음 데이터베이스를 동기화 합니다.

1. 변환이 완료 되 면 **SQL Server Metadata 탐색기** 를 사용 하 여 이전 단계에서 만든 데이터베이스로 이동 합니다.

1. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스와 동기화**를 선택한 다음 확인을 클릭 합니다.

   ![데이터베이스와 동기화](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>데이터 마이그레이션

마지막 단계는 데이터를 마이그레이션하는 것입니다.

1. **Oracle 메타 데이터 탐색기**에서 **HR**을 마우스 오른쪽 단추로 클릭 하 고 **데이터 마이그레이션**을 선택 합니다.

1. 데이터 마이그레이션 단계를 수행 하려면 Oracle 및 SQL Server 자격 증명을 다시 입력 해야 합니다.

1. 완료 되 면 데이터 마이그레이션 보고서를 검토 합니다 .이 보고서는 다음 스크린샷 처럼 표시 됩니다.

   ![데이터 마이그레이션 보고서](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>다음 단계

더 복잡 한 Orcale 스키마의 경우 변환 프로세스에는 클라이언트 응용 프로그램에 대 한 더 많은 시간, 테스트 및 변경 내용이 포함 될 수 있습니다. 이 자습서는 전체 마이그레이션 프로세스의 일부로 Oracle 용 SSMA를 사용 하는 방법을 보여 주기 위한 것입니다.

이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * Windows에 SSMA 설치
> * 새 SSMA 프로젝트 만들기
> * Oracle에서 마이그레이션 평가 및 실행

다음으로 SSMA를 사용 하는 다른 방법을 탐색 합니다.

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant 설명서](../sql-server-migration-assistant.md)
