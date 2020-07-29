---
title: 서버 그룹 만들기 또는 편집
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.editgroup.f1
- sql13.swb.newgroup.f1
helpviewer_keywords:
- Registered Servers [SQL Server], server groups
- server groups [SQL Server]
- groups [SQL Server], server
ms.assetid: d4a942bd-2dd1-42db-ad0e-e9a9ae5b856d
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: eb39627de23f236dcd3a7241f83883b747353501
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001746"
---
# <a name="create-or-edit-a-server-group-sql-server-management-studio"></a>서버 그룹 만들기 또는 편집(SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 서버 그룹을 만들고 등록된 서버를 서버 그룹에 배치하여 등록된 서버에서 서버를 구성하는 방법에 대해 설명합니다. 언제든지 등록된 서버에서 서버 그룹을 만들고, 또한 서버를 등록할 때 서버 그룹을 만들 수도 있습니다.  

## <a name="SSMSProcedure"></a>

### <a name="to-create-a-server-group-in-registered-servers"></a>등록된 서버에 서버 그룹을 만들려면  

1. 등록된 서버의 등록된 서버 도구 모음에서 해당 서버 유형을 클릭합니다. 등록된 서버가 표시되지 않으면 **보기** 메뉴에서 **등록된 서버** 를 클릭합니다.  

2. 서버 또는 서버 그룹을 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **서버 그룹**을 클릭합니다.  

3. **새 서버 그룹** 대화 상자의 **그룹 이름** 목록 상자에 서버 그룹의 고유한 이름을 입력합니다. 서버 그룹 이름은 등록된 서버 트리의 현재 위치에서 고유해야 합니다.

4. 필요에 따라 **그룹 설명** 목록 상자에 서버 그룹을 설명하는 이름을 입력합니다(예: "라틴 아메리카 금융 서버").  

5. **새 서버 그룹의 위치를 선택하세요.** 상자에서 그룹의 위치를 클릭한 다음 **저장**을 클릭합니다.  

   > [!NOTE]
   > 이외에도 서버를 등록할 때 **새 그룹**을 클릭하고 **새 그룹** 대화 상자를 완료하면 새 서버 그룹을 만들 수 있습니다.  

## <a name="see-also"></a>참고 항목

[서버 등록](../../tools/sql-server-management-studio/register-servers.md)