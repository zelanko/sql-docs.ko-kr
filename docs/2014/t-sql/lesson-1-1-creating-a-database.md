---
title: 데이터베이스 만들기(자습서) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- tutorial creating a database
ms.assetid: e1e2c83f-dfad-4bb8-aa7a-09d3f69517ae
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c0353c89dbfc14032d33dfa49fa0c08e698cb5c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211215"
---
# <a name="creating-a-database-tutorial"></a>데이터베이스 만들기(자습서)
  많은 [!INCLUDE[tsql](../includes/tsql-md.md)] 문과 마찬가지로 CREATE DATABASE 문에는 필수 매개 변수로 데이터베이스 이름이 있습니다. 또한 CREATE DATABASE에는 데이터베이스 파일을 저장할 디스크 위치와 같은 많은 선택적 매개 변수가 있습니다. 선택적 매개 변수 없이 CREATE DATABASE를 실행할 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 이러한 여러 매개 변수에 기본값을 사용합니다. 이 자습서에서는 아주 약간의 선택적 구문 매개 변수만 사용합니다.  
  
### <a name="to-create-a-database"></a>데이터베이스를 만들려면  
  
1.  쿼리 편집기 창에서 다음 코드를 입력하되 실행하지는 않습니다.  
  
    ```  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  포인터를 사용하여 `CREATE DATABASE`단어를 선택한 다음 **F1**키를 누릅니다. SQL Server 온라인 설명서의 CREATE DATABASE 항목이 열립니다. 이 기술을 사용하여 CREATE DATABASE 및 이 자습서에 사용되는 다른 문의 전체 구문을 찾을 수 있습니다.  
  
3.  쿼리 편집기에서 **F5** 키를 눌러 문을 실행하고 `TestData`라는 데이터베이스를 만듭니다.  
  
 데이터베이스를 만들 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 는 **model** 데이터베이스의 복사본을 만들고 복사본의 이름을 데이터베이스 이름으로 바꿉니다. 선택적 매개 변수로 데이터베이스의 처음 크기를 큰 값으로 지정하지 않은 경우 이 작업은 몇 초 내에 수행되어야 합니다.  
  
> [!NOTE]  
>  단일 일괄 처리에서 둘 이상의 문을 전송할 경우 GO 키워드는 문을 구분합니다. 일괄 처리에 문이 하나만 포함된 경우 GO는 선택 사항입니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [테이블 만들기&#40;자습서&#41;](lesson-1-2-creating-a-table.md)  
  
## <a name="see-also"></a>관련 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
