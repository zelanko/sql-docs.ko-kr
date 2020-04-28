---
title: PolyBase 연결 구성
description: 외부 Hadoop 또는 Microsoft Azure storage blob 데이터 원본에 연결 하도록 병렬 데이터 웨어하우스에서 PolyBase를 구성 하는 방법을 설명 합니다. PolyBase를 사용 하 여 Hadoop, Azure blob storage 및 병렬 데이터 웨어하우스를 비롯 한 여러 원본의 데이터를 통합 하는 쿼리를 실행 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3b754fb2de33a230bc7d27f239b2778d2849fd5a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401271"
---
# <a name="what-is-polybase"></a>PolyBase란?
PolyBase를 사용 하면 AP (분석 플랫폼 시스템)에서 데이터를 읽고 외부 데이터 원본에 데이터를 쓸 수 있는 Transact-sql 쿼리를 처리할 수 있습니다. 외부 데이터에 액세스 하는 동일한 쿼리는 AP에 관계 테이블을 포함할 수도 있습니다. 이를 통해 외부 원본의 데이터를 APS 데이터베이스의 상위 값 관계형 데이터와 결합할 수 있습니다.

![PolyBase 논리](media/polybase/polybase-logical.png)

APS의 PolyBase는 Hadoop (HDFS) 파일 시스템 및 Azure Blob Storage에 대 한 읽기 및 쓰기를 지원 합니다. 또한 PolyBase는 전체 쿼리 성능을 최적화 하기 위해 Hadoop 노드에 일부 계산을 mapreduce 작업으로 푸시할 수 있습니다. APS의 PolyBase는 분리 된 텍스트, ORC 및 Parquet 파일에 대해 작동할 수 있습니다. 전체 설명 및 해당 기능에 대 한 자세한 내용은 [PolyBase 란?](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) 을 참조 하세요.

> [!NOTE]
> APS는 현재 표준 범용 v1 LRS (로컬 중복) Azure Blob Storage 지원 합니다.

## <a name="features-and-limitations"></a>기능 및 제한 사항
사용 가능한 PolyBase 기능 요약 및 AP 및 기타 SQL Server 제품에 대 한 알려진 제한 사항에 대 한 [기능 및 제한](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary) 사항을 참조 하세요.

> [!NOTE] 
> PolyBase 관련 문서의 나머지 부분에서는 AU6 (APS 2016) 이상에서 PolyBase를 구성 하는 방법을 대해 설명.

## <a name="see-also"></a>참고 항목
- [Hadoop은](polybase-configure-hadoop.md)
- [Azure Blob Storage](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
