---
title: 쓰기 저장 대화 상자 (Analysis Services-Multidimensional Data) 사용-사용 안 함 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitiondesigner.writebackenabledisable.f1
ms.assetid: 2d254393-3f0d-4b70-8b98-87159f9f3639
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6682d8ced6b80e12aea783857da548498641ddd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069350"
---
# <a name="enable-disable-writeback-dialog-box-analysis-services---multidimensional-data"></a>쓰기 저장 대화 상자 (Analysis Services-Multidimensional Data) 사용-사용 안 함
  **쓰기 저장 사용/사용 안 함** 대화 상자를 사용하면 큐브의 측정값 그룹에 대해 쓰기 저장을 사용하거나 사용하지 않도록 설정할 수 있습니다. 측정값 그룹에 대해 쓰기 저장을 설정하면 쓰기 저장 파티션이 정의되고 해당 측정값 그룹에 대한 쓰기 저장 테이블이 생성됩니다. 측정값 그룹에 대해 쓰기 저장을 해제하면 쓰기 저장 파티션이 제거되지만 예기치 않은 데이터 손실을 방지하기 위해 쓰기 저장 테이블은 삭제되지 않습니다. 다음 작업을 수행하면 **쓰기 저장 사용/사용 안 함** 대화 상자가 표시됩니다.  
  
-   큐브 디자이너의 **파티션** 탭에서 **측정값 그룹** 창의 **쓰기 저장 설정** 을 클릭합니다.  
  
-   큐브 디자이너의 **파티션** 탭에 있는 **측정값 그룹** 창에서 **파티션** 표에 있는 파티션을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **쓰기 저장 설정** 을 선택합니다.  
  
## <a name="options"></a>변수  
 **테이블 이름**  
 선택한 파티션에 대해 만들려는 쓰기 저장 테이블의 이름을 입력합니다. 쓰기 저장 테이블은 클라이언트 애플리케이션의 측정값 그룹 변경 내용을 저장합니다.  
  
> [!NOTE]  
>  쓰기 저장을 설정하지 않으면 이 옵션도 사용할 수 없습니다.  
  
 **데이터 원본**  
 쓰기 저장 테이블을 포함할 데이터 원본을 선택합니다.  
  
> [!NOTE]  
>  쓰기 저장을 설정하지 않으면 이 옵션도 사용할 수 없습니다.  
  
 **새로 만들기**  
 **연결 관리자** 대화 상자를 표시하고 쓰기 저장 테이블을 포함할 새 데이터 원본을 정의하려면 클릭합니다.  
  
> [!NOTE]  
>  쓰기 저장을 설정하지 않으면 이 옵션도 사용할 수 없습니다.  
  
  
