---
title: Master, tempdb 및 model 데이터베이스에서는 전체 텍스트 인덱스가 지원 되지 않습니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 743c7153b034cf5e1267c6a0da1e585845800980
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095196"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>master, tempdb 및 model 데이터베이스에서는 전체 텍스트 인덱스가 지원되지 않습니다.
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 시스템 데이터베이스에 전체 텍스트 인덱스를 사용할 수 없습니다.  
  
## <a name="description"></a>설명  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서는 전체 텍스트 인덱스가 master, tempdb 및 model 데이터베이스에서 지원되었습니다.  
  
 Master, tempdb 및 model 데이터베이스의 전체 텍스트 카탈로그는 업그레이드 하는 동안 제거 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
