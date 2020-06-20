---
title: 수정 된 데이터베이스를 사용 하 여 데이터베이스 다이어그램 조정 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- updating diagram to match database
- reconciling database diagrams
- diagrams [SQL Server], reconciling changes
- updating database to match diagram
- database diagrams [SQL Server], reconciling changes
ms.assetid: eda8dea2-eedd-43a7-85aa-92bd97783b5f
author: stevestein
ms.author: sstein
ms.openlocfilehash: f3d124a72caadc2d802765aa80d80baf5c6a3697
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048589"
---
# <a name="reconcile-a-database-diagram-with-a-modified-database-visual-database-tools"></a>수정된 데이터베이스와 데이터베이스 다이어그램 일치(Visual Database Tools)
  다이어그램에 일치하도록 데이터베이스를 업데이트할 준비가 되면 데이터베이스 다이어그램을 저장합니다. 그러나 다이어그램을 연 이후에 다른 사용자가 이미 데이터베이스를 업데이트한 경우에는 다른 사용자의 변경 내용이 현재 사용자의 다이어그램에 영향을 줄 수 있습니다. 그 반대의 경우도 마찬가지입니다.  
  
 이 상태에서 다이어그램을 저장하면 데이터베이스가 현재 사용자의 다이어그램에 일치하도록 조정됩니다. 즉, 다른 사용자의 변경 내용을 덮어쓰게 됩니다.  
  
### <a name="to-update-a-database-to-match-your-diagram"></a>다이어그램에 일치하도록 데이터베이스를 업데이트하려면  
  
1.  데이터베이스 다이어그램을 저장합니다.  
  
     다이어그램을 처음 저장하는 경우에는 **새 데이터베이스 다이어그램 저장** 대화 상자에 다이어그램의 이름을 입력하고 **확인**을 선택합니다.  
  
2.  다이어그램을 저장할 때 영향을 받는 테이블 목록이 **저장** 대화 상자에 표시됩니다. **예** 를 선택하여 작업을 계속 진행합니다.  
  
3.  다이어그램에 일치하도록 수정 및 변경되는 개체의 목록이 **데이터베이스 변경 감지** 대화 상자에 표시됩니다. **예** 를 선택하여 다이어그램을 저장하고 변경 목록을 승인합니다.  
  
    > [!NOTE]  
    >  데이터베이스에서 삭제한 테이블이나 열이 다이어그램에 포함되어 있으면 다이어그램을 저장할 때 해당 정의만 데이터베이스에 다시 작성됩니다. 이러한 개체를 삭제하기 전에 있던 데이터는 이 과정에서 복원되지 않습니다.  
  
### <a name="to-update-your-diagram-to-match-a-modified-database"></a>수정된 데이터베이스에 일치하도록 다이어그램을 업데이트하려면  
  
1.  변경 내용을 저장하지 않은 채 다이어그램을 닫습니다.  
  
2.  개체 탐색기에서 다이어그램을 마우스 오른쪽 단추로 클릭합니다.  
  
3.  바로 가기 메뉴에서 **새로 고침**을 클릭합니다.  
  
4.  다이어그램을 다시 엽니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 다이어그램 작업&#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
