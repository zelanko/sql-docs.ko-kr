---
title: 사용 되지 않는 DBCC CONCURRENCYVIOLATION 명령에 대 한 호출을 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
caps.latest.revision: 7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2486546efae7daa63441e12fa350ef878c7daa77
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37261899"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>더 이상 사용되지 않는 DBCC CONCURRENCYVIOLATION 명령에 대한 호출을 제거합니다.
  업그레이드 관리자가 DBCC CONCURRENCYVIOLATION 명령 사용을 발견했습니다. 이 명령은 더 이상 사용할 수 없습니다. 이 명령을 실행하면 오류 2526이 반환됩니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 작업 관리자가 없기 때문에 이 명령이 제거되었습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 더 이상 사용되지 않는 이 명령에 대한 참조를 제거하도록 응용 프로그램과 스크립트를 업데이트합니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
