---
title: SQL Server 유틸리티에 연결
description: SQL Server 리소스 상태를 관리할 수 있도록 SQL Server 유틸리티에 연결하는 방법을 알아봅니다. SSMS(SQL Server Management Studio)를 통해 연결할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fb961ccd1a1ec3013e186c7b45a54004ff400e07
ms.sourcegitcommit: e08d28530e0ee93c78a4eaaee8800fd687babfcc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86301792"
---
# <a name="connect-to-a-sql-server-utility"></a>SQL Server 유틸리티에 연결

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 연결하려면 먼저 UCP(유틸리티 제어 지점)를 만들어야 합니다. 자세한 내용은 [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)를 참조하세요.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스 상태를 보고 관리하려면 SSMS( [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] )를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 연결합니다.  

SSMS를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 연결하려면  

1. SSMS를 시작합니다.

2. SSMS에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결합니다.

3. **보기**를 선택한 다음, **유틸리티 탐색기**를 선택합니다.

4. 유틸리티 탐색기 탐색 창에서 :::image type="icon" source="media/connect-to-utility.gif" border="false":::**유틸리티에 연결**을 선택합니다.

5. **서버에 연결** 대화 상자에서 UCP 인스턴스 이름을 지정한 다음, **연결**을 선택합니다.

6. UCP의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스에 대한 트리 뷰를 보려면 유틸리티 탐색기 탐색 창을 보면 됩니다.

새 UCP를 만들어도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 연결됩니다. 자세한 내용은 [SQL Server 유틸리티 제어 지점 만들기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [SQL Server 유틸리티 기능 및 태스크](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [리소스 상태 정책 결과 보기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)