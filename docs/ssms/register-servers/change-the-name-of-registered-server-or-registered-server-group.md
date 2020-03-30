---
title: 등록된 서버 또는 등록된 서버 그룹 이름 변경
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/02/2016
ms.openlocfilehash: cefef29e85ea4494faaa10385c45fc45a77a7e1e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75258889"
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>등록된 서버 또는 등록된 서버 그룹 이름 변경

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 등록된 서버 또는 서버 그룹의 이름을 변경하는 방법에 대해 설명합니다. 이 이름은 언제든지 변경할 수 있습니다. 등록된 서버의 서버 이름을 변경하면 이름이 표시되는 방식만 변경됩니다. 다른 서버에 연결하려면 등록된 서버의 연결 속성을 편집해야 합니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용

메뉴에서 **보기\\등록된 서버**로 이동하여 **등록된 서버** 창을 엽니다.

### <a name="to-change-the-name-of-a-server"></a>서버 이름을 변경하려면

1. **등록된 서버**에서 **데이터베이스 엔진** , **로컬 서버 그룹**을 차례로 확장합니다.  

2. 서버를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택한 다음 **서버 등록 속성 편집** 대화 상자 창을 엽니다.

3. **등록된 서버 이름** 입력란에 서버 등록을 위해 새 이름을 입력한 다음 **저장**을 클릭합니다.  

### <a name="to-change-the-name-of-a-server-group"></a>서버 그룹의 이름을 변경하려면  

1. **등록된 서버**에서 **데이터베이스 엔진** , **로컬 서버 그룹**을 차례로 확장합니다.  

2. 서버 그룹을 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택한 다음 **서버 그룹 속성 편집** 대화 상자 창을 엽니다. 

3. **그룹 이름** 입력란에 서버 그룹의 새 이름을 입력한 다음 **저장**을 클릭합니다.  

## <a name="see-also"></a>참고 항목

[서버 등록 변경&#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)