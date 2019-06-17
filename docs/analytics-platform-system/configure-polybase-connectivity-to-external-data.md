---
title: Analytics Platform System-PolyBase 연결 구성 | Microsoft Docs
description: 외부 Hadoop 또는 Microsoft Azure storage blob 데이터 원본에 연결할 Parallel Data Warehouse에서 PolyBase를 구성 하는 방법을 설명 합니다. PolyBase를 사용 하 여 Hadoop, Azure blob storage 및 병렬 데이터 웨어하우스를 포함 하 여 여러 원본에서 데이터를 통합 하는 쿼리를 실행 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da6d71521f72ff23b4caf2f27dbc663dee684592
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057821"
---
# <a name="what-is-polybase"></a>PolyBase란?
PolyBase에 Analytics Platform System (APS)에서 데이터를 읽고 외부 데이터 원본에 데이터를 쓸 수 있는 TRANSACT-SQL 쿼리를 처리할 수 있습니다. 외부 데이터에 액세스 하는 동일한 쿼리에 AP에서 관계 테이블을 포함할 수도 있습니다. 이 통해 높은 가치의 AP 데이터베이스에서 관계형 데이터를 사용 하 여 외부 원본의 데이터를 결합할 수 있습니다.

![PolyBase 논리](media/polybase/polybase-logical.png)

AP에서 PolyBase에는 읽기 및 쓰기 파일 시스템 HDFS (Hadoop) 및 Azure Blob Storage를 지원 합니다. PolyBase에는 전체 쿼리 성능을 최적화 하기 위해 mapreduce 작업으로 Hadoop 노드를 몇 가지 계산을 푸시할 수가 있습니다. AP에 PolyBase 파일 구분 기호로 분리 된 텍스트, ORC 및 Parquet에서 작동할 수 있습니다. 참조 [PolyBase 란](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) 전체 설명과 해당 기능에 대 한 합니다.

> [!NOTE]
> AP는 현재 지원 표준 범용 v1 로컬 중복 (LRS) Azure Blob Storage입니다.

## <a name="features-and-limitations"></a>기능 및 제한 사항
참조 [기능 및 제한 사항](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary) PolyBase 요약이 AP 및 기타 SQL Server 제품에 대 한 사용 가능 하 고 알려진 제한입니다.

> [!NOTE] 
> PolyBase의 나머지를 관련 문서에서는 이상 APS 2016 (AU6)에서 PolyBase를 구성 하는 방법.

## <a name="see-also"></a>관련 항목
- [Hadoop](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
