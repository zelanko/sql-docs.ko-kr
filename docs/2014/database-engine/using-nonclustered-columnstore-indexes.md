---
title: 비클러스터형 Columnstore 인덱스 사용 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 4c341fb8-7cb1-4cab-921b-e80b751d6c19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c190e95df57c80d29428b39b72a4115ac7d23de1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175352"
---
# <a name="using-nonclustered-columnstore-indexes"></a>비클러스터형 columnstore 인덱스 사용
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 테이블에서 비클러스터형 columnstore 인덱스를 사용하기 위한 주요 태스크를 설명합니다.

 columnstore 인덱스에 대한 개요는 [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md)를 참조하십시오.

 클러스터형 columnstore 인덱스에 대한 자세한 내용은 [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md)을 참조하십시오.

## <a name="contents"></a>콘텐츠

-   [비클러스터형 Columnstore 인덱스 만들기](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)

-   [비클러스터형 Columnstore 인덱스의 데이터 변경](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)

##  <a name="create-a-nonclustered-columnstore-index"></a><a name="load"></a>비클러스터형 Columnstore 인덱스 만들기
 비클러스터형 columnstore 인덱스로 데이터를 로드 하려면 먼저 힙 또는 클러스터형 인덱스로 저장 된 기존의 rowstore 테이블로 데이터를 로드 한 다음 [CREATE COLUMNSTORE index &#40;transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql) 를 사용 하 여 columnstore 인덱스를 만듭니다.

 ![데이터를 columnstore 인덱스로 로드](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "데이터를 columnstore 인덱스로 로드")

##  <a name="change-the-data-in-a-nonclustered-columnstore-index"></a><a name="change"></a>비클러스터형 Columnstore 인덱스의 데이터 변경
 테이블에 비클러스터형 columnstore 인덱스를 만든 후에는 해당 테이블에서 데이터를 직접 수정할 수 없습니다. INSERT, UPDATE, DELETE 또는 MERGE를 사용한 쿼리는 실패하며 오류 메시지를 반환합니다. 테이블에서 데이터를 추가하거나 수정하려면 다음 중 하나를 수행합니다.

-   Columnstore 인덱스를 사용 하지 않도록 설정 합니다. 그런 다음 테이블에서 데이터를 업데이트할 수 있습니다. columnstore 인덱스를 사용하지 않도록 설정하는 경우 데이터 업데이트를 완료할 때 columnstore 인덱스를 다시 작성할 수 있습니다. 예를 들면 다음과 같습니다.

    ```
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;
    -- update mytable --
    ALTER INDEX mycolumnstoreindex on mytable REBUILD
    ```

-   Columnstore 인덱스를 삭제 하 고 테이블을 업데이트 한 다음 CREATE COLUMNSTORE INDEX를 사용 하 여 columnstore 인덱스를 다시 만듭니다. 예를 들면 다음과 같습니다.

    ```
    DROP INDEX mycolumnstoreindex ON mytable
    -- update mytable --
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;

    ```

-   columnstore 인덱스가 없는 준비 테이블에 데이터를 로드합니다. 준비 테이블에서 columnstore 인덱스를 작성합니다. 준비 테이블을 주 테이블의 빈 파티션으로 전환합니다.

-   columnstore 인덱스가 있는 테이블에서 빈 준비 테이블로 파티션을 전환합니다. 준비 테이블에 columnstore 인덱스가 있는 경우 columnstore 인덱스를 사용하지 않도록 설정합니다. 업데이트를 수행합니다. columnstore 인덱스를 작성 또는 다시 작성합니다. 준비 테이블을 주 테이블의 파티션(현재 비어 있음)으로 다시 전환합니다.




