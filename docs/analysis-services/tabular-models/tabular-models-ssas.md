---
title: 테이블 형식 모델 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 119cb1c2b92dc78784871ffd78b3fb69ffc9b228
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="tabular-models"></a>테이블 형식 모델
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  테이블 형식 모델은 메모리 내에서 또는 DirectQuery 모드에서 실행되어 백 엔드 관계형 데이터 원본에서 데이터에 직접 액세스하는 Analysis Services 데이터베이스입니다. 최신 상태 압축 알고리즘과 다중 쿼리 프로세서를 사용 하 여 분석 엔진 테이블 형식 모델 개체와 데이터에 대 한 빠른 액세스 Power BI 및 Excel 같은 클라이언트 응용 프로그램을 보고 하 여 제공 됩니다.  
  
 DirectQuery는 되어 있거나 모델에 대 한 대체 쿼리 모드는 메모리 내 모델은 기본값, 너무 커서 메모리에 또는 데이터 휘발성을 적절 한 처리 전략 불가능 합니다. DirectQuery 달성 다양 한 종류의 데이터 원본, 백 엔드 데이터베이스에 도달 하 고 쿼리 하는 DAX 식 통한 행 수준 보안이 DirectQuery 모델에서 계산 된 테이블 및 열을 처리할 수 있는 기능에 대 한 지원을 통해 메모리 내 모델을 통한 패리티 더 빠른 처리량을 최적화 합니다.
  
 테이블 형식 모델에서 만들어진 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 모델, 테이블, 관계 및 DAX 식을 만들기 위한 디자인 화면을 제공 하는 테이블 형식 모델 프로젝트 템플릿을 사용 하 여 합니다. 여러 원본에서 데이터를 가져온 다음 관계, 계산된 테이블/열, 측정값, KPI, 계층 및 변환을 추가하여 모델을 보강할 수 있습니다.  
  
 SQL Server Analysis Services 인스턴스의 테이블 형식 서버 모드용으로 구성 하거나 모델 Azure Analysis Services에 다음 배포할 수 있습니다. SQL Server Management Studio에서 배포 된 테이블 형식 모델을 관리할 수 있습니다. 모델 성장 함에 따라 처리 최적화를 위해 분할 하 고 수의 역할 기반 보안을 사용 하 여 행 수준 보안 합니다.  

  
  
