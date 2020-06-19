---
title: 데이터베이스 다이어그램 디자인(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65536
- vdt.DatabaseDesigner
helpviewer_keywords:
- Database Diagram Designer
- Visual Database Tools [SQL Server], database diagrams
- database diagrams [SQL Server], designing
- diagrams [SQL Server], designing
ms.assetid: 6d2c14e1-3d73-4d10-ae5b-7f2b5d6c4ea8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 78c8bb22ba6fdeb9e39b7173c4975af22d5124a2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044430"
---
# <a name="design-database-diagrams-visual-database-tools"></a>데이터베이스 다이어그램 디자인(Visual Database Tools)
  데이터베이스 디자이너는 연결할 데이터베이스를 디자인하고 시각화할 수 있게 하는 비주얼 도구입니다. 데이터베이스를 디자인할 때 데이터베이스 디자이너를 사용하여 테이블, 열, 키, 인덱스, 관계, 제약 조건 등을 만들거나 편집하거나 삭제할 수 있습니다. 데이터베이스를 시각화하기 위해 테이블, 열, 키, 관계의 일부 또는 전부를 표시하는 다이어그램을 하나 이상 만들 수 있습니다.  
  
 ![테이블 관계를 보여 주는 데이터베이스 다이어그램](../../database-engine/media//dv3w7c1.gif "테이블 관계를 보여 주는 데이터베이스 다이어그램")  
  
 모든 데이터베이스에 대해 필요한 수만큼 데이터베이스 다이어그램을 만들 수 있습니다. 각 데이터베이스 테이블을 표시하는 다이어그램의 수에는 제한이 없습니다. 따라서 서로 다른 다이어그램을 만들어 데이터베이스의 다른 부분을 시각화하거나 디자인의 다른 부분을 강조할 수 있습니다. 예를 들어, 모든 테이블과 열을 표시하는 큰 다이어그램을 만들 수 있고 열은 표시하지 않고 테이블만 모두 표시하는 작은 다이어그램을 만들 수도 있습니다.  
  
 사용자가 만든 각 데이터베이스 다이어그램은 관련 데이터베이스에 저장됩니다.  
  
## <a name="tables-and-columns-in-a-database-diagram"></a>데이터베이스 다이어그램의 테이블 및 열  
 데이터베이스 다이어그램의 각 테이블에는 세 가지 고유 기능인 제목 표시줄, 행 선택기 및 속성 열 집합이 표시될 수 있습니다.  
  
 **제목 표시줄** 제목 표시줄에는 테이블 이름이 표시됩니다.  
  
 테이블을 수정한 다음 아직 저장하지 않은 경우 테이블 이름의 끝에 별표(*)가 표시되어 변경 내용이 저장되지 않았음을 나타냅니다. 수정된 테이블 및 다이어그램을 저장하는 방법에 대한 자세한 내용은 [데이터베이스 다이어그램 작업&#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
 **행 선택기** 행 선택기를 클릭하여 테이블에서 데이터베이스 열을 선택할 수 있습니다. 행 선택기는 해당 열이 테이블의 기본 키에 있는 경우 키 기호를 표시합니다. 기본 키에 대 한 자세한 내용은 [primary And Foreign Key 제약 조건](../../relational-databases/tables/primary-and-foreign-key-constraints.md)을 참조 하세요.  
  
 **속성 열** 속성 열 집합은 테이블의 특정 뷰에만 표시됩니다. 다섯 가지 뷰 형식 중 하나를 사용하여 테이블을 볼 수 있으며, 이를 통해 다이어그램의 크기 및 레이아웃을 쉽게 관리할 수 있습니다.  
  
 테이블 뷰에 대한 자세한 내용은 [다이어그램에 표시된 정보의 양 사용자 지정&#40;Visual Database Tools&#41;](customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md)을 참조하세요.  
  
## <a name="relationships-in-a-database-diagram"></a>데이터베이스 다이어그램에서의 관계  
 데이터베이스 다이어그램의 각 관계는 세 가지 고유 기능인 엔드포인트, 선 스타일 및 관련 테이블을 사용하여 나타낼 수 있습니다.  
  
 **엔드포인트** 선의 엔드포인트는 관계가 일 대 일 관계인지 일 대 다 관계인지를 나타냅니다. 관계의 한 엔드포인트에 키가 있고 다른 엔드포인트에 숫자 8이 있는 경우 이는 일 대 다 관계이며, 관계의 각 엔드포인트에 키가 있는 경우 일 대 일 관계입니다.  
  
 **선 스타일** 선의 엔드포인트가 아니라 선 자체는 외래 키 테이블에 데이터를 새로 추가하는 경우 DBMS(데이터베이스 관리 시스템)에서 관계에 대한 참조 무결성을 적용할지 여부를 나타냅니다. 선이 실선으로 표시되면 외래 키 테이블에서 행을 추가하거나 수정할 때 DBMS에서 관계에 대한 참조 무결성을 적용합니다. 그러나 선이 점선으로 표시되면 외래 키 테이블에서 행을 추가하거나 수정할 때 DBMS에서 관계에 대한 참조 무결성을 적용하지 않습니다.  
  
 **관련 테이블** 관계 선은 한 테이블과 다른 테이블 사이에 외래 키 관계가 있음을 나타냅니다. 일 대 다 관계의 경우 외래 키 테이블은 선의 숫자 8 기호 옆에 있는 테이블입니다. 선의 두 엔드포인트가 모두 같은 테이블에 연결되면 반사 관계입니다. 자세한 내용은 [반사 관계 그리기&#40;Visual Database Tools&#41;](draw-reflexive-relationships-visual-database-tools.md)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터베이스 다이어그램 소유권 이해&#40;Visual Database Tools&#41;](understand-database-diagram-ownership-visual-database-tools.md)  
  
 [데이터베이스 다이어그램 디자이너에서 탐색&#40;Visual Database Tools&#41;](navigate-in-database-diagram-designer-visual-database-tools.md)  
  
 [데이터베이스 다이어그램 디자이너 설정&#40;Visual Database Tools&#41;](set-up-database-diagram-designer-visual-database-tools.md)  
  
 [이전 버전에서 데이터베이스 다이어그램 업그레이드&#40;Visual Database Tools&#41;](upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
  
 [데이터베이스 다이어그램 디자이너 열기&#40;Visual Database Tools&#41;](open-database-diagram-designer-visual-database-tools.md)  
  
## <a name="see-also"></a>참고 항목  
 [Visual Database Tools를 &#40;데이터베이스 다이어그램 작업&#41;](visual-database-tools.md)   
 [데이터베이스 다이어그램에서 테이블 작업 &#40;Visual Database Tools&#41;](work-with-tables-in-database-diagram-visual-database-tools.md)   
 [다이어그램 레이아웃 작업&#40;Visual Database Tools&#41;](work-with-diagram-layout-visual-database-tools.md)  
  
  
