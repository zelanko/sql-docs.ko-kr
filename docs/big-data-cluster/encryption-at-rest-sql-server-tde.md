---
title: SQL Server 빅 데이터 클러스터 TDE(투명한 데이터 암호화) 미사용 데이터 암호화 사용 가이드
titleSuffix: SQL Server Big Data Clusters
description: 이 문서에서는 BDC의 SQL Server TDE 미사용 데이터 암호화 기능을 사용하는 방법을 보여 줍니다.
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 55456185a6503ee11465a1e65cb9cd91de3ba6e2
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199584"
---
# <a name="sql-server-big-data-clusters-transparent-data-encryption-tde-at-rest-usage-guide"></a>SQL Server 빅 데이터 클러스터 TDE(투명한 데이터 암호화) 미사용 데이터 암호화 사용 가이드

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 가이드에서는 SQL Server 빅 데이터 클러스터의 미사용 데이터 암호화 기능을 통해 데이터베이스를 암호화하는 방법을 보여 줍니다.

환경은 일반적으로 SQL Server on Linux와 동일하며 따로 명시하지 않은 한 [표준 TDE 설명서](../relational-databases/security/encryption/transparent-data-encryption.md)가 적용됩니다. 마스터의 암호화 상태를 모니터링하려면 [`sys.dm_database_encryption_keys`](../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 및 [`sys.certificates`](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)를 기반으로 한 표준 DMV 쿼리 패턴을 따릅니다.

__지원되지 않는 기능:__
* 데이터 풀 암호화
* [HA 배포](deployment-high-availability.md)에서 포함된 가용성 그룹의 데이터베이스에 대한 암호화 키 회전


## <a name="prerequisites"></a><a id="prereqs"></a> 필수 조건

- [SQL Server 빅 데이터 클러스터 CU8+](release-notes-big-data-cluster.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
   - **Azure Data Studio**
- SQL Server 및 관리자 권한이 있는 사용자

## <a name="query-the-installed-certificates"></a>설치된 인증서 쿼리

1. Azure Data Studio에서 빅 데이터 클러스터의 SQL Server 마스터 인스턴스에 연결합니다. 자세한 내용은 [SQL Server 마스터 인스턴스에 연결](connect-to-big-data-cluster.md#master)을 참조하세요.

1. **서버** 창에서 연결을 두 번 클릭하여 SQL Server 마스터 인스턴스의 서버 대시보드를 표시합니다. **새 쿼리** 를 선택합니다.

   ![SQL Server 마스터 인스턴스 쿼리](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. 다음 Transact-SQL 명령을 실행하여 마스터 인스턴스의 **마스터** 데이터베이스로 컨텍스트를 변경합니다.

   ```sql
   USE master
   GO
   ```

1. 설치된 시스템 관리형 인증서를 쿼리합니다. 

   ```sql
    SELECT TOP 1 name FROM sys.certificates WHERE name LIKE 'TDECertificate%' ORDER BY name DESC
   ```

    필요에 따라 다른 쿼리 조건을 사용하세요.

    인증서 이름은 "TDECertificate{timestamp}"로 표시됩니다. TDECertificate 접두사 및 타임스탬프가 표시되 면 시스템 관리형 기능에서 제공하는 인증서입니다.

## <a name="encrypt-a-database-using-the-system-provided-certificate"></a>시스템 제공 인증서를 사용하여 데이터베이스 암호화

다음 예제에서는 __userdb__ 라는 데이터베이스를 암호화 대상으로 고려하고 이전 섹션의 출력에서 __TDECertificate2020_09_15_22_46_27__ 이라는 시스템 제공 인증서를 고려합니다.

1. 다음 패턴을 사용하여 제공된 시스템 인증서로 데이터베이스 암호화 키를 생성합니다.

   ```sql
    USE userdb; 
    GO
    CREATE DATABASE ENCRYPTION KEY WITH ALGORITHM = AES_256 ENCRYPTION BY SERVER CERTIFICATE TDECertificate2020_09_15_22_46_27;
    GO
   ```

1. 다음 명령을 사용하여 데이터베이스 __userdb__ 를 암호화합니다.

   ```sql
    ALTER DATABASE userdb SET ENCRYPTION ON;
    GO
   ```

## <a name="next-steps"></a>다음 단계

HDFS용 미사용 데이터 암호화에 대해 알아봅니다.
> [!div class="nextstepaction"]
> [HDFS 암호화 영역](encryption-at-rest-hdfs-encryption-zones.md)
