---
title: 전체 텍스트 인덱스가 master, tempdb 및 model 데이터베이스에 없습니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1d334a3626c11050418df3fae483f5b9029adeb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080356"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>master, tempdb 및 model 데이터베이스에서는 전체 텍스트 인덱스가 지원되지 않습니다.
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 시스템 데이터베이스에 전체 텍스트 인덱스를 사용할 수 없습니다.  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서는 전체 텍스트 인덱스가 master, tempdb 및 model 데이터베이스에서 지원되었습니다.  
  
 Master, tempdb 및 model 데이터베이스의 모든 전체 텍스트 카탈로그 업그레이드 하는 동안 제거 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  