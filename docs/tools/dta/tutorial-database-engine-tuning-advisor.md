---
title: '자습서: 데이터베이스 엔진 튜닝 관리자 | Microsoft 문서'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
- tutorials [Database Engine Tuning Advisor]
ms.assetid: 3b54cbbe-d8c6-424d-92f1-aa58179f4da8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6c557c537bd4b6f0eaec6b59d1f753200528445c
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67731750"
---
# <a name="tutorial-database-engine-tuning-advisor"></a>자습서: 데이터베이스 엔진 튜닝 관리자
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
데이터베이스 엔진 튜닝 관리자 자습서를 시작합니다. 사용자가 지정한 데이터베이스에서 쿼리를 처리하는 방법을 검사한 다음 인덱스, 인덱싱된 뷰 및 분할과 같은 데이터베이스 구조를 수정하여 쿼리 처리 성능을 높일 수 있는 방법을 권장합니다.  
  
데이터베이스 엔진 튜닝 관리자는 GUI(그래픽 사용자 인터페이스)와 **dta** 명령 프롬프트 유틸리티의 두 가지 사용자 인터페이스를 제공합니다. GUI를 사용하면 튜닝 세션의 결과를 빠르게 볼 수 있고 **dta** 유틸리티를 사용하면 데이터베이스 엔진 튜닝 관리자 기능을 스크립트에 쉽게 통합하여 튜닝을 자동화할 수 있습니다. 또한 데이터베이스 엔진 튜닝 관리자는 XML 입력을 받아들일 수 있고 자세히 튜닝 프로세스를 제어할 수 있습니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서에서는 데이터베이스 엔진 튜닝 관리자 GUI를 탐색하는 방법과 GUI와 **dta** 유틸리티를 모두 사용하여 일부 기본 태스크를 수행하는 방법을 배웁니다. 다음 단원이 포함됩니다.  
  
[1단원: 데이터베이스 엔진 튜닝 관리자 기본 탐색](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
이 단원에서는 새 데이터베이스 엔진 튜닝 관리자 GUI에 익숙해지고 표시 옵션과 레이아웃을 설정하는 방법을 배웁니다.  
  
[2단원: 데이터베이스 엔진 튜닝 관리자 사용](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
이 단원에서는 데이터베이스 엔진 튜닝 관리자 GUI로 기본 튜닝 태스크를 수행하는 방법을 배웁니다.  
  
[3단원: dta 명령 프롬프트 유틸리티 사용](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
이 단원에서는 **dta** 명령 프롬프트 유틸리티를 시작하는 방법과 일부 단순 튜닝 명령을 실행하는 방법을 알아봅니다.  
  
## <a name="requirements"></a>요구 사항  
이 자습서는 데이터베이스 엔진 튜닝 관리자 GUI나 **dta** 명령 프롬프트 유틸리티에는 익숙하지 않지만 데이터베이스 개념과 인덱스 및 인덱싱된 뷰와 같은 구조에는 많은 경험이 있는 데이터베이스 관리자를 대상으로 합니다.  
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 예제 데이터베이스가 포함된 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] (또는 최신 버전)를 설치해야 합니다. 보안을 위해 예제 데이터베이스는 기본적으로 설치되지 않습니다. 예제 데이터베이스를 설치하려면 [SQL Server 예제 및 예제 데이터베이스](https://sqlserversamples.codeplex.com)를 참조하세요.  
  
## <a name="after-you-finish-this-tutorial"></a>이 자습서를 마친 후  
이 자습서의 학습을 마친 후에는 다음 항목을 참조하여 데이터베이스 엔진 튜닝 관리자에 대한 자세한 내용을 보십시오.  
  
-   [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) - 이 도구로 태스크를 수행하는 방법에 대한 설명  
  
-   [dta Utility](../../tools/dta/dta-utility.md) - 유틸리티 작업을 제어하는 데 사용할 수 있는 명령 프롬프트 유틸리티 및 선택적 XML 파일에 대한 참조 자료  
  
## <a name="next-lesson"></a>다음 단원  
[1단원: 데이터베이스 엔진 튜닝 관리자 기본 탐색](../../tools/dta/lesson-1-basic-navigation-in-database-engine-tuning-advisor.md)  
  
  
  
