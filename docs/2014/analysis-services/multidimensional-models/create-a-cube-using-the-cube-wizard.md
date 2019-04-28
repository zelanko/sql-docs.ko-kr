---
title: 큐브 마법사를 사용 하 여 큐브 만들기 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7545bc1e1ad37ff395f3e4c3f65b1cb4614e533e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726897"
---
# <a name="create-a-cube-using-the-cube-wizard"></a>큐브 마법사를 사용하여 큐브 만들기
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 큐브 마법사를 사용하여 새 큐브를 만들 수 있습니다.  
  
### <a name="to-create-a-new-cube"></a>새 큐브를 만들려면  
  
1.  **솔루션 탐색기**에서 **큐브**를 마우스 오른쪽 단추로 클릭한 다음 **새 큐브**를 클릭합니다.  
  
2.  큐브 마법사의 **생성 방법 선택** 페이지에서 **기존 테이블 사용**을 선택한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  기존 테이블 없이 큐브를 만들어야 하는 경우도 있습니다. 빈 큐브를 만들려면 **빈 큐브 만들기**를 선택하고 테이블을 생성하려면 **데이터 원본에 테이블 생성**을 선택하십시오.  
  
3.  **측정값 그룹 테이블 선택** 페이지에서 다음 절차를 수행합니다.  
  
    1.  **데이터 원본 뷰** 목록에서 데이터 원본 뷰를 선택합니다.  
  
    2.  **측정값 그룹 테이블** 목록에서 측정값 그룹을 만드는 데 사용할 테이블을 선택합니다.  
  
    3.  **다음**을 클릭합니다.  
  
4.  **측정값 선택** 페이지에서 큐브에 포함할 측정값을 선택한 후 **다음**을 클릭합니다.  
  
     경우에 따라 측정값 및 측정값 그룹의 이름을 변경할 수도 있습니다.  
  
5.  **기존 차원 선택** 페이지에서 큐브에 포함할 기존 차원을 선택한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  선택한 측정값 그룹의 데이터베이스에 차원이 이미 있으면 **기존 차원 선택** 페이지가 나타납니다.  
  
6.  **새 차원 선택** 페이지에서 새로 만들 차원을 선택한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  아무 테이블이나 차원 테이블로 사용할 수 있고 기존 차원에서 이러한 테이블을 아직 사용하지 않은 경우 **새 차원 선택** 페이지가 나타납니다.  
  
7.  **누락 차원 키 선택** 페이지에서 차원의 키를 선택한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  지정한 모든 차원 테이블에 키가 정의되어 있지 않으면 **누락 차원 키 선택** 페이지가 나타납니다.  
  
8.  **마법사 완료** 페이지에서 새 큐브의 이름을 입력하고 큐브 구조를 검토합니다. 변경하려면 **뒤로**를 클릭하고 변경하지 않으려면 **마침**을 클릭합니다.  
  
    > [!NOTE]  
    >  큐브 마법사를 완료한 후 큐브 디자이너를 사용하여 큐브를 구성할 수 있습니다. 또한 차원 디자이너를 사용하여 만든 차원에서 특성과 계층을 추가, 제거 및 구성할 수도 있습니다.  
  
  
