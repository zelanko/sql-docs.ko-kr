---
title: Analytics Platform System의 공통 부분식 설명 | Microsoft Docs
description: 분석 플랫폼 시스템 CU7.3에 도입 된 표시 예제 쿼리 개선
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 12/17/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 2dd02bed55f3d3781428eae3ec4bc2d0655819ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312466"
---
# <a name="common-subexpression-elimination-explained"></a>공용 부분식 제거 설명

AP CU7.3 SQL 쿼리 최적화 프로그램의 공용 부분식 제거를 사용 하 여 쿼리 성능을 향상 시킵니다. 향상 두 가지 방법으로 쿼리를 개선합니다. 첫 번째 이점은 식별 하 고 제거 하는 등 있다는 점입니다 식 SQL 컴파일 시간을 줄이는 데 도움이 됩니다. 두 번째 및 더 중요 한 장점은 쿼리가 더 빠르게 됩니다에 대 한 이러한 중복 하위 식에 대 한 데이터 이동 작업 실행 시간에 따라서 제거 됩니다.

```sql
select top 100 asceding.rnk, i1.i_product_name best_performing, i2.i_product_name worst_performing
  from(select *
       from (select item_sk,rank() over (order by rank_col asc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V1)V11
       where rnk  < 11) asceding,
      (select *
       from (select item_sk,rank() over (order by rank_col desc) rnk
             from (select ss_item_sk item_sk,avg(ss_net_profit) rank_col
                   from store_sales ss1
                   where ss_store_sk = 8
                   group by ss_item_sk
                   having avg(ss_net_profit) > 0.9*(select avg(ss_net_profit) rank_col
                                                    from store_sales
                                                    where ss_store_sk = 8
                                                      and ss_hdemo_sk is null
                                                    group by ss_store_sk))V2)V21
       where rnk  < 11) descending,
  item i1,
  item i2
  where asceding.rnk = descending.rnk
    and i1.i_item_sk=asceding.item_sk
    and i2.i_item_sk=descending.item_sk
  order by asceding.rnk
  ;
```
TPC-DS 벤치 마크 도구에서 위의 쿼리를 살펴보십시오.  위의 쿼리에서 하위 동일 하지만 order by와 함수를 통해을 사용 하 여 절에 두 가지 방법으로 정렬 됩니다. CU7.3, 이전에이 하위 쿼리를 계산 하 고 오름차순 및 내림차순에 대 한 두 가지 데이터 이동 작업을 발생 한 번에 한 번 실행을 두 번 가져오기 됩니다. AP CU7.3를 설치한 후 데이터 이동을 줄이고 더 빠른 쿼리를 완료 합니다. 따라서 한 번 하위 파트를 평가 됩니다.

도입 했습니다를 [기능 스위치가](appliance-feature-switch.md) 'OptimizeCommonSubExpressions' 하는 호출을 AP CU7.3로 업그레이드 한 후에 기능을 테스트 하면 합니다. 기능을 기본적으로 켜져 있지만 해제할 수 있습니다. 

> [!NOTE] 
> 기능 스위치 값 변경에는 서비스를 다시 시작을 해야합니다.

다음 표에서 테스트 환경에서 만들고 위에 언급 한 쿼리에 대해 explain 계획을 평가 하 여 샘플 쿼리를 시도할 수 있습니다. 

```sql
CREATE TABLE [dbo].[store_sales] (
    [ss_sold_date_sk] int NULL, 
    [ss_sold_time_sk] int NULL, 
    [ss_item_sk] int NOT NULL, 
    [ss_customer_sk] int NULL, 
    [ss_cdemo_sk] int NULL, 
    [ss_hdemo_sk] int NULL, 
    [ss_addr_sk] int NULL, 
    [ss_store_sk] int NULL, 
    [ss_promo_sk] int NULL, 
    [ss_ticket_number] int NOT NULL, 
    [ss_quantity] int NULL, 
    [ss_wholesale_cost] decimal(7, 2) NULL, 
    [ss_list_price] decimal(7, 2) NULL, 
    [ss_sales_price] decimal(7, 2) NULL, 
    [ss_ext_discount_amt] decimal(7, 2) NULL, 
    [ss_ext_sales_price] decimal(7, 2) NULL, 
    [ss_ext_wholesale_cost] decimal(7, 2) NULL, 
    [ss_ext_list_price] decimal(7, 2) NULL, 
    [ss_ext_tax] decimal(7, 2) NULL, 
    [ss_coupon_amt] decimal(7, 2) NULL, 
    [ss_net_paid] decimal(7, 2) NULL, 
    [ss_net_paid_inc_tax] decimal(7, 2) NULL, 
    [ss_net_profit] decimal(7, 2) NULL
)
WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH([ss_item_sk]),  PARTITION ([ss_sold_date_sk] RANGE RIGHT FOR VALUES (2450815, 2451180, 2451545, 2451911, 2452276, 2452641, 2453006)));

CREATE TABLE [dbo].[item] (
    [i_item_sk] int NOT NULL, 
    [i_item_id] char(16) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, 
    [i_rec_start_date] date NULL, 
    [i_rec_end_date] date NULL, 
    [i_item_desc] varchar(200) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_current_price] decimal(7, 2) NULL, 
    [i_wholesale_cost] decimal(7, 2) NULL, 
    [i_brand_id] int NULL, 
    [i_brand] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_class_id] int NULL, 
    [i_class] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_category_id] int NULL, 
    [i_category] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manufact_id] int NULL, 
    [i_manufact] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_size] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_formulation] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_color] char(20) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_units] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_container] char(10) COLLATE Latin1_General_100_CI_AS_KS_WS NULL, 
    [i_manager_id] int NULL, 
    [i_product_name] char(50) COLLATE Latin1_General_100_CI_AS_KS_WS NULL
)
WITH (CLUSTERED INDEX ( [i_item_sk] ASC ), DISTRIBUTION = REPLICATE);
```
쿼리 작업 및 CU7.3 후 (또는 설정 기능 스위치를 사용 하 여) 17 총 수는 쿼리의 explain 계획 살펴보면, CU7.3 하기 전에 확인할 수 있습니다 (또는 기능 스위치가 해제 되었습니다 하는 경우) 하는 경우 동일한 쿼리 9 총 작업 수를 보여 줍니다. 데이터 이동 작업을 세기만 하는 경우 이전 계획이 새 계획의 두 이동 작업 및 네 개의 이동 작업에 표시 됩니다. 새로운 쿼리 최적화는 쿼리 런타임의 줄이기 새 계획을 사용 하 여 만든 임시 테이블을 다시 사용 하 여 두 데이터 이동 작업을 줄일 수 있었습니다. 


