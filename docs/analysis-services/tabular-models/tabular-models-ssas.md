---
title: Analysis Services에서 테이블 형식 모델 | Microsoft Docs
ms.date: 09/17/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae7dfd78e71c41ab5b826a27742923445117417d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162431"
---
# <a name="tabular-models"></a>테이블 형식 모델
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  Analysis Services에서 테이블 형식 모델은 메모리 내 또는 원본 백 엔드 관계형 데이터에서 직접 데이터에 연결 하는 DirectQuery 모드에서 실행 되는 데이터베이스입니다. 최첨단 비교 알고리즘과 다중된 쿼리 프로세서를 사용 하 여 Analysis Services Vertipaq 분석 엔진은 빠른 액세스 Power BI 및 Excel과 같은 클라이언트 응용 프로그램을 보고 하 여 테이블 형식 모델 개체 및 데이터에 제공 합니다.  
  
 DirectQuery 모델 중 하나에 대해서는 대체 쿼리 모드는 메모리 내 모델은 기본값 이므로 하는 동안 너무 커서 메모리에 또는 데이터 변동성에 적절 한 처리 전략을 인덱스나 관계에 맞지 않습니다. DirectQuery는 다양 한 데이터 원본에 DirectQuery 모델에서 백 엔드 데이터베이스에 연결 하 고 쿼리 하는 DAX 식 통한 행 수준 보안이 열 및 계산 된 테이블을 처리 하는 기능에 대 한 지원을 통해 메모리 내 모델을 사용 하 여의 패리티를 실현 합니다. 처리량이 더 발생 하는 최적화 합니다.
  
 테이블 형식 모델에서 만들어진 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 테이블 형식 모델 프로젝트 템플릿을 사용 하 여 합니다. 프로젝트 템플릿에 테이블, 파티션, 관계, 계층, 측정값 및 Kpi와 같은 의미 체계 모델 개체를 만들기 위한 디자인 화면을 제공 합니다. 
  
 Azure Analysis Services 또는 테이블 형식 서버 모드용으로 구성 하는 SQL Server Analysis Services 인스턴스의 테이블 형식 모델을 배포할 수 있습니다. SQL Server Management Studio에서 배포 된 테이블 형식 모델을 관리할 수 있습니다. 

여기에 포함 된 테이블 형식 모델링 설명서는 대부분의 경우 SQL Server Analysis Services와 Azure Analysis Services에 적용 됩니다. Azure Analysis Services에 특정 된 문서는 다른 Azure 문서와 함께 게시 됩니다. 자세한 내용은 참조 하세요 [Azure Analysis Services 설명서](https://docs.microsoft.com/azure/analysis-services/)합니다.
  
