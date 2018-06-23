---
title: 기록 보존 기간 설정(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- history retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: c288daab-5181-4d4b-ba2a-8a147098e758
caps.latest.revision: 34
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bc2bed6e9f65245168ec9fac3160345e80371d62
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080206"
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>기록 보존 기간 설정(SQL Server Management Studio)
  **배포 데이터베이스 속성 - \<DistributionDatabase>** 대화 상자의 **일반** 페이지에서 기록 보존 기간을 지정합니다. 이 설정은 복제 에이전트 기록이 저장되는 기간을 제어합니다. **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 이 페이지를 사용할 수 있습니다. 이 대화 상자에 액세스하는 방법은 [배포자 및 게시자 속성 보기 및 수정](view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
### <a name="to-specify-the-history-retention-period"></a>기록 보존 기간을 지정하려면  
  
1.  **배포자 속성 - \<Distributor>** 대화 상자의 **일반** 페이지에서 배포 데이터베이스에 대한 속성 단추(**…**)를 클릭합니다.  
  
2.  **최소 다음 기간 동안 복제 성능 기록 저장** 상자에 값을 입력합니다.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [배포 구성](configure-distribution.md)  
  
  