---
title: 통계 업데이트 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.updatestatisticstask.f1
helpviewer_keywords:
- updating statistics
- Update Statistics task [Integration Services]
ms.assetid: 0247483b-f092-4511-8fa8-3610108bd1bc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d367886273ade6efab0c5d26017ed3ae6f5cd35b
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913857"
---
# <a name="update-statistics-task"></a>통계 업데이트 태스크

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  통계 업데이트 태스크는 지정된 테이블이나 인덱싱된 뷰에서 하나 이상의 통계 그룹(컬렉션)의 키 값 배포에 대한 정보를 업데이트합니다. 자세한 내용은 [통계](../../relational-databases/statistics/statistics.md)를 참조하세요.  
  
 통계 업데이트 태스크를 사용하면 패키지가 단일 데이터베이스나 여러 데이터베이스의 통계를 업데이트할 수 있습니다. 태스크가 단일 데이터베이스의 통계만 업데이트하는 경우 통계를 업데이트할 뷰 또는 테이블을 선택할 수 있습니다. 모든 통계, 열 통계만 또는 인덱스 통계만 업데이트하도록 구성할 수 있습니다.  
  
 이 태스크는 다음 인수와 절을 포함하여 UPDATE STATISTICS 문을 캡슐화합니다.  
  
-   *table_name* 또는 *view_name* 인수가 포함됩니다.  
  
-   업데이트가 모든 통계에 적용되면 WITH ALL 절이 포함됩니다.  
  
-   업데이트가 열에만 적용되면 WITH COLUMN 절이 포함됩니다.  
  
-   업데이트가 인덱스에만 적용되면 WITH INDEX 절이 포함됩니다.  
  
 통계 업데이트 태스크는 여러 데이터베이스의 통계를 업데이트하는 경우 각 테이블이나 뷰에 대해 하나씩, 여러 개의 UPDATE STATISTICS 문을 실행합니다. UPDATE STATISTICS의 모든 인스턴스는 동일한 절을 사용하지만 *table_name* 또는 *view_name* 값이 다릅니다. 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md) 및 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  태스크에서 실행할 Transact-SQL 문을 만드는 데 걸리는 시간은 태스크에서 업데이트하는 통계 수에 비례합니다. 많은 수의 인덱스가 있는 데이터베이스의 모든 테이블과 뷰의 통계를 업데이트하거나 여러 데이터베이스의 통계를 업데이트하도록 태스크를 구성하면 Transact-SQL 문을 생성하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="configuration-of-the-update-statistics-task"></a>통계 업데이트 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [통계 업데이트 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  
