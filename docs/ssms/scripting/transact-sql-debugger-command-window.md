---
title: 명령 창
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 226acc4696b5edacde3b6950c10c8b5370e29b42
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243426"
---
# <a name="transact-sql-debugger---command-window"></a>Transact-SQL 디버거 - 명령 창

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**명령 창** 을 사용하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 쿼리 편집기 창에서 현재 디버깅 중인 코드에 디버그 및 편집 명령과 같은 명령을 실행합니다. **명령 창**을 사용하려면 디버그 모드여야 합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **명령** 창에서도 지원되는 많은 명령을 지원합니다. 자세한 내용은 [Visual Studio 명령 창](https://go.microsoft.com/fwlink/?LinkId=112007)을 참조하십시오.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>작업 목록

**명령 창에 액세스하려면**

- **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.

**변수 값을 인쇄하려면**

- **명령 창**에서 **Debug.Print \<VariableName>** 을 입력하고 Enter 키를 누릅니다.

**현재 스레드에 대한 정보를 표시하려면**

- **명령 창**에서 **Debug.ListThread**를 입력하고 Enter 키를 누릅니다.

**간략한 조사식 창에 변수를 추가하려면**

- **명령 창**에서 **Debug.QuickWatch \<VariableName>** 을 입력하고 Enter 키를 누릅니다.

## <a name="see-also"></a>참고 항목

[Transact-SQL 디버거](../../relational-databases/scripting/transact-sql-debugger.md)
