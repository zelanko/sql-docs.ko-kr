---
title: Linux에 PolyBase 설치
titlesuffix: SQL Server
description: 이 문서에서는 Linux에 SQL Server PolyBase를 설치하는 방법을 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.date: 7/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f72635a68b0b47a29151d45d2bf1e32e85c1f1bc
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823578"
---
# <a name="install-polybase-on-linux"></a>Linux에 PolyBase 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

다음 단계에서는 Linux에 [PolyBase](../../relational-databases/search/full-text-search.md)(**mssql server polybase**)를 설치합니다. PolyBase를 사용하면 원격 데이터 원본에 대해 외부 쿼리를 실행할 수 있습니다. 

>[!NOTE]
> Polybase를 설치하기 전에 먼저 [SQL Server 2019 미리 보기를 설치](../../linux/sql-server-linux-setup.md#platforms)합니다. 이렇게 하면 **mssql-server-polybase** 패키지를 설치할 때 사용하는 키 및 리포지토리가 구성됩니다.
>
> PolyBase는 Linux 용 SQL Server 2017에서 지원되지 않습니다.
> Linux에서 PolyBase용 스케일 아웃은 현재 사용할 수 없습니다.

운영 체제에 맞는 PolyBase 설치:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)



## <a name=""></a><a name="RHEL">RHEL에 설치</a>

다음 명령을 사용하여 Red Hat Enterprise Linux에 **mssql-server-polybase**를 설치합니다. 

```bash
sudo yum install -y mssql-server-polybase
```

SQL Server 인스턴스를 다시 시작하라는 메시지가 표시됩니다. 이렇게 하려면 다음 명령을 사용합니다.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>설치 후 [PolyBase 기능을 사용하도록 설정](#enable)해야 합니다.

오프라인 설치가 필요한 경우 [릴리스 정보](../../linux/sql-server-linux-release-notes.md)에서 PolyBase 패키지 다운로드를 찾습니다. 그런 다음, [SQL Server 설치](../../linux/sql-server-linux-setup.md#offline) 문서에 설명된 것과 동일한 오프라인 설치 단계를 사용합니다.

## <a name=""></a><a name="ubuntu">Ubuntu에 설치</a>

다음 명령을 사용하여 Ubuntu에 **mssql-server-polybase**를 설치합니다. 

```bash
sudo apt-get install mssql-server-polybase
```

SQL Server 인스턴스를 다시 시작하라는 메시지가 표시됩니다. 이렇게 하려면 다음 명령을 사용합니다.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>설치 후 [PolyBase 기능을 사용하도록 설정](#enable)해야 합니다.

오프라인 설치가 필요한 경우 [릴리스 정보](../../linux/sql-server-linux-release-notes.md)에서 PolyBase 패키지 다운로드를 찾습니다. 그런 다음, [SQL Server 설치](../../linux/sql-server-linux-setup.md#offline) 문서에 설명된 것과 동일한 오프라인 설치 단계를 사용합니다.

## <a name=""></a><a name="SLES">SLES에 설치</a>

다음 명령을 사용하여 SUSE Linux Enterprise Server에 **mssql-server-polybase**를 설치합니다. 

```bash
sudo zypper install mssql-server-polybase
```

SQL Server 인스턴스를 다시 시작하라는 메시지가 표시됩니다. 이렇게 하려면 다음 명령을 사용합니다.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>설치 후 [PolyBase 기능을 사용하도록 설정](#enable)해야 합니다.


오프라인 설치가 필요한 경우 [릴리스 정보](../../linux/sql-server-linux-release-notes.md)에서 PolyBase 패키지 다운로드를 찾습니다. 그런 다음, [SQL Server 설치](../../linux/sql-server-linux-setup.md#offline) 문서에 설명된 것과 동일한 오프라인 설치 단계를 사용합니다.


## <a name=""></a><a name="enable">PolyBase 사용</a> 

설치 후 PolyBase를 활성화하여 해당 기능에 액세스해야 합니다. 설치된 SQL Server 인스턴스에 연결하고 다음 Transact-SQL 명령을 사용하여 활성화합니다.

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="update-polybase"></a>PolyBase 업데이트

**mssql server polybase**가 이미 설치된 경우 다음 명령을 사용하여 최신 버전으로 업데이트할 수 있습니다.

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
```

SQL Server 인스턴스를 다시 시작하라는 메시지가 표시됩니다. 이렇게 하려면 다음 명령을 사용합니다.

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
```

SQL Server 인스턴스를 다시 시작하라는 메시지가 표시됩니다. 이렇게 하려면 다음 명령을 사용합니다.

```
sudo systemctl restart mssql-server
```

### <a name="sles"></a>SLES

```bash
sudo zypper remove mssql-server-polybase
sudo zypper refresh
sudo zypper install mssql-server-polybase
```

SQL Server 인스턴스를 다시 시작하라는 메시지가 표시됩니다. 이렇게 하려면 다음 명령을 사용합니다.

```
sudo systemctl restart mssql-server
```

>[!NOTE]
>설치 후 [PolyBase 기능을 사용하도록 설정](#enable)해야 합니다.

## <a name="next-steps"></a>다음 단계

Linux의 PolyBase는 다음 데이터 원본에 액세스할 수 있습니다. PolyBase에서 이러한 소스로 외부 테이블을 만드는 방법에 대한 자세한 내용은 제공된 링크를 따릅니다. 

- [SQL Server(및 SQL Database, Azure SQL Data Warehouse)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB(및 Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

이 항목의 사용 방법에 대한 자세한 내용은 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)의 Transact-SQL 참조 문서를 참조하세요.
