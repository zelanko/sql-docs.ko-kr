---
title: "Azure SQL 데이터베이스에서 R을 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: ef6573ca1d682ae4b4f4336ad6f809f1e094e9fc
ms.sourcegitcommit: 16347f3f5ed110b5ce4cc47e6ac52b880eba9f5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="using-r-in-azure-sql-database"></a>Azure SQL 데이터베이스에서 R을 사용 하 여

2017 년 1 월에서에서 SQL Server 개발 팀은 R 코드에서-데이터베이스의 SQL Server 2016에서 R 서비스와 비슷한 저장된 프로시저를 사용 하 여 실행을 지원 하려면 계획을 발표 했습니다. 이 기능은 아직 개발 중인 있습니다.

최신 공개 릴리스 일정 및 예정 된 이벤트를 유지 하려면 참조는 [SQL Server 블로그](https://blogs.technet.microsoft.com/dataplatforminsider/) 또는 [Microsoft R Server 블로그](https://blogs.msdn.microsoft.com/rserver/)합니다.

> [!IMPORTANT]
> 초기 미리 보기 릴리스를 발표 된 테스트 및 탐색만 되어있습니다. 현재 기능은을 제한 된 영역에 Azure SQL 데이터베이스에서 사용할 수와 기능이 2017 또는 SQL Server 2016에서 지원 되는 기능에 비해 제한 됩니다.

**Azure 리소스**

그 동안에 Azure 마켓플레이스에서 사용할 수 있는 SQL Server 2017 가상 컴퓨터 중 하나를 사용 하는 것이 좋습니다. 

+ [Azure 기계 학습에 대 한 가상 컴퓨터를 프로 비전](provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

또한 다양 한 도구를 학습 하는 인기 있는 컴퓨터와 미리 구성 된 상태로 이러한 Vm을 확인해 보세요.

+ [데이터 과학 가상 컴퓨터](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)
+ [가상 컴퓨터를 심층 학습](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview), 

