---
title: 사용 되지 않는 DBCC CONCURRENCYVIOLATION 명령에 대 한 호출을 제거 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2cc9f6ff-de36-4e94-bd04-59f5c45c4911
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cde04ebfc2ea9996d1c9ed233123e5b66f6e81fa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065210"
---
# <a name="remove-calls-to-the-deprecated-dbcc-concurrencyviolation-command"></a>더 이상 사용되지 않는 DBCC CONCURRENCYVIOLATION 명령에 대한 호출을 제거합니다.
  업그레이드 관리자가 DBCC CONCURRENCYVIOLATION 명령 사용을 발견했습니다. 이 명령은 더 이상 사용할 수 없습니다. 이 명령을 실행하면 오류 2526이 반환됩니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 작업 관리자가 없기 때문에 이 명령이 제거되었습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 더 이상 사용되지 않는 이 명령에 대한 참조를 제거하도록 애플리케이션과 스크립트를 업데이트합니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
