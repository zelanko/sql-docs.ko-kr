---
title: 와이드 세계 가져오기-SQL 용 샘플 데이터베이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 872892d307883bb7df31b08de701b2030d9aeb1f
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794600"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Microsoft SQL 용 와이드 세계 가져오기 샘플 데이터베이스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
SQL Server 및 Azure SQL Database에 대 한 WideWorldImporters 예제 데이터베이스에서 해결 된 가상의 회사 전체 가져오기 및 워크플로에 대 한 개요입니다.  

WWI (와이드 세계 가져오기)는 샌프란시스코 베이 영역에서 작동 하는 도매 새로 움 상품 가져오기 및 배포자입니다.

Wholesaler, WWI 고객은 대부분 개인에 게 재판매 하는 회사입니다. WWI는 특수 매장, supermarkets, 컴퓨팅 매장, tourist 인력 상점 및 일부 개인을 포함 하 여 미국에서 소매 고객에 게 판매 합니다. WWI는 또한 WWI를 대신 하 여 제품을 홍보 하는 에이전트 네트워크를 통해 다른 프랜차이즈에 판매 합니다. 모든 WWI 고객은 현재 미국에 기반 하 고 있지만 다른 국가로 확장 하기 위해이 회사를 푸시하는 것이 좋습니다.

WWI는 새로 움 및 장난감 제조업체와 기타 새로 움 프랜차이즈를 포함 하 여 공급 업체의 상품을 구입 합니다. 이는 WWI 웨어하우스에서 상품을 재고 하 고, 필요에 따라 고객 주문을 수행할 하 여 공급 업체의 순서를 변경 합니다. 또한 대용량 포장 자료를 구매 하 고 고객의 편의를 위해 이러한 자료를 작은 수량으로 판매 합니다.

최근 WWI는 chilli 빠졌습니다과 같은 다양 한 novelties를 판매 하기 시작 했습니다.  이전에는 회사에서 chilled 항목을 처리할 필요가 없습니다. 이제 음식 처리 요구 사항을 충족 하기 위해 냉각기 실내의 온도와 냉각기 섹션을 포함 하는 트럭을 모니터링 해야 합니다.

## <a name="workflow-for-warehouse-stock-items"></a>웨어하우스 재고 항목에 대 한 워크플로

항목의 보충 및 배포 방법에 대 한 일반적인 흐름은 다음과 같습니다.
- WWI는 구매 주문을 만들고 해당 주문을 공급자에 게 제출 합니다.
- 공급 업체는 항목을 보내고, WWI는 항목을 수신 하 고 창 고 합니다.
- WWI에서 항목 주문 하는 고객
- WWI는 웨어하우스의 재고 항목으로 고객 주문을 채우고, 재고가 충분 하지 않은 경우 suppliers에서 추가 재고를 주문 합니다.
- 일부 고객은 재고가 없는 항목에 대해 대기 하지 않으려고 합니다. 5 개의 다른 재고 항목을 표시 하 고 4를 사용할 수 있는 경우 4 개의 항목을 받고 나머지 항목의 순서를 역순으로 만들려고 합니다. 그런 다음 항목은 나중에 별도의 배송에서 전송 됩니다.
- WWI는 일반적으로 주문을 송장으로 변환 하 여 재고 항목에 대 한 고객을 송장으로 변환 합니다.
- 고객이 재고가 없는 항목을 주문할 수 있습니다. 이러한 항목은 backordered입니다.
- WWI는 자체 배달 vans를 통하거나 다른 고객 또는 운임 메서드를 통해 재고 항목을 고객에 게 제공 합니다.
- 고객은 WWI로 송장을 지불 합니다.
- 정기적으로 WWI는 구매 주문서에 있던 항목에 대 한 공급자를 지불 합니다. 이는 상품을 받은 후에 종종 발생 합니다.

## <a name="data-warehouse-and-analysis-workflow"></a>데이터 웨어하우스 및 분석 워크플로

WWI의 팀은 SQL Server Reporting Services를 사용 하 여 WideWorldImporters 데이터베이스에서 작업 보고서를 생성 하는 동안에도 데이터에 대 한 분석을 수행 하 고 전략적 보고서를 생성 해야 합니다. 팀이 데이터베이스 WideWorldImportersDW에 차원 데이터 모델을 만들었습니다. 이 데이터베이스는 Integration Services 패키지로 채워집니다.

SQL Server Analysis Services는 차원 데이터 모델의 데이터에서 분석 데이터 모델을 만드는 데 사용 됩니다. SQL Server Reporting Services는 차원 데이터 모델에서 직접 전략적 보고서를 생성 하는 데 사용 되 고 분석 모델 에서도 사용 됩니다. Power BI는 동일한 데이터에서 대시보드를 만드는 데 사용 됩니다. 대시보드는 웹 사이트 및 휴대폰 및 태블릿에서 사용 됩니다. *참고: 이러한 데이터 모델 및 보고서는 아직 사용할 수 없습니다.*

## <a name="additional-workflows"></a>추가 워크플로

추가 워크플로는 다음과 같습니다.
- WWI는 고객이 어떤 이유로 든 지 나 상품에 문제가 발생 한 경우 크레딧 정보를 발급 합니다. 이는 부정 송장으로 처리 됩니다.
- WWI는 시스템에서 사용 가능한 것으로 표시 된 주식 수량이 정확한 지 확인 하기 위해 재고 항목의 재고 수량을 주기적으로 계산 합니다. (이 작업을 수행 하는 프로세스를 stocktake 라고 합니다.)
- 냉 실내 온도. Perishable 상품은 refrigerated 방에 저장 됩니다. 이러한 방에 있는 센서 데이터는 모니터링 및 분석을 위해 데이터베이스에 수집 됩니다.
- 차량 위치 추적. WWI 용 상품을 전송 하는 차량에는 위치를 추적 하는 센서가 포함 됩니다. 이 위치는 모니터링 및 추가 분석을 위해 데이터베이스에 다시 수집 됩니다.

## <a name="fiscal-year"></a>회계 연도

이 회사는 11 월 1 일에 시작 하는 재무 연도를 사용 합니다.

## <a name="terms-of-use"></a>사용 약관

예제 데이터베이스 및 예제 코드에 대 한 라이선스는 다음에 설명 되어 있습니다. [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

예제 데이터베이스에는 data.gov 및 자연 EarthData에서 로드 된 공용 데이터가 포함 되어 있습니다. 사용 약관은 다음과 같습니다.[https://www.naturalearthdata.com/about/terms-of-use/](https://www.naturalearthdata.com/about/terms-of-use/)
