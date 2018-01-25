---
title: "데이터베이스 크기 예측 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- space allocation [SQL Server], database size
- calculating database size
- increasing database size
- database size [SQL Server], estimating
- predicting database size
- size [SQL Server], databases
- estimating database size
- designing databases [SQL Server], estimating size
ms.assetid: 5b240161-eba4-44b0-946c-61a8fc00fc8c
caps.latest.revision: "20"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1fd8ebd7223c44cdfb5b830ae0f9fc5ea08f3266
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="estimate-the-size-of-a-database"></a>데이터베이스 크기 예측
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 데이터베이스를 디자인할 때는 데이터베이스가 데이터로 가득 찰 때 얼마나 커질 수 있는지를 추정해야 합니다. 데이터베이스의 크기를 추정하면 다음을 수행하는 데 필요한 하드웨어 구성을 결정하는 데 도움이 됩니다.  
  
-   응용 프로그램에서 필요한 성능을 확보합니다.  
  
-   데이터 및 인덱스를 저장하는 데 필요한 물리적 디스크 공간을 충분히 확보합니다.  
  
 또한 데이터베이스의 크기를 추정하면 데이터베이스 디자인을 수정해야 할지 여부를 결정할 수 있습니다. 예를 들어 예상 크기가 회사에서 실제로 구현하기에 너무 큰 경우에는 정규화가 더 필요하다는 것을 알 수 있습니다. 반대로 예상 크기가 생각보다 더 작을 수도 있습니다. 이 경우 데이터베이스를 비정규화하여 쿼리 성능을 높일 수 있습니다.  
  
 데이터베이스의 크기를 추정하려면 각 테이블의 크기를 따로 추정한 다음 그 값을 더하면 됩니다. 테이블의 크기는 테이블에 인덱스가 있는지 여부와 인덱스 유형에 따라 달라집니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[테이블 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-table.md)|테이블 및 연결된 인덱스에 데이터를 저장하는 데 필요한 공간을 예측하는 단계와 필요한 계산을 설명합니다.|  
|[힙 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-heap.md)|힙에 데이터를 저장하는 데 필요한 공간을 예측하는 단계와 필요한 계산을 설명합니다. 힙은 클러스터형 인덱스가 없는 테이블입니다.|  
|[클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)|클러스터형 인덱스에 데이터를 저장하는 데 필요한 공간을 예측하는 단계와 필요한 계산을 설명합니다.|  
|[비클러스터형 인덱스의 크기 예측](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)|비클러스터형 인덱스에 데이터를 저장하는 데 필요한 공간을 예측하는 단계와 필요한 계산을 설명합니다.|  
  
  
