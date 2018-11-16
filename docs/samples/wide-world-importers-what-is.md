---
title: Wide World Importers-sql 예제 데이터베이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 017f301d9888ddd4f90d70e7d993faf840640a66
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670692"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Microsoft sql wide World Importers 예제 데이터베이스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
이것이 회사인 Wide World Importers 및 WideWorldImporters 샘플 데이터베이스는 SQL Server 및 Azure SQL Database에 대 한 주소가 지정 된 워크플로 개요입니다.  

Wide World Importers (WWI)는 도매 새로 움 상품 가져오기 샌프란시스코 베이 영역에서 운영 하는 배포자입니다.

도매업,으로 WWI의 고객에 게는 개인에 게 재판매 하는 회사 대부분입니다. WWI 판매 소매 고객에 게 전문 저장소 슈퍼마켓을 비롯 한 미국에서 컴퓨팅, 저장소, 여행자 인력 상점 및 일부 사용자에 게 합니다. 또한 WWI 네트워크 WWI의 대신 제품을 홍보 하는 에이전트를 통해 다른 프랜차이즈를 판매 합니다. WWI의 고객의 모든 현재 미국의 기반으로 하는 동안 회사 다른 국가에 대 한 확장에 대 한 적용할 예정입니다.

WWI 새로 움 장난감 제조업체 및 기타 새로 움 프랜차이즈를 포함 하 여 공급 업체에서 제품을 구입 합니다. 스톡 고객 주문을 수행할 수 있도록 하는 데 필요한 대로 WWI 웨어하우스 및 공급 업체에서 다시 정렬에서 상품 합니다. 또한 많은 양의 자료, 패키지를 구입 하 고 고객에 대 한 편의 위해 더 작은 수량에서 이러한 판매 합니다.

최근에 WWI 식용 novelties chilli 등의 다양 한 초콜릿 판매 하기 시작 했습니다.  회사는 이전에 chilled 항목을 처리할 수 없습니다. 이제 음식 처리 요구를 달성 하기 위해가 냉각기 방 냉각기 섹션이 포함 된 해당 트럭 중 하나에 온도 모니터링 해야 합니다.

## <a name="workflow-for-warehouse-stock-items"></a>웨어하우스 주식 항목에 대 한 워크플로

항목은 누적 및 분산 하는 방법에 대 한 일반적인 흐름은 다음과 같습니다.
- WWI 구매 주문을 만들고 공급 업체에 주문을 제출 합니다.
- 공급 업체 항목을 보낼, WWI를 수신 합니다 및는 웨어하우스에서 구할 하 합니다.
- WWI에서 고객 주문 항목
- WWI 웨어하우스의 재고 항목을 사용 하 여 고객 주문을 채우고 공급 업체에서 추가 재고 주문 충분 한 재고가 없는 경우.
- 일부 고객은 재고가 없는 항목에 대 한 대기 하지 않으려는 합니다. 다른 5 개의 예를 들어 주문 주식 항목 및 4는 사용 가능한 경우 네 항목 및 나머지 항목 재고가 수신 하려는 합니다. 항목을 별도 배송 항목을 나중에 전송 됩니다.
- WWI 송장으로 순서를 전환 하 여 주식 항목에 대 한 고객은 일반적으로 송장 합니다.
- 고객 재고가 없는 항목을 주문할 수 있습니다. 이러한 항목은 미처리입니다.
- WWI 자신의 배달 van를 통하거나 다른 couriers 또는 freight 메서드를 통해 고객에 게 재고 항목을 제공합니다.
- 고객은 WWI에 청구서를 지불합니다.
- 정기적으로 WWI 구매 주문서에 있던 항목에 대 한 공급 업체를 지불 합니다. 이 종종 잠시 상품 받은 후입니다.

## <a name="data-warehouse-and-analysis-workflow"></a>데이터 웨어하우스 및 분석 워크플로

SQL Server Reporting Services를 사용 하 여 WideWorldImporters 데이터베이스에서 운영 보고서를 생성 하는 WWI 팀은를 전략적 보고서를 생성 해야 하는 데이터 분석을 수행도 필요 합니다. 팀은 WideWorldImportersDW 데이터베이스에서 차원 데이터 모델을 만들었습니다. 이 데이터베이스는 Integration Services 패키지에서 채워집니다.

SQL Server Analysis Services는 분석 데이터 모델을 만드는 데이터 차원 데이터 모델에서 사용 됩니다. SQL Server Reporting Services 보고서를 생성할 전략적 차원 데이터 모델에서 직접 및 분석 모델에서 사용 됩니다. Power BI 대시보드를 만드는 동일한 데이터에서 사용 됩니다. 대시보드는 휴대폰 및 태블릿 및 웹 사이트에서 사용 됩니다. *참고: 이러한 데이터 모델 및 보고서 아직 제공 되지 않습니다.*

## <a name="additional-workflows"></a>추가 워크플로

이들은 추가 워크플로입니다.
- WWI 문제 신용 정보 때 고객이 상품 잘못 된 경우 또는 어떤 이유로 good를 수신 하지 않습니다. 이 음수 송장으로 처리 됩니다.
- WWI는 주기적으로 시스템에 사용 가능한 것으로 표시 된 재고 수량 정확한 지 확인 하는 주식 항목의 보유 수량을 계산 합니다. (이 프로세스는 stocktake를 이라고) 합니다.
- 콜드 방 온도입니다. 부패 상품 refrigerated 대화방에 저장 됩니다. 이 대화방에서 센서 데이터 모니터링 및 분석을 위해 데이터베이스에 수집 됩니다.
- 차량 위치를 추적 합니다. WWI에 대 한 상품을 전송 하는 차량에 위치를 추적 하는 센서가 포함 됩니다. 이 위치는 다시 추가 모니터링 및 분석에 대 한 데이터베이스에 수집 됩니다.

## <a name="fiscal-year"></a>회계 연도

회사에서 11 월 1 일부 터 시작 하는 회계 연도 사용 하 여 작동 합니다.

## <a name="terms-of-use"></a>사용 약관

예제 데이터베이스 및 샘플 코드에 대 한 라이선스 여기에 설명 된: [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

샘플 데이터베이스 data.gov 및 자연 스러운 EarthData에서 로드 된 공용 데이터를 포함 합니다. 사용 약관은 다음과 같습니다. [https://www.naturalearthdata.com/about/terms-of-use/](https://www.naturalearthdata.com/about/terms-of-use/)
