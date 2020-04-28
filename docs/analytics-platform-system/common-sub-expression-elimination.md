---
title: 공통 하위 식
description: 분석 플랫폼 시스템 CU 7.3에 도입 된 예제 쿼리 개선 사항을 표시 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 12/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: d05314f4d100e469c621d42a10ed89671b2bdd9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401330"
---
# <a name="common-subexpression-elimination-explained"></a>Common 부분식 제거 설명

APS CU 7.3은 SQL 쿼리 최적화 프로그램에서 일반적인 하위 식 제거를 사용 하 여 쿼리 성능을 향상 시킵니다. 향상 된 기능은 두 가지 방법으로 쿼리를 향상 시킵니다. 첫 번째 혜택은 이러한 식을 확인 하 고 제거 하는 기능을 통해 SQL 컴파일 시간을 단축 하는 것입니다. 두 번째와 더 중요 한 혜택은 이러한 중복 부분식에 대 한 데이터 이동 작업은 제거 되므로 쿼리의 실행 시간이 더 빨라집니다.

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
TPC-DS 벤치 마크 도구에서 위의 쿼리를 참조 하세요.  위의 쿼리에서 하위 쿼리는 동일 하지만 rank () over 함수를 사용 하는 order by 절은 서로 다른 두 가지 방법으로 정렬 됩니다. CU 7.3 이전에는이 하위 쿼리를 평가 하 고 두 번 실행 합니다. 오름차순으로 한 번, 내림차순으로 한 번, 두 개의 데이터 이동 작업을 발생 시킵니다. APS CU 7.3을 설치한 후에는 하위 쿼리 부분이 한 번 평가 되어 데이터 이동이 줄어들고 쿼리가 더 빨리 완료 됩니다.

APS CU 7.3로 업그레이드 한 후에도 기능을 테스트 하는 데 사용할 수 있는 ' OptimizeCommonSubExpressions ' 라는 [기능 스위치](appliance-feature-switch.md) 를 도입 했습니다. 이 기능은 기본적으로 켜져 있지만 해제할 수 있습니다. 

> [!NOTE] 
> 기능 스위치 값을 변경 하려면 서비스를 다시 시작 해야 합니다.

테스트 환경에서 다음 테이블을 만들고 위의 설명 된 쿼리에 대 한 설명 계획을 평가 하 여 샘플 쿼리를 시도할 수 있습니다. 

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
쿼리의 설명 계획을 살펴보면 CU 7.3 이전에 (또는 기능 스위치가 해제 된 경우) 쿼리는 총 작업 수 17 개, CU 7.3 이후, 즉 기능 스위치가 설정 된 상태에서 동일한 쿼리는 총 9 개의 작업 수를 표시 합니다. 데이터 이동 작업을 계산 하는 경우에는 이전 계획에 두 개의 이동 작업과 두 개의 이동 작업이 새 계획에 포함 된 것을 알 수 있습니다. 새 쿼리 최적화 프로그램은 새 계획으로 이미 만든 임시 테이블을 다시 사용 하 여 두 데이터 이동 작업을 줄일 수 있으므로 쿼리 런타임이 줄어듭니다. 


