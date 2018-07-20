---
title: Linux의 SQL Server로 Oracle HR 스키마 마이그레이션 | Microsoft Docs
description: Linux의 SQL Server 샘플 Oracle 스키마 변환
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.suite: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: 9a556b8b800a03808def02c2953107faa90d7e34
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086075"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Oracle 스키마를 SQL Server Migration Assistant를 사용 하 여 Linux에서 SQL Server 2017로 마이그레이션

이 자습서를 사용 하 여 SQL Server Migration Assistant (SSMA) Oracle Windows에 대 한 Oracle 샘플 변환 **HR** 스키마 [Linux의 SQL Server 2017](../../linux/sql-server-linux-overview.md)합니다.

> [!div class="checklist"]
> * 다운로드 하 고 Windows SSMA 설치
> * 마이그레이션 관리를 SSMA 프로젝트 만들기
> * Oracle에 연결
> * 마이그레이션 보고서를 실행 합니다.
> * 샘플 HR 스키마 변환
> * 데이터 마이그레이션

## <a name="prerequisites"></a>사전 요구 사항

- 인스턴스가 Oracle 12c (12.2.0.1.0)는 **HR** 스키마 설치
- Linux의 SQL Server의 작업 인스턴스를

> [!NOTE]
> Windows, SQL Server 대상에 동일한 단계를 사용할 수 있지만 Windows에서 선택 해야 합니다는 **마이그레이션** 프로젝트 설정 합니다.

## <a name="download-and-install-ssma-for-oracle"></a>다운로드 및 Oracle 용 SSMA 설치

여러 버전의 SQL Server Migration Assistant는 원본 데이터베이스에 따라 사용할 수 있습니다.  현재 버전을 다운로드 [SQL Server Migration Assistant for Oracle](http://aka.ms/ssmafororacle) 다운로드 페이지에 나와 있는 지침을 사용 하 여 설치 합니다.

> [!NOTE]
> 이번에 **확장 팩 Oracle 용 SSMA** linux에서 지원 되지 않습니다 이지만이 자습서에 필요 하지 않습니다.

## <a name="create-and-set-up-project"></a>만들기 및 설치 프로젝트

새 SSMA 프로젝트를 만들려면 다음 단계를 사용 합니다.

1. Oracle 용 SSMA를 열고 **새 프로젝트** 에서 합니다 **파일** 메뉴.

1. 프로젝트 이름을 지정 합니다.

1. "SQL Server 2017 (Linux)-미리 보기"를 선택 합니다 **마이그레이션** 필드입니다.

Oracle 용 SSMA는 기본적으로 Oracle 샘플 스키마를 사용 하지 않습니다. HR 스키마를 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. SSMA를 선택 합니다 **도구** 메뉴.

1. 선택 **기본 프로젝트 설정**를 선택한 후 **시스템 개체 로드**합니다.

1. 했는지 **HR** 을 선택 하면 선택한 **확인**합니다.

## <a name="connect-to-oracle"></a>Oracle에 연결

다음 SSMA Oracle에 연결 합니다.

1. 도구 모음에서 클릭 **Connect to Oracle**합니다.

1. 서버 이름, 포트, Oracle SID, 사용자 이름 및 암호를 입력 합니다.

   ![Oracle에 연결](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 그런 다음 **연결**을 클릭합니다. 몇 분에서 Oracle 용 SSMA 데이터베이스에 연결 하 고 해당 메타 데이터를 읽습니다.

## <a name="create-a-report"></a>보고서 만들기

마이그레이션 보고서를 생성 하려면 다음 단계를 사용 합니다.

1. 에 **Oracle 메타 데이터 탐색기**, 서버의 노드를 확장 합니다.

1. 확장 **스키마**를 마우스 오른쪽 단추로 클릭 **HR**를 선택 하 고 **보고서 만들기**합니다.

   ![Oracle 메타 데이터 탐색기는 보고서 만들기](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 모든 경고 및 변환와 관련 된 오류를 나열 하는 보고서를 사용 하 여 새 브라우저 창이 열립니다.

   > [!NOTE]
   > 이 자습서에 대 한 해당 목록을 사용 하 여 아무 작업도 수행할 필요가 없습니다. 사용자 고유의 Oracle 데이터베이스에 대 한이 단계를 수행 하는 경우 데이터베이스에 대 한 중요 한 변환 문제를 해결 하려면 보고서를 검토 해야 합니다.

   ![샘플 마이그레이션 보고서](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>SQL Server에 연결

다음 선택 **SQL Server에 연결** 적절 한 연결 정보를 입력 합니다.  아직 하지 않은 데이터베이스 이름을 사용 하는 경우 존재, Oracle 용 SSMA를 만듭니다.

![SQL Server에 연결](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>스키마 변환

마우스 오른쪽 단추로 클릭 **HR** 에 **Oracle 메타 데이터 탐색기**를 변환 하는 스키마를 선택 합니다.

![스키마 변환](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>데이터베이스 동기화

다음으로 데이터베이스를 동기화 합니다.

1. 변환이 완료 되 면 사용 된 **SQL Server 메타 데이터 탐색기** 이전 단계에서 만든 데이터베이스를 이동 합니다.

1. 선택한 데이터베이스를 마우스 오른쪽 단추로 클릭 **데이터베이스와 동기화**, 확인을 클릭 하 고 있습니다.

   ![데이터베이스와 동기화](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>데이터 마이그레이션

마지막 단계는 데이터를 마이그레이션하는 것입니다.

1. 에 **Oracle 메타 데이터 탐색기**를 마우스 오른쪽 단추로 클릭 **HR**를 선택한 **데이터 마이그레이션**합니다.

1. 데이터 마이그레이션 단계는 Oracle 및 SQL Server 자격 증명을 다시 입력 해야 합니다.

1. 완료 되 면 다음 스크린샷과 유사 데이터 마이그레이션 보고서를 검토 합니다.

   ![데이터 마이그레이션 보고서](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>다음 단계

더 복잡 한 Orcale 스키마의 경우 변환 프로세스는 자세한 시간, 테스트 및 클라이언트 응용 프로그램 변경이 발생할에 포함 됩니다. 이 자습서의 용도 전체 마이그레이션 프로세스의 일부로 Oracle 용 SSMA를 사용 하는 방법을 보여 줍니다.

이 자습서에서는 학습 하는 방법.
> [!div class="checklist"]
> * SSMA Windows 설치
> * 새 SSMA 프로젝트 만들기
> * 평가 하 고 Oracle 로부터 마이그레이션 실행

다음으로, SSMA를 사용 하는 다른 방법 살펴보기

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant 설명서](../sql-server-migration-assistant.md)
