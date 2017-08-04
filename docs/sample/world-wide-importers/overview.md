---
title: "개요 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/30/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d4dcb00-b93e-44db-9d67-061702bba41a
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e5a3dd9c765c347b7516706d6e157a47f3c9bd03
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="wide-world-importers-overview"></a>방법 개요
이것이 회사인 Wide World Importers 및 SQL Server 및 Azure SQL 데이터베이스에 대 한 WideWorldImporters 예제 데이터베이스에 주소가 지정 된 워크플로에 대 한 개요입니다.  

Wide World Importers (WWI)은 도매 새로 움 상품 가져오기 및 배포자 샌프란시스코 베이 영역에서 작동 합니다.

도매업, WWI의 고객이 개인에 게 재판매할 회사 대부분 됩니다. WWI 판매 소매 고객에 게 슈퍼마켓, specialty 저장소를 포함 하 여 미국에서 여행자 인력 상점 상점과 일부 사용자를 계산 합니다. 또한 WWI WWI의를 대신 하 여 제품을 승격 하는 네트워크를 통해 다른 wholesalers를 판매 합니다. 미국에서 기반으로 현재 모든 WWI의 고객 하는 동안 회사 확장에 대 한 다른 국가 밀어넣을 예정입니다.

WWI 새로 움 장난감 제조업체 및 기타 새로 움 wholesalers 포함 하는 공급 업체에서 제품을 구입 합니다. 고객 주문을 수행할 수 있도록 하는 데 필요한 만큼 WWI 웨어하우스 및 순서 바꾸기 공급 업체에서 제품 원가 판매 합니다. 또한 많은 양의 자료 패키징 구입 하 고 고객에 대 한 편의 위해 작은 수량에 이러한 판매 합니다.

최근에 WWI 초콜릿 식용 novelties chilli 등의 다양 한 판매를 시작 했습니다.  회사는 이전에 chilled 항목을 처리할 수 없었습니다. 이제 음식 처리 요구를 충족 하기 위해 냉각기 방에 냉각기 섹션을 갖는 해당 트럭의 온도 모니터링 해야 합니다.

## <a name="workflow-for-warehouse-stock-items"></a>웨어하우스 스톡 항목에 대 한 워크플로

항목 되어 재고로 하 게 분산 하는 방법에 대 한 일반적인 흐름은 다음과 같습니다.
- WWI 구매 주문을 만들고 공급 업체에 주문을 제출 합니다.
- 공급 업체 항목 보낼, WWI 수신 하 고 자신의 웨어하우스에를 구할 합니다.
- WWI에서 고객 주문 항목
- WWI 웨어하우스에서 스톡 항목과 고객 주문 채우고 공급 업체에서 추가 재고 주문 때 충분 한 재고를 갖지 않습니다.
- 일부 고객의 재고가 없는 항목에 대해 기다려야 안 됩니다. 서로 다른 5 예: 주문 스톡 항목 및 4 개를 사용할 수, 4 개 항목 및 나머지 항목 재고가 수신 하려면. 항목을 별도 배송의 뒷부분에 나오는 보낼 수는 있습니다.
- WWI 순서 송장으로 변환 하 여 재고 항목에 대 한 고객 일반적으로 송장 합니다.
- 고객의 재고가 없는 항목을 주문할 수 있습니다. 이러한 항목은 미처리입니다.
- WWI 자신의 배달 van을 통해 또는 다른 couriers 또는 운송 방법을 통해 고객에 게 재고 항목을 제공합니다.
- 고객은 WWI를 송장을 지불합니다.
- 정기적으로, WWI 구매 주문서에서 항목에 대 한 공급 업체를 유용 합니다. 이 종종 잠시 상품 받은 후 합니다.

## <a name="data-warehouse-and-analysis-workflow"></a>데이터 웨어하우스 및 분석 워크플로

WideWorldImporters 데이터베이스에서 작업 보고서를 생성 하기 위해 SQL Server Reporting Services를 사용 하는 팀 WWI에서, 해야가 데이터에 대해 분석을 수행 하 고 전략적 보고서를 생성 해야 합니다. 팀은 WideWorldImportersDW 데이터베이스에서 차원 데이터 모델을 만들었습니다. 이 데이터베이스는 Integration Services 패키지에 의해 채워집니다.

SQL Server Analysis Services 차원 데이터를 모델의 데이터에서 분석 데이터 모델을 만드는 사용 됩니다. SQL Server Reporting Services 보고서를 생성할 전략적 차원 데이터를 모델에서 직접 및 분석 모델에서 사용 됩니다. Power BI 대시보드를 만들려면 동일한 데이터에서 사용 됩니다. 대시보드는 휴대폰 및 태블릿 및 웹 사이트에 사용 됩니다. *참고: 이러한 데이터 모델 및 보고서 아직 제공 되지 않습니다.*

## <a name="additional-workflows"></a>추가 워크플로

이들은 추가 워크플로입니다.
- 어떤 이유로 또는 물품은 잘못 된 경우 고객 WWI 문제 신용 정보 good를 받지 않습니다. 이러한 값은 음수 송장으로 취급 됩니다.
- 주기적으로 WWI가 시스템에 사용 가능으로 표시 하는 재고 수량 정확 하 게 되도록 스톡 항목 보유 수량을 계산 합니다. (이 작업의 프로세스는 stocktake를 라고) 합니다.
- 콜드 방 온도 합니다. 일회용 상품 refrigerated 대화방에 저장 됩니다. 이 대화방에서 센서 데이터는 수집 된 모니터링 및 분석 목적으로 데이터베이스에 있습니다.
- 자동차 위치를 추적 합니다. 위치를 추적 하는 센서 포함 하는 차량 상품 WWI에 대 한 전송입니다. 이 위치는 다시 수집 된 추가 모니터링 및 분석에 대 한 데이터베이스에 있습니다.

## <a name="fiscal-year"></a>회계 연도

회사에서 11 월 1 일부 터 시작 하는 회계 연도 사용 하 여 작동 합니다.

## <a name="terms-of-use"></a>사용 약관

예제 데이터베이스와 예제 코드에 대 한 라이선스 여기에 설명 된: [license.txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

샘플 데이터베이스 data.gov 및 자연 EarthData에서 로드 된 공용 데이터를 포함 합니다. 사용 약관에는 여기: [http://www.naturalearthdata.com/about/terms-of-use/](http://www.naturalearthdata.com/about/terms-of-use/)

